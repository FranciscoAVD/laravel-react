# Development steps
<!--Project follows tutorial video from https://youtu.be/VrQRa-afCAk?si=omlQR_SMD_yt4zg9-->

## Scripts for project set up

1. `composer create-project laravel/laravel <project_name>`
2. `composer require laravel/breeze --dev`
3. `php artisan breeze:install`
4. `npm install`

## Database
### Script for creating schemas and factories
<!--The files created live under database/factories and database/migrations-->
- `php artisan make:model <MODEL_NAME> -fm` <!--FLAGS: f FACTORY, m MIGRATE-->
### Important steps
1. Define your schema for each table created under ./database/migrations
2. Pass the columns to the respective factory in ./database/factories to be able to generate fake data
3. Define your table relationships in ./app/models
4. Write population commands with the necessary models in ./database/seeders/DatabaseSeeder.php

### Script for migrations
- php artisan migrate:refresh --seed <!--:refresh is to drop all existing tables-->
To verify your migration was successfull, run 
- `php artisan tinker`
- `\App\Models\<MODEL_NAME>::count()` <!--Should equal to the amount created in -->

## Controllers
For creating controllers use `php artisan make:controller <CONTROLLER_NAME> --model=<MODEL> --resource --request`

## Auth
### Email verification

Add
```php 
extends Authenticatable implements MustVerifyEmail
``` 
from 
```php
Illuminate\Contracts\Auth\MustVerifyEmail
```
to the User class. It should be commented out by default.