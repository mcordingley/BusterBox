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

## Provisioning Tips

If you want to open the database to external connections so you can see and edit your database from your IDE or other
such tool, all you need to do is add the following lines to your provision script. The database user is already
configured to work with external logins. 

```
sudo sed -i 's/127.0.0.1/0.0.0.0/g' /etc/mysql/mariadb.conf.d/50-server.cnf
sudo service mysql restart >/dev/null 2>&1
```

For XDebug support, the following snippet will install XDebug and then configure it to connect back to your host system:

```
sudo apt install -y php-xdebug >/dev/null 2>&1

DEFAULT_GATEWAY=$(ip route show default | awk '/default/ {print $3}')

for CONFIG in "cli" "apache2"
do
    echo "xdebug.remote_enable=1" | sudo tee -a /etc/php/7.3/$CONFIG/php.ini >/dev/null 2>&1
    echo "xdebug.remote_host=$DEFAULT_GATEWAY" | sudo tee -a /etc/php/7.3/$CONFIG/php.ini >/dev/null 2>&1
    echo "xdebug.remote_autostart=1" | sudo tee -a /etc/php/7.3/$CONFIG/php.ini >/dev/null 2>&1
done
```

The following will set up ZSH, switch themes to the "gentoo" theme, and disable automatic updates.

```
sudo apt install -y zsh >/dev/null 2>&1
wget --no-check-certificate https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - 2>/dev/null | sh >/dev/null 2>&1
sudo chsh -s /bin/zsh vagrant >/dev/null 2>&1
sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="gentoo"/g' /home/vagrant/.zshrc
sed -i 's/# DISABLE_AUTO_UPDATE="true"/DISABLE_AUTO_UPDATE="true"/g' /home/vagrant/.zshrc
```