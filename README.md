グループ構成　イマズ　クバ　リョウジ　ヨシノ

###---------担当　クバ---------

#TMUX導入

参考にしたサイト

http://kanjuku-tomato.blogspot.jp/2014/02/tmux.html

http://monopocket.jp/blog/programming/1845/

##TMUXとは
tmux とは GNU Screenと同じ仮想端末管理ソフトウェアである。tmux はターミナル上における作業の使いやすさを大幅に向上させるものです。

メリットとして
* 複数の端末を軌道でき、タブのように切り替えができる
* 端末の画面分割ができる
* 端末を複数のユーザーで共有できる


##導入手順

tmuxをインストールします。

`$ sudo apt-get install tmux`

ここで404エラーが出た場合は/etc/apt/source.listファイルを編集する必要があります。
http://repogen.simplylinux.ch/　
で住んでる国とUbuntuのバージョンを入れて必要なものにチェックを入れると自動的にsources.listを生成できます。
ここで生成したコードの一番上を/etc/apt/source.listファイルにコピーし

`$ sudo apt-get update`

を実行しエラーがでなければ先ほどのコマンドを実行し完了となります。

使い方はこちらから

http://room6933.com/mymemo/tmux/tmux-basic.html
<br />


なお端末を複数のユーザーで共有する場合はopenssh-serverが必要となります。


#実装できなかった機能

##パスワードリマインダ

参考にしたサイト

http://qiita.com/ytr_i/items/0907ee3312ed9d79c9e8

###実装したかった機能
* Sign up済みアカウントのパスワードをリセット
* Gmailで再登録用のURLを送信






###---------担当　今頭---------

#「いいねボタン実装してみた」

参考にしたサイトはコチラ↴  
http://easyramble.com/activerecord-reputation-system.html  
http://railscasts.com/episodes/364-active-record-reputation-system?language=ja&view=asciicast

##まずはインストール  
初めにGemファイルに下記を追加します

```Gemfile
gem 'activerecord-reputation-system', github: 'NARKOZ/activerecord-reputation-system', branch: 'rails4'
```

追加場所は今までチュートリアルで追加してきたもののすぐ下の方でも大丈夫だと思います。

続いて、ターミナルでインストールからの～マイグレーションまでしましょう。

```ターミナルで打つコマンド
$ bundle install  
$ bundle exec rails generate reputation_system  
$ bundle exec rake db:migrate
```

しかし環境によってはインストールそのものができない場合があるかもしれませんので、  
その時は諦めましょう。（自分のパソコンで失敗したため...乙。）

続いて、マイグレーションまでちゃんと成功したら  
####「いいね」を導入したい対象のモデルに**has_reputation**を追加しましょう。

と言うことで今回はチュートリアルに沿って作成される、**micropost.rb**に追加したいと思います。  
ファイル場所　　/app/models/micropost.rb
```micropost.rb
class Micropost < ActiveRecord::Base  
  has_reputation :votes, source: :user, aggregated_by: :sum #追加 
  .  
  .  
  . 
end
```

つぎに**routes.rb**に新たに**resources**追加します。  
ファイル場所　　/config/routes.rb
```/config/routes.rb
AkisApp::Application.routes.draw do
  .
  .
  .
  resources :microposts, only: [:create, :destroy]
  resources :microposts do  #新しく追加するresources
    member do
      post :vote
    end
  end   #ここまで
  .
  .
  .
end
```

###「いいね」ボタンのアクションを作成

**microposts_controller.rb**に「いいね」用のアクションを作りましょう。  
上記で**post :vote**としているため**def vote**として作ります。  
ファイル場所　　/app/controllers/microposts_controller.rb
```/app/controllers/microposts_controller.rb
class MicropostsController < ApplicationController
  .
  .
  .
  def vote
    value = params[:type] == "up" ? 1 : -1
    @micropost = Micropost.find(params[:id])
    @micropost.add_or_update_evaluation(:votes, value, current_user)
    redirect_to :back, notice: "Thank you for ええやん!"
  end
  
  private
  .
  .
  .
end
```

##投票用のリンクを貼り付ける

ここでようやく**いいね！**が押せるボタン（リンク）を**_micropost.html.erb**に導入します。  
ファイル場所   /app/views/microposts/_micropost.html.erb 
```/app/views/microposts/_micropost.html.erb 
<li>
  <span class="content">
  	<%= micropost.content %>

  	<%= pluralize micropost.reputation_for(:votes).to_i, "vote"%>   #追加
  	| <%= link_to "ええやん", vote_micropost_path(micropost, type: "up"), method: "post" %>   #追加
  	| <%= link_to " なんでやねん", vote_micropost_path(micropost, type: "down"), method: "post" %>    #追加
  </span>
  .
  .
  .
</li>
```

###以上で実装の手順は終わりです。
このやり方でちゃんと実装できるはずです。  
理論的なものが分かるようになれば簡単にほかのページにも応用できるはずです。

最終的にherokuにうpしたのが下のURLから行けます。  
###https://akis-app.herokuapp.com
<hr>
<hr>




