> [!NOTE]
> Finalmente use XAMPP para el entorno, por lo tanto use php y mysql 

## Extensiones:
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

Si un controladoroclase solo tiene 1 metodo se le puede llamar __invoke() eso hara que cuando llamemos la clase accede a su único método.  

----

## Crear las vistas 
Se hace en Resources -> carpeta views 

Cuando queires ingresar auna vista desde el controlador se hace asi:

```bash
class HomeController extends Controller
{
    public function index(){
        return view('home');
    }
}

```
+ ruta.
* LA función view lo que esta declarando es que buscas un vista(En la carpeta) con el nombre home.

  En caso de que en un controler yo qusiera usar un parametro y pasarlo a la vista se haría de la siguiente forma en el controller:
  ```bash
   public function show($post)
    {
        return view('posts.show', [
            'post' => $post
        ]);
    }
  //Hay otra forma más de añadir la varibale con
      return view('posts.show', compact('post'));


```


En el hmtl se coloca
```bash
    <h1>Aqui se mostrará el post <?= $post?></h1>
```

Los ficheros de vsiaulización que son home.blade.php trbaja con platilla eso nos permite.

Poner el contendip de la varible asi 
```bash
<h1>Aqui se mostrará el post {{$post}}></h1>
```

También nos permite o siguiente:
```bash
    @if(true)<!--Muestra solo si existe una varible-->
    <p>Contenido de prueba</p>
    @endif
```

## Condicionales en el HTML
```bash
    @if ()
        
    @else
        
    @endif
----

    @switch($type)
        @case(1)
            
            @break
        @case(2)
            
            @break
        @default
            
    @endswitch
```

En caso de que queira escribir codigo php tmabien sepuede hacer asi 
```bash
    @php
        
    @endphp

```

## Bucles

```bash

    @foreach ($collection as $item)
        
    @endforeach
```
----
# Componentes Anónimos
## TailwindCSS
En el curso se presenta es  tailwindcss y como dentro de las etiquetas se puede crear componentes pra el HTML. 
Dentro de la carpeta views -> components y colocar alert.blade.php 
PAra que se viera debería ponerse en el html así
```bash
    <x-alert>
{{--         <x-slot name='title'>
            titulo de alerta
        </x-slot> --}}
        Contenido de la alerta
    </x-alert>
```

alert.blade.php
```bash
<div class="p-4 mb-4 text-sm text-blue-800 rounded-lg bg-blue-300">
    <!--<span class="font-medium">Info Alert!</span>{{$slot}} <!--Esto es para que pueda mandar un mensaje variable-->

    <span class="font-medium">{{$title ?? 'Info alert'}}</span>{{$slot}} <!-- Otro titulo, Esto es para que pueda mandar un mensaje variable--> 

</div>
```

Se puede poner atributos para poner diferentes alertas.


> [!NOTE]
> Se puede hacer con variables y cmabiar lo que espera recibir en los componentes.

alert.blade.php
```bash
@props(['type' => 'info'])<!--Es para recibir el valor y poner una cindcional múltiple, es recomendable poenr un valor po defecto-->

@php
    switch ($type) {
        case 'info':
            $class = 'text-blue-800 bg-blue-300';
            break;

        case 'danger':
            $class = 'text-red-800 bg-red-300';
            break;

        case 'success':
            $class = 'text-green-800 bg-green-300';
            break;

        case 'warning':
            $class = 'text-yellow-800 bg-yellow-300';
            break;

        default:
            $class = 'text-orange-800 bg-orange-300';
            break;
    }
@endphp

<div class="p-4 mb-4 text-sm rounded-lg {{ $class }}">
    <span class="font-medium">{{ $title ?? 'Info alert' }}</span>
    {{ $slot }}
</div>

```

Y en HTML se verya solo esto 
```bash
<x-alert type="warning">
```

## Componentes de clases (Dependientes)
Se puede crear con un comando... Elcomando crea 2 archivos. dentro de app -> view/Components/alert2.php y el componente de alert2.blade.php
```bash
php artisan make:component alert2
```

Sobre el html se veria asi 
´´´bash
        <x-alert2 type="info">
            <x-slot name='title'>
                titulo de alerta
            </x-slot> 
            Contenido de la alerta
        </x-alert2>
´´´
Y sobre el controles en Alert2.php
´´´bash
class Alert2 extends Component
{
    /**
     * Create a new component instance.
     */
    public $class; /*Definición dela variable*/

    public function __construct($type = 'info')
    {

        switch ($type) {
            case 'info':
                $class = 'text-blue-800 bg-blue-300';
                break;

            case 'danger':
                $class = 'text-red-800 bg-red-300';
                break;

            case 'success':
                $class = 'text-green-800 bg-green-300';
                break;

            case 'warning':
                $class = 'text-yellow-800 bg-yellow-300';
                break;

            default:
                $class = 'text-orange-800 bg-orange-300';
                break;

        }
        $this->class = $class;
    }
´´´

y en alert2.blade.php
```bash
<div class="p-4 mb-4 text-sm rounded-lg {{ $class }}">
    <span class="font-medium">{{ $title ?? 'Info alert' }}</span>
    {{ $slot }}
</div>

```
