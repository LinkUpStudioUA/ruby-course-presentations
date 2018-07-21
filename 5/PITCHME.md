## Ruby on Rails

---

#### Preparation

Check RoR version to make sure that RoR has been installed

```text
$ rails -v
```

+++

#### Preparation

Create new rails project

```text
$ rails new publications_app --database=postgresql
```

```text
$ cd publications_app
```

+++

#### Preparation

Generate a scaffold for the User resource <br>
We need it now for the lecture but please don't use scaffolding in future projects.

```text
$ rails generate scaffold User email:string
```

+++

#### Preparation

OK, we're ready to start. Just open the project in your IDE/Editor

---

#### Gemfile and Gemfile.lock

These files allow you to specify what gem dependencies are needed for your Rails application.

+++

#### Gemfile

```ruby
source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '2.5.1'

# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '~> 5.2.0'
# Use postgresql as the database for Active Record
gem 'pg', '>= 0.18', '< 2.0'

...

group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
  gem 'rspec-rails'
end

group :development do
  # Access an interactive console on exception pages or by calling 'console' anywhere in the code.
  gem 'web-console', '>= 3.3.0'
  gem 'listen', '>= 3.0.5', '< 3.2'
  # Spring speeds up development by keeping your application running in the background. Read more: https://github.com/rails/spring
  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'
end

...

gem 'active_campaign', github: 'mhenrixon/active_campaign', branch: 'master'
```
@[1](Gemfiles require at least one gem source, in the form of the URL for a RubyGems server)
@[2](This line allow us to get source of some gems from specific repositories, branches on the GitHub)
@[29](For example)
@[6-9](Every gem from default set has description)
@[13-25](If we need some gems not in all environments we can do like this)

---

#### Configuring a Database

Just about every Rails application will interact with a database. <br>
The database to use is specified in a configuration file, `config/database.yml`.

+++

#### Configuring a Database

```yml
default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default
  database: publications_app_development

test:
  <<: *default
  database: publications_app_test

production:
  <<: *default
  database: publications_app_production
  username: publications_app
  password: <%= ENV['PUBLICATIONS_APP_DATABASE_PASSWORD'] %>
```

+++

#### Rails Environments

There are three different environments in which Rails can run by default:

- The **development** environment is used on your development/local computer as you interact manually with the application.
- The **test** environment is used when running automated tests.
- The **production** environment is used when you deploy your application for the world to use.

---

#### MVC in Rails
 
Let's remember MVC

Models<br>
The model refers to the data objects that we use. 
It's the object oriented approach to design. 
The data in our database will be the most common type of object that we'll put there.

Views<br>
The view is the Presentation layer. 
It's what the user sees and interacts with, essentially the web pages. 
The HTML, the CSS and the JavaScript.

Controllers<br>
The controller will make decisions based on the request and then control what happens in response. 
It controls the interaction with our models and with our views.


+++

#### MVC in Rails