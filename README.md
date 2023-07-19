# Laravel Task Scheduling
Laravel Task Scheduling adalah fitur yang disediakan oleh framework PHP Laravel untuk mengatur eksekusi tugas-tugas (tasks) secara otomatis pada interval tertentu.

## Usage
Membuat file command untuk menjalakan perintah yang akan di jalankan nanti ketika membuat sebuah penjadwalan

```sh
php artisan make:command AddUser
```

Maka file tersebut ada di direktory `app/Console/Commands/AddUser.php`
Didalam file `AddUser.php` membuat sebauah perintah yang akan di jalankan dalam waktu tertentu, contohnya disini menambahkan sebuah data user ke dalam database.

```php
public function handle(){
    $data = [
        'name' => 'Irfan Yasin',
        'email' => 'admin' . time() . '@gmail.com',
        'password' => 'pass' . time(),
        'created_at' => now()->format('Y-m-d H:i:s'),
        'updated_at' => now()->format('Y-m-d H:i:s'),
    ];

    DB::table('users')->insert($data);
    $this->info('success');
}
```


