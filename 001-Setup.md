Setup
=====

1. Créez une nouvelle application Rails :

		$ rails new deux_scoops --database postgresql --skip-test

2. Remplacez le contenu de `bin/setup` avec :

		#!/bin/sh

		set -e

		gem install bundler --conservative
		bundle check || bundle install

		bundle exec rails db:setup

3. Initialisez la base de données avec : `./bin/setup`
