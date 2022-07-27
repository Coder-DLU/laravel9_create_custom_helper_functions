# laravel9_create_custom_helper_functions
## 1. Install Laravel 9

```Dockerfile
composer create-project laravel/laravel laravel9_create_custom_helper_functions
```
## 2. Create helpers.php File
- Vào app/Helpers/helpers.php
```Dockerfile
<?php
  
use Carbon\Carbon;
  
/**
 * Write code on Method
 *
 * @return response()
 */
if (! function_exists('convertYmdToMdy')) {
    function convertYmdToMdy($date)
    {
        return Carbon::createFromFormat('Y-m-d', $date)->format('m-d-Y');
    }
}
  
/**
 * Write code on Method
 *
 * @return response()
 */
if (! function_exists('convertMdyToYmd')) {
    function convertMdyToYmd($date)
    {
        return Carbon::createFromFormat('m-d-Y', $date)->format('Y-m-d');
    }
}
```
## 3.Register File Path In composer.json File
- Vào composer.json
```Dockerfile
"autoload": {
    "psr-4": {
        "App\\": "app/",
        "Database\\Factories\\": "database/factories/",
        "Database\\Seeders\\": "database/seeders/"
    },
    "files": [
        "app/Helpers/helpers.php"
    ]
},
```
- Chạy 
```Dockerfile
composer dump-autoload
```
## 4. Add Route
- Vào routes/web.php
```Dockerfile
<?php
  
use Illuminate\Support\Facades\Route;
  
/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
|
| Here is where you can register web routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| contains the "web" middleware group. Now create something great!
|
*/
  
Route::get('call-helper', function(){
  
    $mdY = convertYmdToMdy('2022-02-12');
    var_dump("Converted into 'MDY': " . $mdY);
    
    $ymd = convertMdyToYmd('02-12-2022');
    var_dump("Converted into 'YMD': " . $ymd);
});
```
## 5.Run Laravel App:
```Dockerfile
php artisan serve
```
```Dockerfile
http://localhost:8000/call-helper
```
- Output:
```Dockerfile
string(32) "Converted into 'MDY': 02-12-2022" 
string(32) "Converted into 'YMD': 2022-02-12"
```
- Use In Blade File:
```Dockerfile
<p>Date: {{ convertYmdToMdy('2022-02-12') }}</p>
<p>Date: {{ convertMdyToYmd('02-12-2022') }}</p>
```
