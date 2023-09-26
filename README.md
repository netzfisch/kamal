# README

## DEMO transcript

to install Rails 7.1-beta via Kamal to cloud provider:

    $ gem install -v 7.1.0.beta1 rails
    $ rails _7.1.0.beta1_ new kamal -d postgresql -c tailwind
    $ gem install kamal
    $ rails generate scaffold post title:string content:text
    $ rails db:create db:migrate
    $ ./bin/dev

Check

* http://127.0.0.1:3000/posts to use PostController and
* use http://127.0.0.1:3000/up (returns green + status code: 200-ok) for load
  balancer

Go for

    $ kamal init

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* Licence

### Links

* [Kamal deploy](https://kamal-deploy.org/) 4:09
