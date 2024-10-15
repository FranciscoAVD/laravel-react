# Laravel and Inertia
Project follows tutorial video from https://youtu.be/VrQRa-afCAk?si=omlQR_SMD_yt4zg9

## Scripts for project set up

1. `composer create-project laravel/laravel <PROJECT_NAME>`
2. `composer require laravel/breeze --dev`
3. `php artisan breeze:install`
4. `npm install`

## Local Development
Be sure to run both simultaneously
- `php artisan serve`
- `npm run dev`

## Database
### Script for creating schemas and factories
The files created live under ./database/factories and ./database/migrations
- `php artisan make:model <MODEL_NAME> -fm` FLAGS: f FACTORY, m MIGRATE
### Important steps
1. Define your schema for each table created under ./database/migrations
2. Pass the columns to the respective factory in ./database/factories to be able to generate fake data
3. Define your table relationships in ./app/models
4. Write population commands with the necessary models in ./database/seeders/DatabaseSeeder.php

### Script for migrations
- `php artisan migrate:refresh --seed` (refresh is to drop all existing tables)

#### To verify your migration was successfull, run:
- `php artisan tinker`
- `\App\Models\<MODEL_NAME>::count()` (Should equal to the amount created in your seeder file)

## Controllers
For creating controllers use:
 `php artisan make:controller <CONTROLLER_NAME> --model=<MODEL_NAME> --requests --resource`.
 ### Flags
 #### --requests
 The `--requests` flag will create two files for the purpose of validating whether a user is authorized to update or create an entity. These files live under ./app/Http/Requests
 #### --resource
 This will create all the crud methods inside the controller (index,create,store,show,edit,update,destroy)

## Auth
### Email verification

Change User model to include
```php 
class User extends Authenticatable implements MustVerifyEmail{
    ...
}
``` 
from 
```php
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Contracts\Auth\MustVerifyEmail
```
It should be commented out by default.