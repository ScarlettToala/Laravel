> [!NOTE]
> Finalmente use XAMPP para el entorno, por lo tanto use php y mysql 

##Extensiones:
* Laravel Blade formatter
* Laravel Blade Snippets (Autocompletado)
* Laravel goto view (Ver codigo de referencia)
* Laravel Snippets (Agiliza para poner las rutas)
* PHP Intelephense (Ayuda a escribir codigo php)
* Spanish Lenguage Pack for Visual Studio Code(Codigo en español) 

> [!WARNING]
> Una vez se utiliza XAMPP accedemos a la carpeta public y se visualiza el archivo index.php 
> Para acceder se hace mediante el google que es mi navegador de preferencia y escribimos (http://localhost/Laravel/blog/public/index.php o blog.test)


Para concer las rutas existente esta en la carpeta routes


## Tipos de peticiones 
* GET
* POST
* PUT
* PATCH
* DELETE

Se pueden establecer rutas con variables: OJO Por parametro se le pasa la variable con el mismo nombre
```bash
Route::get('/posts/{post}', function($post){
    return "Aqui se mostrará el post " . $post;
});
```
Si dentro de la ruta tenemos varios / podemos hacer que algun valor sea opcional como el siguiente. OJO hay que dar valor por defecto:

```bash
Route::get('/posts/{post}/{category?}', function($post, $category = null){
    return "Aqui se mostrará el post " . $post . ". De categoria: " . $category;
});
```

> [!WARNING]
> El orden de las rutas si importan ya que va por orden de declración y si cumple la condición se queda en ese aunque el siguinete también cumpla(En caso de que las rutas tenga una declaración similar)

Para Crear un controler integrado a través d eun comando se puede crear, por la terminal del proyecto:
en este caso Homecontroller es el nombre del archivo 

```bash 
php artisan make:controller HomeController
```
Una vez realizado se mira en app/Http/Homecontroller.php.

PAra usar este controler se pondra en la web.php 

```bash
use App\Http\Controllers\HomeController;
```

Entonces para usarlo en la ruta se debe poner algo asi:
```bash 
Route::get('/', [HomeController::class, 'index']);
```
Poneos el nombre del metodo 