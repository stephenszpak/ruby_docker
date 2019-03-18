# Docker Ruby 2.6 app build for Ubuntu Server 18.04 LTS

In directory run `docker-compose run web rails new . --force --no-deps --database=postgresql`

It installs as root and makes files readonly so you need to run `sudo chown -R $USER:$USER .` 

Build Gemfile with `docker-compose build`

Connect to the postgres db by replaceing the contents of `config/database.yml` with

```
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password:
  pool: 5

development:
  <<: *default
  database: myapp_development


test:
  <<: *default
  database: myapp_test
```

Then boot up the app via `docker-compose up`

Open another terminal and type this to create a database : `docker-compose run web rake db:create`

Go to `localhost:3000` to see the app home page or use docker-machine (https://docs.docker.com/machine/overview/)

To stop the app type `docker-compose down`


When you want to make changes to `docker-compose.yml` run this command after making the changes `docker-compose up --build`

When you want to add to or update the Gemfile run `docker-compose run web bundle install` and then follow that up with `docker-compose up --build`

