<div align="center">

# Laravel Auto Deploy

Deploy Laravel Application to Server via SSH by RSync

</div>

This project is fork from  [Charliex2/laravel-deploy-x](https://github.com/charliex2/laravel-deploy-x) with some change:

- [x] Fix rsync command;


## Default Artisan Commands
```
php artisan migrate 
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
            -   name: Install Packages
                run: composer install --no-dev
            -   name: Deploy to Server
                uses: hypertech-lda/laravel-auto-deploy@master
                with:
                    user: user
                    host: host
                    port: port
                    path: path
                    owner: owner
                    commands: "# Customer commands"
                env:
                    DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
```
