# Heroku WordPress
=========

This is a template for installing and running [WordPress](http://wordpress.org/) on [Heroku](http://www.heroku.com/) with a focus on minimal and fast configurations using the official Heroku and Wordpress stack.


# Deploy to Heroku
------------

Make sure you have the [Heroku Toolbelt](https://toolbelt.heroku.com/) installed and configured for your account. This provides the `heroku` CLI tool for creating and managing your Heroku apps.

- Create application in heroku. For instance : my_wp
- Execute:

```
heroku git:clone -a my_wp
```
- Clone the template from Github in other folder

```
git clone https://github.com/jrichardsz/heroku-wordpress-template.git .
```

- Paste the content from template to your heroku application cloned folder
- Push to heroku

```
git add .
git commit -am "make it better"
git push heroku master
```

- If no errors, add cleardb o any mysql public instance.
- In the settings section of your heroku app, add this environment variables:

  - DB_NAME
  - DB_USER
  - DB_PASSWORD
  - DB_HOST  -
  - AUTH_KEY
  - SECURE_AUTH_KEY
  - LOGGED_IN_KEY
  - NONCE_KEY
  - AUTH_SALT
  - SECURE_AUTH_SALT
  - LOGGED_IN_SALT
  - NONCE_SALT
  - DISABLE_WP_CRON = true

- Restart app
- Click in open app option
- Follow the wordpress wizard (backup your admin password)
- Thats all!

# About
-----

The repository is built on top of the standard Heroku PHP buildpack so you don't need to trust some sketchy 3rd party s3 bucket.
* [NGINX](http://nginx.org) - Fast scalable webserver.
* [PHP 7](http://php.net) - Latest and greatest with performance on par with HHVM.
* [Composer](https://getcomposer.org) - A dependency manager to make installing and managing plugins easier.

WordPress and most included plugins are installed by Composer on build. To add new plugins or upgrade versions of plugins simply update the `composer.json` file and then generate the `composer.lock` file with the following command locally:

```bash
$ composer install
$ composer update
```

Php 7.2 is required to run composer. You could use this docker container to do that:

[https://gist.github.com/jrichardsz/9fea9c990d79ecc1b895910a69d8682f#file-usage-md](https://gist.github.com/jrichardsz/9fea9c990d79ecc1b895910a69d8682f#file-usage-md)

Heroku WP uses the following addons:
* [ClearDB](https://w2.cleardb.net/about-cleardb/) - A fast and compatible MySQL replacement with even better performance. ClearDB are in environment section of your heroku app.


To add local plugins and themes, you can create ```plugins/``` and ```themes/``` folders inside `/public/wp-content` which upon deploy to Heroku will be copied on top of the standard WordPress install, themes, and plugins specified by Composer.

Usage
-----

Because a file cannot be written to Heroku's file system, updating and installing plugins or themes should be done locally and then pushed to Heroku. Even better would be to use Composer to install plugins so that version control and upgrading is simply a matter of editing the `composer.json` file and bumping the version number.
