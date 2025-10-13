# Laravel
----
Laravel es un framework PHP de código abierto y gratuito para el desarrollo de aplicaciones y sitios web.

## Gestionar la base de datos (Postgres)
**Creamos un nuevo rol y una database especificamente para Laravel **
1- Un nuevo rol
```bash
CREATE ROLE laravel_user WITH LOGIN PASSWORD 'tu_contraseña_segura';
```

2- Una nueva base de datos
```bash
CREATE DATABASE laravel_db OWNER laravel_user;
```

3- Darle los privilegios al usuario en la base de datos
```bash
GRANT ALL PRIVILEGES ON DATABASE laravel_db TO laravel_user;
```

## Pasos a seguir para instalar Laravel  
> [!NOTE] **Documentación oficial de Laravel**
> Consulta la guía completa para crear un proyecto desde cero:
> [Link](https://laravel.com/docs/12.x#creating-a-laravel-project)

Después de descargar *PHP* + *Composer* + *Instalador de Laravel* + *Postgres* inicio un nuevo proyecto sobre el terminal:

> [!WARNING]
> Este comando se tiene que ejecutar en la carpeta donde lo quieres crear ;)

```bash
laravel new nombre-del-proyecto
```

Posteriomnete configurarlo en el proyecto:

```bash
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=laravel_db
DB_USERNAME=laravel_user
DB_PASSWORD=tu_contraseña_segura
```
---
Con el siguiente comando se puede crear el sevidor local y observar el primer proyecto.
```bash
php artisan serve
```

