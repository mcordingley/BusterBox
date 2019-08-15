# BusterBox

BusterBox is a minimal Vagrant box for PHP development built using Debian
Buster. The goal is to be usable without modification for the major PHP
frameworks, but to otherwise stay as close as possible to upstream.

## Apache

Apache has the default virtual host set up to point to /var/www/html/public and
has mod_rewrite and mod_ssl enabled.

## PHP

PHP 7.2 comes installed with the curl, mbstring, mysql, xml extensions installed,
along with Composer installed via apt.

## Database Configuration

Database: vagrant
User: vagrant
Password: vagrant

## NPM and NodeJS

Node 10.15 and NPM 5.8 are installed to handle your asset build needs.
