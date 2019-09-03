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


