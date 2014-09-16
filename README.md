グループ構成　イマズ　クバ　リョウジ　ヨシノ
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




