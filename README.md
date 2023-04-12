# Doc Laravel GNU/Linux
Documentación para instalar y configurar proyectos usando Laravel.

## Instalación en Debian 11 desde cero.

### Apache2 - php>8
```bash
apt install apache2
apt install apt-transport-https gnupg2 ca-certificates
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
apt update
apt install libapache2-mod-php php php-common php-xml php-gd php8.0-opcache php-mbstring 
php-tokenizer php-json php-bcmath php-zip unzip curl
```

### Descargar Composer

```bash
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```

### Crear proyecto Laravel

```bash
cd /var/www/html
composer create-project --prefer-dist laravel/laravel myproject
chown -R ${USER}:www-data /var/www/html/myproject
chmod -R 775 /var/www/html/myproject
```

### Configuración Apache - Laravel

```bash
emacs /etc/apache2/sites-available/myproject.conf
```

```bash
<VirtualHost *:8000>
	ServerName localhost
	ServerAdmin admin@localhost
	DocumentRoot /var/www/html/myproject/public

	<Directory /var/www/html/myproject/public>
	Options Indexes MultiViews
	AllowOverride None
	Require all granted
	</Directory>

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

```bash
a2enmod rewrite
a2ensite myproject.conf
systemctl restart apache2
```

## PHP-laravel & Bases de datos

* MariaDB

```bash
apt install php-mysql
```

* Postgres

```bash
apt install php-pgsql
```

## Instalar bootstrap con npm en proyecto laravel

```bash
npm install bootstrap --save-dev
```

En el archivo "myproject/resources/sass/app.scss"

```bash
@import 'bootstrap/scss/bootstrap';
```

En el archivo "myproject/resources/js/app.js

```bash
import * as bootstrap from 'bootstrap';
```
## Instalar scss

```bash
npm install sass --save-dev
```
