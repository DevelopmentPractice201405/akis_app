source 'https://rubygems.org'
ruby '2.0.0'
# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '4.0.5'
gem 'bootstrap-sass', '2.3.2.0'
gem 'sprockets', '2.11.0'
# Use sqlite3 as the database for Active Record
group :development, :test do
gem 'sqlite3','1.3.8'
gem 'rspec-rails', '2.13.1'
end

group :test do
  gem 'selenium-webdriver', '2.35.1'
  gem 'capybara', '2.1.0'
end


# Use SCSS for stylesheets
gem 'sass-rails', '~> 4.0.2'
gem 'uglifier', '2.1.1'
gem 'coffee-rails', '4.0.1'
gem 'jquery-rails', '3.0.4'
gem 'turbolinks', '1.1.1'
gem 'jbuilder', '1.0.2'

# Use Uglifier as compressor for JavaScript assets


# Use CoffeeScript for .js.coffee assets and views


# See https://github.com/sstephenson/execjs#readme for more supported runtimes
gem 'therubyracer', platforms: :ruby

# Use jquery as the JavaScript library

# Turbolinks makes following links in your web application faster. Read more: https://github.com/rails/turbolinks

# Build JSON APIs with ease. Read more: https://github.com/rails/jbuilder

group :doc do
  # bundle exec rake doc:rails generates the API under doc/api.
  gem 'sdoc','0.3.20', require: false
end

# Use ActiveModel has_secure_password
# gem 'bcrypt', '~> 3.1.7'

# Use unicorn as the app server
# gem 'unicorn'

# Use Capistrano for deployment
# gem 'capistrano', group: :development

# Use debugger
# gem 'debugger', group: [:development, :test]
group :production do
  gem 'pg', '0.15.1'
  gem 'rails_12factor', '0.0.2'
end
