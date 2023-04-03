# PHP Docker for application development

Docker images that can be used for applicaiton development/ci-cd and for production. These images are based on official [PHP images](https://hub.docker.com/_/php)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/D1D5DMOTA)

## SDK

Images for use in CI/CD and for application development

- Based on [php-cli](http://www.php-cli.com/)

This image contains:

- [NodeJS](https://nodejs.org/en) and [NPM](https://www.npmjs.com/)
- [Yarn](https://yarnpkg.com/)
- [Codesniffer](https://github.com/squizlabs/PHP_CodeSniffer)
  - phpcs
  - phpcbf
  - [php-cs-fixer](https://github.com/PHP-CS-Fixer)
- [PSALM](https://psalm.dev/)
- [PHPUnit](https://phpunit.de/)
- [Xdebug](https://xdebug.org/)
- [Redis](https://redis.io/)
- PHP Extensions: [intl](https://www.php.net/manual/en/book.intl.php) [pdo_pgsql](https://www.php.net/manual/en/ref.pdo-pgsql.php) [gd](https://www.php.net/manual/en/book.image.php) [zip](https://www.php.net/manual/en/book.zip.php) [pdo_mysql](https://www.php.net/manual/en/ref.pdo-mysql.php)
- [phar-composer](https://github.com/clue/phar-composer)
  - Image has set phar.readonly to 0 (zero) to allows you to create phar files 

## Runtime

This image can be used for application in production environment

- based on [php-fpm](https://www.php.net/manual/en/install.fpm.php)

This image contains:

- [Redis](https://redis.io/)
- PHP extensions: [intl](https://www.php.net/manual/en/book.intl.php) [pdo_pgsql](https://www.php.net/manual/en/ref.pdo-pgsql.php) [gd](https://www.php.net/manual/en/book.image.php) [zip](https://www.php.net/manual/en/book.zip.php) [pdo_mysql](https://www.php.net/manual/en/ref.pdo-mysql.php)

## Versions

Use `sdk:latest` for latest build or use wanted version e.g. `sdk:8.1.6`.

## Usage

For docker you can use `docker pull ghcr.io/maymeow/php/{imagename}:latest` where image name is `sdk` or `runtime`.

In docker compose use:

```yml
image: ghcr.io/maymeow/php/runtime:latest
# Or for SDK
image: ghcr.io/maymeow/php/sdk:latest
```
### Creating image for production environment

Runtime image does not contains composer so you need to install all composer dependencies first.

You can create image with multistep build like this

```Dockerfile
FROM ghcr.io/maymeow/php/sdk:latest AS build-env

WORKDIR /app
COPY . /app
RUN composer install --no-ansi --no-dev --no-interaction --no-plugins --no-progress --optimize-autoloader #--no-scripts

FROM ghcr.io/maymeow/php/runtime:latest

ARG user=www-data
COPY --from=build-env /app /var/www
RUN chown -R $user:$user /var/www
WORKDIR /var/www
RUN chmod -R 777 /var/www/logs
USER $user
```

License: MIT
