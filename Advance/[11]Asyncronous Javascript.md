### 11.Asyncronous Javascript

Sebelum kita mempelajari hal mengenai:

##### - Callback
##### - Promise
##### - Ajax
##### - Async & Await

Alangkah baiknya kita pula bertanya kembali ke diri kita sendiri apakah `Javascript` itu ???

Is a `single-threaded`,`non-blocking`,`asynchronous` and `concurrent` language
( http://latentflip.com/ )

Jadi javascript sendiri itu bahasa yang  `single-threaded`,`non-blocking`,`asynchronous` and `concurrent`

#### Thread

Urutan eksekusi kode yang dapat dilakukan secara bebas / independent satu sama lain,Dan pada javascript pula dia menggunakan thread `Single-Thread`

Jadi untuk javascript sendiri ketika mempunyai sebuah task/tugas dia akan menunggu nya sampai task tersebut selesai dan tidak akan melanjukannya ke task berikutnnya....

#### Blocking And Non-Blocking

Terdapat dua metode yang dapat di gunakan untuk melakukan operasi input/output(I/O) di dalam javascript sendiri,yaitu `Blocking (I/O)` dan `Non-Blocking (I/O)`.Dalam metode `Blocking (I/O)`,Proses eksekusi kode akan di lakukan sesuai urutan (synchronous),Sedangkan dalam metode `Non-Blocking` eksekusinya di lakukan tidak sesuai urutan (asynchronous).Untuk mengetahui perbedaan antara kedua metode tersebut.perhatikan terlebih dahulu kode yang di tulis menggunakan metode `Blocking (I/O)` berikut:

```javascript

	// Blocking
	console.log("kesatu")
	console.log("kedua")
	console.log("ketiga")

``` 

Pada metode `Blocking (I/O)` seperti di atas,perintah program akan di eksekusi sesuai dengan urutan.Artinya,perintah kedua akan di eksekusi setelah selesai di kerjakan.Demikian juga dengan perintah ketiga,yang akan di kerjakan setelah perintah kedua selesai.

Selanjutnya.perhatikan kode yang menggunakan metode `Non-Blocking (I/O)` berikut:

```javascript

	console.log("kesatu")
	setTimeout(function(){
		console.log("kedua")
	},2000)
	console.log("ketiga")

```

Kali ini,perintah program tidak dieksekusi berdasarkan urutan pada contoh di atas,kita menunda eksekusi perintah kedua selama 2 detik menggunakan fungsi `setTimeout()`.Sambil menunggu waktu tunda selesai,Javascript akan mencoba untuk menjalankan perintah-perintah lain yang dapat di eksekusi lebih dulu.Dengan demikian,fungsi `setTimeout()` merupakan fungsi yang akan di panggil menggunakan metode `Non-Blocking (I/O)`

Untuk membahas lebih jelas tentang `Syncronous` dan `Asyncronous`:
( http://latentflip.com/loupe/ )
`by.Phillip Roberts`