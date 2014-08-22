---
layout: techpost
title: Migrating Diaspora from MariaDB (MySQL) to Postgresql
tags: diaspora mariadb mysql postgresql migration
---
I decided to bite the bullet and move my pod from MariaDB (an enhanced MySQL) to Postgresql. It wasn't too bad, and the performance seems to be much improved. I thought I'd write down what I did before I forget.

I started by installing Postgresql, and creating a user `diaspora` that had `CREATE DATABASE` privileges:

    create user diaspora;
    alter role diaspora with CREATEDB;

Then I altered `diaspora.yml` and `database.yml` in the `config` directory so that they would use Postgres instead of MySQL.

Then I ran the database setup for a new postgres installation to create all of the tables:

    RAILS_ENV=production  DB=postgres  bundle install --without test development
    RAILS_ENV=production  DB=postgres  bundle exec rake db:create db:schema:load
    DB=postgres bundle exec rake assets:precompile

Then I had to shut off my pod and move the data over. To do this, I used [py-mysql2pgsql](https://github.com/philipsoutham/py-mysql2pgsql), a migration tool. In order to manage foreign key constraints in the tables, I set up the following configuration file (usernames and passwords redacted):

    # a socket connection will be selected if a 'socket' is specified
    # also 'localhost' is a special 'hostname' for MySQL that overrides the 'port' option
    # and forces it to use a local socket connection
    # if tcp is chosen, you can use compression

    mysql:
     hostname: localhost
     port: 3306
     #socket: /tmp/mysql.sock
     username: diaspora
     password:
     database: diaspora_production
     compress: false
    destination:
     # if file is given, output goes to file, else postgres
     file:
     postgres:
      hostname: localhost
      port: 5432
      username: diaspora
      password:
      database: diaspora_production

    # if only_tables is given, only the listed tables will be converted.  leave empty to convert all tables.
    only_tables:
    - pods
    - people
    - users
    - posts
    - aspects
    - profiles
    - blocks
    - comments
    - contacts
    - conversations
    - invitations
    - likes
    - locations
    - mentions
    - messages
    - notifications
    - participations
    - photos
    - polls
    - reports
    - roles
    - services
    - taggings
    - tags
    - account_deletions
    - aspect_memberships
    - invitation_codes
    - aspect_visibilities
    - user_preferences
    - share_visibilities
    - simple_captcha_data
    - conversation_visibilities
    - tag_followings
    - notification_actors
    - schema_migrations
    - poll_answers
    - poll_participations
    - rails_admin_histories
    - o_embed_caches
    - open_graph_caches

    #- table2
    # if exclude_tables is given, exclude the listed tables from the conversion.
    #exclude_tables:
    #- table3
    #- table4

    # if supress_data is true, only the schema definition will be exported/migrated, and not the data
    supress_data: false

    # if supress_ddl is true, only the data will be exported/imported, and not the schema
    supress_ddl: true

    # if force_truncate is true, forces a table truncate before table loading
    force_truncate: true

    # if timezone is true, forces to append/convert to UTC tzinfo mysql data
    timezone: false

    # if index_prefix is given, indexes will be created whith a name prefixed with index_prefix
    index_prefix:

Once that completed (about ten minutes or so was all it took), I just started the pod with `DB=postgres ./script/server` and it ran fine!
