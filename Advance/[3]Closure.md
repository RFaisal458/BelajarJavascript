### 3.Closure

Sebelum kita mempelajari apa itu closure,dan bagaimana cara penggunaannya,alangkah baiknya kita harus mengetahui 3 konsep ini dalam javascript:

#### Execution Context,Hoisting,Scope

di dalam Execution Context awalnya berada pada Global Context dan Execution Context pula sendiri terbagi menjadi 2 fase yaitu

- `CREATION`

- `EXECUTION`

```javascript

console.log(nama)
var nama='Rafif Faisal Ghozi'

// Creation Phase pada Global Context
// var nama=undefined
// function=fn()
// hoisting
// window=global object
// this=window

```

Jika kita jalan kode di atas akan menghasilkan undifined,dan kenapa tidak error ??Nah..disini terjadi proses yang di namakan hoisting,jadi untuk kode seperti di atas pula di sebut dengan `Creation Phase`,jadi javascript sendiri akan men-check dari atas sampai ke bawah apakah ada sebuah deklarasi variable atau function,dan jika ada untuk variable sendiri javascript akan mengisinya dengan undifined sendangkan untuk function dia akan di isi dengan isi function itu sendiri tetapi berisi string `fn()`.tapi sebetulnya selain mencari deklarasi variable dan function javascript juga mendefinisikan object `window=global object` dan `this=window`.

Setelah `Creation Phase` kita akan mempelajari pula apa itu `Execution Phase` untuk sekarang kita akan mencoba apa yang di namakan dengan `Execution Phase`

```javascript

console.log(sayHello())

var nama='Rafif'
var umur=17

function sayHello(){
	return `Halo,Nama saya ${nama},dan saya berumur ${umur}`
}

// Function membuat Local Execution Context
// yang di dalamnya terdapat creation phase dan execution phase
//window
//arguments
//hoisting

```

Jika kode program di atas di jalankan,kita akan mendapatkan output kurang lebih seperti ini `Halo,Nama saya undefined,dan saya berumur undefined`,jadi undefined sendiri di akibatkan karena hoisting,jadi untuk membaca kode program di atas pula

- pertama variable nama dan umur terkena hoisting dan akibatnya berisi `undefined`,sedangkan function juga di isi dengan object
- kedua kita langsung masuk ke local context function dari si `sayHello`,setelah itu javascript memeriksa terlebih dahulu apakah ada yang di hoisting,ternyata tidak fungsi hanya mengembalikan nilai
- ketiga program menampilkan nilai yang di kembalikan oleh fungsi tadi
- keempat sendiri kita baru mendefinisikan `nama` dengan isi `Rafif` dan `umur` dengan isi `17`

Untuk melihat tentang alur dari `EXECUTION CONTEXT` sendiri ada sebuah website yang menyediakan penelurusan alur ini,nama websitenya sendiri adalah:http://www.pythontutor.com/javascript.html

Agar bisa lebih memahami lagi saya akan menyertakan contoh lagi di bawah ini:

```javascript

var username="@RFaisal458"

function cetakUrl(username){
	var instagramUrl="https://instagram.com/"
	return instagramUrl + username
}

console.log(cetakUrl(username))

```

Mungkin kita bisa menebak apa dari output kode di atas,jadi untuk alurnya sendiri 

- pertama javascript akan akan memeriksa global context  terlebih dahulu apakah ada variable/function untuk di hoisting,ternyata ada yaitu variable username dan function cetakUrl,tapi username sendiri akan tertimpah dengan `@RFaisal458`,dan untuk function sendiri di isi dengan object function itu sendiri
- kedua karena kita melakukan `console.log(cetakUrl(username))` dan sekaligus mengoper parameter dengan isi variable `username` dari yang di atas
- ketiga setelah melakukan pemanggilan dengan `console.log(cetakUrl(username))` kita masuk ke local context dari si function `CetakUrl`,setelah di dalamnya javascript pula akan memeriksa apakah ada variable/function yang di hoisting,ternyata ada satu variable yaitu `var instagramUrl="https://instagram.com/` kemudian setelah itu function ini mengembalikan nilai

Setelah kita mengetahui tentang `Execution Context`,`Hoisting` kemudian kita akan mempelajari pula `Scope`,pertanyaanya untuk kode di atas adalah bagaimana jika kita menghapus bagian isi parameter dari function `cetakUrl` jadi seperti ini `function cetakUrl(){` begitu pula dengan `console.log(cetakUrl())`,yang jadi pertanyaannya `return instagramUrl + username` jadi si variable `username` ini dari mana ???,Nah sifat dari function di javascript sendiri ketika di dalam Scope atau Wadah function itu sendiri tidak ada variable yang ada di dalamnya function tersebut akan mencari variable tersebut ke luar scope/lingkupnya.

Setiap konteks fungsi akan membuat private scope,  yang berisi deklarasi-deklarasi di dalam fungsi tersebut dan ini akan bersifat lokal, dan tidak bisa diakses dari luar scope fungsi tersebut. Fungsi bisa mengakses variabel yang berada diluar konteks fungsi tersebut, tetapi yang diluar tidak bisa mengakses yang didalam.

