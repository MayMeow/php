# PHP Docker for application development

Docker images that can be used for applicaiton development/ci-cd and for production. These images are based on official [PHP images](https://hub.docker.com/_/php)

## SDK

Images for use in CI/CD and for application development

- Based on php-cli

This image contains:

- NodeJS and NPM
- Yarn
- Codesniffer
  - phpcs
  - phpcbf
  - php-cs-fixer
- PSALM
- PHPUnit
- Xdebug
- Redis
- PHP Extensions: intl pdo_pgsql gd zip pdo_mysql
- phar-composer
  - Image has set phar.readonly to 0 (zero) to allows you to create phar files 

## Runtime

This image can be used for application in production environment

- based on php-fpm

This image contains:

- Redis
- PHP extensions: intl pdo_pgsql gd zip pdo_mysql

Runtime image does not contains composer so you need to install all composer dependencies first.
