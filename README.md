# Ruby rails app + db in docker

## Name your app
    RAILS_APP_NAME=myapp

## Create initial docker files 
    git clone git@github.com:joaocosta/docker-rails-pg.git $RAILS_APP_NAME
    cd $RAILS_APP_NAME
    rm -fR .git
    sed -i s/myapp/$RAILS_APP_NAME/g database.yml docker-compose.yml Dockerfile .env.*

## Initialize rails app
    docker-compose run web rails new . --force --database=postgresql --skip-bundle

## Configure database
    mv database.yml config/database.yml

## Edit Gemfile and update any required gems
    vi Gemfile

## Install the bundle in a reusable docker image
    docker-compose build

## Create database schema
    docker-compose run web rake db:create

## Run application
    docker-compose up -d

## Initialize new repo
    git init .
