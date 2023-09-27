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

Start '% kamal init' and configure '% vim config/deploy.yml'. Ensure that

* that '% cat.env' secrets are correct,
* having the same ruby-version in Gemfile, docker-compose.yml, etc. and
* database password is known.

Further more ensure your ssh-settings allow you root-access to target server.

Than align building architecrute (laptop) with runtime enviroment, maybe do
'% bundle lock --add-platform aarch64-linux' and start building locally Docker
container and pushing the remote server with '% kamal setup'.

If things do not work as expected, go directly to the machine
'% ssh root@213.128.146.47' and manage docker conatiner
'% docker ps / stop ed2a0cd4e864 / rm ed2a0cd4e864'.

---
FIX:

ActiveRecord::ConnectionNotEstablished: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: No such file or dire
	Is the server running locally and accepting connections on that socket?


Caused by:
PG::ConnectionBad: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: No such file or directory
	Is the server running locally and accepting connections on that socket?

Tasks: TOP => db:prepare

---

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
