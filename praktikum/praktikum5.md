# Dynamic Route dan Middleware

Untuk praktikum ini, kita dapat menggunakan aplikasi dari modul sebelumnya. <br>

## Dynamic Route

Dynamic route adalah route yang dapat berubah-ubah, contohnya pada saat kita membuka suatu halaman web, kadang kita melihat `/users/1` atau `/users/2`, hal ini yang dinamakan dynamic routes.
Untuk menambahkan dynamic routes pada aplikasi lumen kita, kita dapat menggunakan syntax berikut,

  ```
  $router->get('/user/{id}', function ($id) {
      return 'User Id = ' . $id;
  });
  ```

  ![Hasil Screenshot](../prak5/img1.jpg)<br>
  ![Hasil Screenshot](../prak5/img2.jpg)<br>

Saat menambahkan parameter pada routes, kita tidak terbatas pada 1 variable saja, namun kita dapat menambahkan sebanyak yang diperlukan seperti kode berikut,

  ```
  $router->get('/post/{postId}/comments/{commentId}', function ($postId, $commentId) {
      return 'Post ID = ' . $postId . ' Comments ID = ' . $commentId;
  });
  ```

![Hasil Screenshot](../prak5/img3.jpg)<br>
![Hasil Screenshot](../prak5/img4.jpg)<br>

Pada dynamic routes kita juga bisa menambahkan optional routes, yang mana optional routes tidak mengharuskan kita untuk memberi variable pada endpoint kita, namun saat kita memanggil endpoint, dapat menggunakan parameter variable ataupun tidak, seperti pada kode dibawah ini,

  ```
  $router->get('/users[/{userId}]', function ($userId = null) {
      return $userId === null ? 'Data semua users' : 'Data user dengan id ' . $userId;
  });
  ```

![Hasil Screenshot](../prak5/img5.jpg)<br>
Ketika mengakses endpoint /users
![Hasil Screenshot](../prak5/img6.jpg)<br>
Ketika mengakses endpoint /users/1
![Hasil Screenshot](../prak5/img7.jpg)<br>

## Aliases Route

Aliases Route digunakan untuk memberi nama pada route yang telah kita buat, hal ini dapat membantu kita, saat kita ingin memanggil route tersebut pada aplikasi kita. Berikut syntax untuk menambahkan aliases route

  ```
  $router->get('/auth/login', ['as' => 'route.auth login', function (...) {...}])
  ...
  $router->get('/profile', function (Request $request) {
    if ($request->isLoggedIn) {
      return redirect()->route('route.auth.login');
    }
  });
  ```

![Hasil Screenshot](../prak5/img8.jpg) <br>
Jika kita masuk ke endpoint /profile, akan redirect ke endpoint /auth/login <br>
![Hasil Screenshot](../prak5/img9.jpg) <br>
![Hasil Screenshot](../prak5/img10.jpg)<br>

## Group Route

Pada lumen, kita juga dapat memberikan grouping pada routes kita agar lebih mudah pada saat penulisan route pada web.php. Kita dapat melakukan grouping dengan menggunakan syntax berikut,

  ```
  $router->group(['prefix' => 'users'], function () use ($router) {
    $router->get('/', function () { 
      // menjadi /users/, /users => prefix, / => path
      return "GET /users";
    });
  });
  ```

![Hasil Screenshot](../prak5/img11.jpg)<br>
![Hasil Screenshot](../prak5/img12.jpg)<br>

Selain dapat mengelompokkan prefix, kita juga dapat mengelompokkan middleware dan
namespace pada kelompok routes kita.

## Middleware

Middleware adalah penengah antara komunikasi aplikasi dan client. Middleware biasanya digunakan untuk membatasi siapa yang dapat berinteraksi dengan aplikasi kita dan semacamnya, kita dapat menambahkan middleware dengan menambahkan file pada folder `app/Http/Middleware`. Pada folder tersebut terdapat file `ExampleMiddleware`, kita dapat mencopy file tersebut untuk membuat middleware baru. Pada praktikum kali ini akan dibuat middleware Age dengan isi,

  ```
  class AgeMiddleware{
      /**
      * Handle an incoming request.
      *
      * @param \Illuminate\Http\Request $request
      * @param \Closure $next
      * @return mixed
      */
      public function handle($request, Closure $next){
          if ($request->age < 17)
              return redirect('/fail');
          return $next($request);
      }
  }
  ```

![Hasil Screenshot](../prak5/img13.jpg)<br>

Setelah menambahkan filter pada AgeMiddleware , kita harus mendaftarkan
AgeMiddleware pada aplikasi kita, pada file `bootstrap/app.php` seperti berikut ini,

```
  ...

  // $app->middleware([
  //      App\Http\Middleware\ExampleMiddleware::class
  // ]);
  
  // $app->routeMiddleware([
  //    'auth' => App\Http\Middleware\Authenticate::class,
  //    'age' => App\Http\Middleware\AgeMiddleware::class
  // ]);

  ...
  ```

Pada baris 65 terdapat comment mengenai proses mendaftarkan suatu middleware dalam aplikasi kita. Untuk menambahkan middleware pada aplikasi kita, kita dapat men-uncomment baris 75 hingga 77, kemudian menambahkan age middleware ke dalamnya.Namun, karena kita hanya ingin menambahkan middleware pada route tertentu, kita akan menghapus comment pada baris 79 hingga 81, kemudian menambahkan middleware age di
dalamnya.

![Hasil Screenshot](../prak5/img14.jpg) <br>

Kita dapat menambahkan middleware pada routes kita dengan menambahkan opsi middleware pada salah satu route, contohnya,

  ```
  $router->get('/admin/home/', ['middleware' => 'age', function () {
      return 'Dewasa';
  }]);

  $router->get('/fail', function () {
      return 'Dibawah umur';
  });
  ```

![Hasil Screenshot](../prak5/img15.jpg)<br>
Ketika 'age' kurang dari 17 tahun<br>
![Hasil Screenshot](../prak5/img16.jpg)<br>
Ketika 'age' 17 tahun ke atas<br>
![Hasil Screenshot](../prak5/img17.jpg)<br>