Nah setelah kita mengetahui `Scope` sekarang kita akan mempelajari pula `Arguments`,coba perhatikan kode di bawah ini:

```javascript

var username="@RFaisal458"

function cetakUrl(){
	console.log(arguments)
	var instagramUrl="https://instagram.com/"
	return instagramUrl + username
}

console.log(cetakUrl("Whissper","Rafif"))

```

Jadi kode di atas sendiri adalah contoh dari `Arguments`,pada bagian `console.log(cetakUrl("Whissper","Rafif"))` kita tetap memberikan parameter akan tetapi di bagian `function cetakUrl(){` kita mengosongkannya,secara otomatis/default javascript akan menampung parameter itu ke dalam array yang bernama `Arguments`,jadi `Arguments` ini kita bisa manfaatkan...

Setelah kita memahami 3 konsep tersebut sekarang kita mulai memasuki materi utama yaitu `Closure`

#### Closure

Closure merupakan kombinasi antara function dan lingkungan leksikal(lexical scope) di dalam function tersebut(MDN)

Closure adalah sebuah function ketika memiliki akses ke parent scope-nya,meskipun parent scope-nya sudah selesai dieksekusi(W3SCHOOL)

Closure adalah sebuah function yang di kembalikan oleh function yang lain,yang memiliki akses ke lingkungan saat ia di ciptakan(CodeFellow)

Closure adalah sebuah function yang sebelumnya sudah memiliki data,hasil dari function yang lain(Tehcsith)

#### Lexical Scope

```javascript

	function init(){
		let nama="Rafif Faisal Ghozi" // Local Variable
		function tampilNama(){	// Inner Function	
		return nama // Akses ke parent variable
		}
		console.log(tampilNama())
	}
	
	init()

```

Jadi kode di atas sendiri adalah contoh dari `Closure` jadi singkatnya `Closure` sendiri ketika di sebuah function(parent) dan di dalammnya ada function(child) lagi,kemudian function yang menjadi child tersebut mempunyai ketergantungan ke function parentnya,seperti contoh di atas pada bagian `return nama` di akan mengambil variable dari parentnya

Pada kasus kali ini pula kita akan coba memodifikasi kode programmnya,coba perhatikan kode di bawah ini:

```javascript

	function init(){
		let nama="Rafif Faisal Ghozi" // Local Variable
		function tampilNama(){	// Inner Function	
		console.log(nama) // Akses ke parent variable
		}
		return tampilNama
	}
	
	init()


```

Jika kita menjalankan kode program di atas tidak akan terjadi apa-apa,jadi untuk bisa menjalankannya kita harus menampung `init()` ke dalam sebuah variable,jadi seperti instansiasi pada sebuah class

```javascript

	function init(){
		let nama="Rafif Faisal Ghozi" // Local Variable
		function tampilNama(){	// Inner Function	
		console.log(nama) // Akses ke parent variable
		}
		return tampilNama
	}
	
	let panggilNama=init()
	panggilNama()

```
Dengan menggunakan cari di atas kita nantinya bisa melakukan yang di namakan dengan `Factory Function`,Untuk contoh penggunaan dari `Factory Function` sendiri bisa kita lihat di bawah ini:

```javascript

	function ucapkanSalam(waktu){
	
	return function(nama){
		console.log(`HALO,SELAMAT ${waktu},Semoga harimu ${nama}`
	}	
	
	}
	
	let SelamatPagi=ucapkanSalam("Pagi")
	let SelamatSiang=ucapkanSalam("Siang")
	let SelamatMalam=ucapkanSalam("Malam")
	
	SelamatPagi("Rafif")
	SelamatSiang("Whissper")

```

Nah...jadi dengan menggunakan `Closure` sendiri kita bisa menggunakan yang namanya `Factory Function`,Selain dari `Factory Function` juga `Closure` juga bisa berfungsi seolah-olah kita `membuat private method/variable`,Jadi untuk pembahasannya bisa di lihat di bawah ini:

```javascript

	let count=0
	let add=function(){
	return ++count
	}
	
	console.log(add())
	console.log(add())
	console.log(add())	

``` 

Untuk kode program di atas sendiri tidak ada masalah dan jika jalankan pula,dia akan meng-outputkan `123`,Akan tetapi jika kita sudah banyak pemanggilan fungsi di atas hingga mencapai `100` dan terjadi perubahan pada variable count sendiri.

```javascript

	let count=0
	let add=function(){
	return ++count
	}
	
	console.log(add())
	count=0 // Terjadi Perubahan
	console.log(add())
	console.log(add())	

``` 

Jadi permasalannya variable `count` sendiri menjadi terpengaruh dan kita tidak menginginkannya,jadi untuk mengatasi masalah tersebut kita menggunakan closure

```javascript

	let add=function(){
	
	let count=0
	return function(){
	return ++count
	}

	}
	
	let a=add()
	console.log(a())
	console.log(a())
	console.log(a()) 
	

```

Dengan kode program di atas pula,kita jadi seolah-olah membuat sebuah private method/variable sendiri untuk menghitung,jadi `let count=0` tidak bisa di akses dari luar



