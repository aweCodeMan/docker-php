# Docker PHP starter project

A starting Docker template for developing Laravel and Wordpress projects. The PHP container will have Composer installed as well as extensions for MySQL.

Put your source code inside `src`. 

Run everything with `docker-compose up -d`. Use `-d` for running the containers detached.

Your app will be available on [http://localhost:8080](http://localhost:8080).

To help you manage your database there's an adminer available on [http://localhost:8081](http://localhost:8081).

## Setting up your `wp_config.php` or `.env` files

Change the `host` value for your database inside your `wp_config.php` or `.env` file, as the database is in a different container (`localhost` will not work). Otherwise your app will not be able to connect to the database.

### For `wp_config.php` (Wordpress)

```
define('DB_NAME', 'database');
define('DB_USER', 'root');
define('DB_PASSWORD', 'secret');
define('DB_HOST', 'database');
```

### For `.env` (Laravel)

```
DB_HOST=database
DB_DATABASE=database
DB_USERNAME=root
DB_PASSWORD=secret
```

## Changing NGINX folder structure to Wordpress

The NGINX config file is set up to look for `index.php` inside `src/public` which will not work for a Wordpress project. You have to remove the `public` path from the config file and rebuild the container.

1. Open `docker/nginx/default.conf`.
2. Change line `root /var/www/html/public` to `root /var/www/html`.
3. Rebuild the container