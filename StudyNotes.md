# Grape Gem Tutorial: Building A REST-Like API in Ruby 

This project will be my introduction to using `Ruby` and `Grape` - REST-like API micro-framework for Ruby. The project is inspired by
a project on `toptal` for building a backend support in Rails for a JSON API. Grape is designed to run as a mountable rack engine to 
complement web applications without interfering with them. 


## User Story 

The user story that is focused on for this project is an application capable of capturing and reviewing pair programming sessions. The 
User Interface for the application can be written for any platform but will need to communicate with a backend service for storing and 
retrieving data. The focus for this tutorial is to create a secure and robust backend service that suppports JSON API. 


The API will provide methods for 
- user authentication 
- queries for pair programming session reviews 


### Project Requirements 

Major features include: 
- Every API call must return a valid JSON 
- Every failed API call must be recorded with adequate context and information to subsequently be reproducible and debugged if 
  necessary 
- In terms of security, each request should be restricted to a small subset of developers we track 
- all requests other than logging in and signing up with need to be authenticated


### Test Driven Development and RSpec 

A popular software approach right now is a test driven approach to help ensure the behavior of the API. For testing purposes we will be 
using `RSpec` - a well known testing framework for RubyOnRails. We will use this for our development and should include both positive and 
negative tests. 


## Getting Started 

Let's start the foundation for our REST API by creating a new Rails application. Rails is a web application development framework written 
in the Ruby programming language. It is designed to make programming web applications easier by making assumptions about what every 
developer needs to get started. The Rails philosophy includes two major principles: 

- Don't repeat yourself 
- Convention over configuration 


First we need to install Rails, to do so we need two prerequisites: `Ruby` and `SQLite3`. Verify by running 

```
ruby -v 
sqlite3 --version 
```

To install Rails, use the `gem install` command provided by RubyGems: 

```
gem install rails
```

To verify that everything is up and working we should be able to run the following: 

```
rails --version
```

Now we are ready to start creating the application. Rails comes with a number of scripts called generators that are designed to make 
the development process easier by creating everything that is necessary to start working on a particular task. To create the new rails 
application run: 

```
rails new grape_blog
```

Next we will install RSpec by adding `rspec-rails` into our gemfile: 

```
group :development, :test do 
    gem 'rspec-rails', '~> 3.2' 
end 
```

Then from the command line we run the command: 

```
rails generate rspec:install
```

We will also be using some existing open source software for our testing framework. Specifically: 

- Devise - a flexible authentication solution for Rails based on Warden 
- factory_girl_rails - provides Rails integration for factory_girl, a library for setting up Ruby objects as test data 


First, in order to incorporate these dependencies we add the following into the gemfile: 
```
gem 'devise' 

group :development, :test do 
    gem 'factory_girl_rails', '~> 4.5' 
end 
```


Next, we generate a user model, initialize the `devise` gem, and add it to the user model (this enables the user class to be used for 
authentication)

```
rails g model user 
rails generate devise:install
rails generate devise user
```

## Understanding Rails Models, Views and Controllers 

* The `browser` is the device that makes the request to an endpoint such as https://example.com/video/show/15
* The `web server` (mongrel, WEBrick) receives the request and routes it to find out which controller to use - in this case it will be
  the "video" controller, method "show", with the id parameter set to "15". The web server then uses the dispatcher to create a new 
  controller, call the action and pass the parameters 
* `Controllers` do the work of parsing user requests, data submissions, cookies, sessions and the "browser stuff". They are the managers 
  thatt orders employees around. Ideally they give orders without knowing or caring how it gets done. In this case the show method in our 
  video controller knows that it needs to look up a view and asks the `model` to get video 15 and eventually displays it to the user 
* `Models` are Ruby classes. They talk to the database, store, and validate data, perform the business logic and otherwise do the heavy 
  lifting. They are the guy in the back room crunching the numbers - in this case the model is the one that retrieves video 15 from the 
  database 
* `Views` are what the user sees: HTML, CSS, XML, JavaScript, JSON. They are merely puppets that reads what the controller gives them. In
  our example the controller gives video 15 to the "show" view. The show view generates the HTML: divs, tables, text, descriptions, footers
* `Controllers` are the ones that return the response body and metadata to the server. The server combines the raw data into a proper HTTP
  response and sends it to the user. 


Next we include the `factory_girl` syntax method in our `rails_helper.rb` file in order to use the abbreviated version of user creation in 
our RSpec: 

```
RSpec.configure do |config|
    config.include FactoryGirl::Syntax::Methods
```

Finally we add the grape gem to our DSL (Domain Specific Language) and install it: 
```
gem 'grape'
bundle
```



## User Login Use Case And Spec 

Our backend will need to support a basic login capability. We will create a skeleton for our `login_spec` assuming that a valid login 
request consists of a registered email address and password pair: 

```ruby
require 'rails_helper' do 
  context 'negative tests' do 
    context 'missing params' do 
      context 'password' do 
      end 
      context 'email' do 
      end 
    end 
    context 'invalid params' do 
      context 'incorrect password' do 
      end 
      context 'with a non-existent login' do 
      end 
    end 
  end 
  context 'positive tests' do 
    context 'valid params' do 
    end 
  end 
end 
```

If either of the parameters is missing we want the client to receive an HTTP return status code of 400 (Bad Request) along with 
an error message of 'email is missing' or 'password is missing'. 


We are going to create the user and the parameter hash at the beginning of the spec. We will put this code after the describe
block: 

```ruby
describe '/api/login' do 
  let(:email) {user.email}
  let(:password) {user.password}
  let!(:user) {create :user}
  let(:original_params) {{email: email, password: password}}
  let(:params) {original_params}
```

  
  
  




