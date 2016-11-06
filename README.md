# Ruby rails app + db in docker

## Name your app
    RAILS_APP_NAME=myapp

## Create initial docker files 
    git clone git@github.com:joaocosta/docker-rails-pg.git $RAILS_APP_NAME
    cd $RAILS_APP_NAME
    rm -fR .git

## Initialize rails app
    docker-compose run web rails new . --force --database=postgresql --skip-bundle

## Configure database
    sed -i.bak s/myapp/$RAILS_APP_NAME/g .env.* database.yml
    mv database.yml config/database.yml

## Edit Gemfile and update any required gems
    vi Gemfile

## Install the bundle in a reusable docker image
    docker-compose build

## Create database schema
    docker-compose run web rake db:create

## Run application
    docker-compose up -d
