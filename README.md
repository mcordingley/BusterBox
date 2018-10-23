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

Includes utf8mb4 with large prefix support, to fix the "max key length is 767
bytes" error. The MariaDb configuration changes necessary for this are
contained within the file /etc/mysql/conf.d/utf8mb4.cnf.

Your MySQL connection will need to have the ROW_FORMAT option set to DYNAMIC to
complete this. For users of Laravel, this would mean setting your engine parameter
in config/database.php to "InnoDB ROW_FORMAT=DYNAMIC".

This behavior will be the default in future versions of MariaDB, starting with
MySQL 5.7/MariaDb 10.2.


