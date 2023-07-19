# Laravel Task Scheduling
Laravel Task Scheduling adalah fitur yang disediakan oleh framework PHP Laravel untuk mengatur eksekusi tugas-tugas (tasks) secara otomatis pada interval tertentu.

## Usage
Membuat file command untuk menjalakan perintah yang akan di jalankan nanti ketika membuat sebuah penjadwalan

```sh
php artisan make:command AddUser
```

Maka file tersebut ada di direktory `app/Console/Commands/AddUser.php`. 
Didalam file `AddUser.php` membuat sebuah perintah yang akan di jalankan dalam waktu tertentu, contohnya disini menambahkan sebuah data user ke dalam database.

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

Lalu buka file `Kernel.php` dan buat pengaturan waktu kapan perintah itu akan di jalankan.

```php
protected function schedule(Schedule $schedule): void
{
    $schedule->command('add:user')->everyMinute();
}
```

`command('add:user')` harus di samakan dengan perintah yang ada di file `AddUser.php` di dalam method `protected $signature = 'add:user';`.

</br>

Jalankan schedule yang telah dibuat dengan menulis perintah ini di terminal.
```sh
php artisan schedule:work
```




