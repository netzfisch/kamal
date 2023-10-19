# README

## Setup

DEMO transcript to install Rails 7.1 via Kamal gem to virtual machine on cloud
provider:

    % gem install kamal
    % gem install -v 7.1.1 rails
    % rails _7.1.1_ new test-kamal -d postgresql -c tailwind
    % rails generate scaffold post title:string content:text
    % rails db:prepare # do db:create + migrate at once
    % ./bin/dev

Check that `http://127.0.0.1:3000/up` return **green screen** as status code `200`
for OK.

### Configuration

**Initialize** Kamal with `% kamal init` which creates `config/deploy.yml`, `.env`
and some sample hook example files. Ensure

* that .env-secrets are correct,
* having the same ruby-version in Dockfile, Gemfile and
* using the **same DB_HOST, POSTGRES_PASSWORD** variables in database.yml and deploy.yml.
* Enter the different server IPs in the deploy.yml for traffic management

Depending on **ssl-certificate** existing may comment-out `config.force_ssl = true`
production.rb enviroment.

Further more ensure your ssh-settings allow you root-access to target server.
Copy the given public key to the remote, do
`ssh-copy-id -i ~/.ssh/id_rsa.pub root@213.128.xxx.xxx ` which adds the key by
appending to ~/.ssh/authorized_keys file of remote server user.

If you want to **build remotely** the docker images (preferable), choose a **VM with
at least 2 GB RAM**. Further add to deploy.yml this block:

```yaml
builder:
  remote:
    arch: amd64
    host: ssh://root@213.128.xxx.xxx
```

Alternatively **align native building architecture** on the local machine with
remote runtime enviroment, e.g. `% bundle lock --add-platform aarch64-linux`.

Finalise setup of remote machine with `% kamal setup` which will install Docker
host, push .env-file and do `% kamal deploy` in one step.

### Build + Deployment

If things do not work as expected, try this:

```sh
% kamal build details      # check if on native vs remote build
% kamal build remove       # if needed remove actual setup
% kamal lock release       # remove lock-file to restart
% kamal env push           # push enviroment variables if changed
% kamal deploy             # deploy or (re)deploy
% kamal deploy -d staging  # deploy to staging -> deploy.staging.yml enviroment
```

If you need to delete the database container, go directly to the machine
`% ssh root@213.128.xxx.xxx` and manage docker conatiner

```
% docker ps
% docker stop app-db && docker rm app-db
```

But be aware that your **data will be lost**.

## Links

* [Kamal deploy](https://kamal-deploy.org/)
* [TLS support through Let's Encrypt using Traefik](https://github.com/basecamp/kamal/discussions/112)
* [Multiple apps on a single server](https://www.erikminkel.com/2023/09/29/using-kamal-to-host-multiple-apps-on-a-single-server/)

## Contributing

If you find a problem, please create a [GitHub Issue](https://github.com/netzfisch/test_kamal/issues).

Have a fix, want to add or request a feature? [Pull Requests](https://github.com/netzfisch/test_kamal/pulls) are welcome!

### TODOs

- [done] integrate LetsEncrypt!

### License

The MIT License (MIT), see [LICENSE](https://github.com/netzfisch/test_kamal/blob/master/LICENSE) file.
