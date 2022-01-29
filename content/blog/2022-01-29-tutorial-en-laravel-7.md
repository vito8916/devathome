---
layout: blog
title: Tutorial en Laravel 7
date: 2022-01-29T03:52:02.590Z
---
# Tutorial Laravel Passport

En este tutorial veremos la forma de configurar Passport de Laravel para crear un API Restful utilizando Laravel framework 6.*

---

### Configuración inicial.

Ejecutar el siguiente comando para instalar Laravel

```bash
composer create-project --prefer-dist laravel/laravel passport-api "6.*"
```

El siguiente paso es instalar Passport, para ello ejecutamos el siguiente comando:

```bash
composer require laravel/passport
```

En el archivo ubicado en: *config/app.php* agregar el Service Provider de Passport en el array providers[ ], agregando la línea de código:

```php
Laravel\Passport\PassportServiceProvider::class,
```

El siguiente paso es configurar nuestra conecxión a la base de datos en las variables de entorno de Laravel que se encuentran en el archivo .ENV.

En mi caso esa es la configuración de mi entorno. Cambia estos valores según tu propia configuración.

```php
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=passport-api
DB_USERNAME=root
DB_PASSWORD=
```

Si estas utilizando una versión inferior a MySql 5.7 o MariaDb 10.2, colocar la siguiente línea de código en el método **boot de** app/providers/AppServiceProvider.php

```php
Schema::defaultStringLength(191);
```

Ejecutar las migraciones con el comando:

```php
php artisan migrate
```

Si el comando se ejecuta correctamente podrás ver en tu consola algo como esto:

```php
Migration table created successfully.
Migrating: 2014_10_12_000000_create_users_table
Migrated:  2014_10_12_000000_create_users_table (0.03 seconds)
Migrating: 2014_10_12_100000_create_password_resets_table
Migrated:  2014_10_12_100000_create_password_resets_table (0.03 seconds)
Migrating: 2016_06_01_000001_create_oauth_auth_codes_table
Migrated:  2016_06_01_000001_create_oauth_auth_codes_table (0.07 seconds)
Migrating: 2016_06_01_000002_create_oauth_access_tokens_table
Migrated:  2016_06_01_000002_create_oauth_access_tokens_table (0.07 seconds)
Migrating: 2016_06_01_000003_create_oauth_refresh_tokens_table
Migrated:  2016_06_01_000003_create_oauth_refresh_tokens_table (0.05 seconds)
Migrating: 2016_06_01_000004_create_oauth_clients_table
Migrated:  2016_06_01_000004_create_oauth_clients_table (0.03 seconds)
Migrating: 2016_06_01_000005_create_oauth_personal_access_clients_table
Migrated:  2016_06_01_000005_create_oauth_personal_access_clients_table (0.01 seconds)
Migrating: 2019_08_19_000000_create_failed_jobs_table
Migrated:  2019_08_19_000000_create_failed_jobs_table (0.03 seconds)
```

Para comprobar que todo haya salido bien, vamos a nuestra base de datos y verificamos que las siguiente tablas hayan sido creadas

![table_passport](/assets/images/tablas_passport.png "table_passport")

En el modelo User.php, agregar el uso de la clase HasApiTokens

```php
class User extends Authenticatable
{
    use HasApiTokens, Notifiable;
...
```

En app/providers/AuthServiceProvider.php, agregar el namespace siguiente:

```php
use Laravel\Passport\Passport;
```

Cambiar el dirver de autenticación de api en config/auth.php, por 'passport'

```php
'api' => [
            'driver' => 'passport', //por defecto es token
            'provider' => 'users',
            'hash' => false,
        ],
```

**For Laravel 6**

Now that Laravel 6 [is released](https://laravel-news.com/laravel-6) you need to install `laravel/ui`.

```
composer require laravel/ui "^1.2" --dev
php artisan ui vue --auth
```

You can change `vue` with `react` if you use React in your project (see [Using React](https://laravel.com/docs/6.x/frontend#using-react)).

And then you need to perform the migrations and compile the frontend

```
php artisan migrate
```

Si todo ha salido bien hasta este punto y refrescas tu servidor, podrás ver que en el Navbar de tu web aparecen 2 nuevos link: Login y Register. 

Ahora ejecutamos el comando necesario para instalar passport 

```php
php artisan passport:install
```

### Creación de Clientes.

Registrar las rutas de passport en app/providers/AuthServiceProvider.php en el metodo boot escribimos:

```php
Passport::routes();
```

Para comprobar la rutas podemos ejecutar el siguiente comando:

```php
php artisan route:list
```

*Podremos ver en nuestra consola todas las rutas de nuestro proyecto incluyendo las de aouth.*

...

...

...

Instalar Laravel Cors

composer require fruitcake/laravel-cors

Agregar el provider

php artisan vendor:publish --tag="cors"

```java
https://pagos.aliat.edu.mx/autoservicio/webservicenew/webservicecredencial.php?
```