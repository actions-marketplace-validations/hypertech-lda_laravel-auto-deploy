<div align="center">

# Laravel Deploy Action

[![ForTheBadge built-with-love](http://ForTheBadge.com/images/badges/built-with-love.svg)](https://kosrat.dev)

</div>

## Default Artisan Commands
```
php artisan migrate 
php artisan modelcach:clear 
php artisan cache:clear 
php artisan route:cache
php artisan config:cache
```
All commands above are executed in the default order.

## Custom Artisan Commands
 Custom commands can be executed after default artisan command. Custom commands could be added in the `.github/workflows/deploy.yml` file.


## Config example:

.github/workflows/deploy.yml

```
name: Build and Deploy
on:
    push:
        branches:
            -   master

jobs:
    build:
        name: Build and Deploy
        runs-on: ubuntu-latest
        steps:
            -   name: Checkout Repository
                uses: actions/checkout@master
            -   name: Setup Enviroment
                uses: shivammathur/setup-php@v2
                with:
                    php-version: '7.4'
            -   name: Speed up the packages installation process
                run: composer global require hirak/prestissimo
            -   name: Install Packages
                run: composer install --no-dev
            -   name: Deploy to Server
                uses: charliex2/laravel-action@master
                with:
                    user: user
                    host: host
                    port: port
                    path: path
                    owner: owner
                    commands:     # Custom commands
                env:
                    DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
```
