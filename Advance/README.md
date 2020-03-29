## JAVASCRIPT ADVANCE

### 1.Object

`Object` adalah suatu method yang menyimpan `Variable(Property)` dan `Fungsi(Method)`,dan untuk membuat `Object` di javascript pula  di bagi menjadi 4 jenis yaitu:

#### - OBJECT LITERAL

```javascript

let siswa={
	nama:"Rafif Faisal Ghozi",
	umur:17,
	energy:10,
	makan:function(porsi){
		this.energy=this.energy+porsi
		console.log(`SELAMAT DATANG ${nama},ENERGY ANDA SEKARANG ${this.energy},SELAMAT MAKAN...!!`)
	}
}

let siswa2={
	nama:"Whissper",
	umur:15,
	energy:120,
	makan:function(porsi){
		this.energy+=porsi
		console.log(`SELAMAT DATANG ${nama},ENERGY ANDA SEKARANG ${this.energy},SELAMAT MAKAN...!!`)
	}
}

```

#### - FUNCTION DECLARATION

```javascript

function siswa(nama,umur,energy){
	let siswa={}
	siswa.nama=nama
	siswa.umur=umur
	siswa.energy
	siswa.makan=function(porsi){
		this.energy+=porsi
		console.log(`SELAMAT DATANG ${this.nama},ENERGY ANDA SEKARANG ${this.energy},SELAMAT MAKAN...!!`)
	}
	siswa.main=function(jam){
		this.energy-=jam
		console.log(`HALO ${this.nama} SELAMAT BERMAIN`)
	}
	return siswa
}

let rafif=siswa("Rafif Faisal Ghozi",17,10)

let whissper=siswa("Whissper",15,120)

```

#### - CONSTRUCTOR FUNCTION

```javascript

function siswa(nama,umur,energy){
	this.nama=nama
	this.umur=umur
	this.energy=energy
	this.makan=function(porsi){
		his.energy+=porsi
		console.log(`SELAMAT DATANG ${this.nama},ENERGY ANDA SEKARANG ${this.energy},SELAMAT MAKAN...!!`)
	}
	this.main=function(jam){
		this.energy-=jam
		console.log(`HALO ${this.nama} SELAMAT BERMAIN`)
	}
}

let rafif=new siswa("Rafif Faisal Ghozi",17,10)

let whissper=new siswa("Whissper",15,120)


```

#### - OBJECT.CREATE()

`Object literal` sendiri mempunyai problem/masalah yaitu kurang cocok untuk membuat object yang banyak

`Function Declaration` sendiri juga mempunyai problem/masalah,ketika ada property atau method yang tidak di pakai,property dan method tersebut tetap tersimpan kedalam memori,jadi kurang efektif...
tetapi untuk mengatasi hal tersebut kita bisa menggunakan bantuan dari object literal pada `Function Declaration`.Contoh:

```javascript

let methodSiswa={
	makan:function(porsi){
	this.energy+=porsi
	console.log(`SELAMAT DATANG ${this.nama},ENERGY ANDA SEKARANG ${this.energy},SELAMAT MAKAN...!!`)
	},
	main:function(jam){
	this.energy-=jam
	console.log(`HALO ${this.nama} SELAMAT BERMAIN`)
	}
}

function siswa(nama,umur,energy){
	let siswa={}
	siswa.nama=nama
	siswa.umur=umur
	siswa.energy
	siswa.makan=methodSiswa.makan
	siswa.main=methodSiswa.main
	return siswa
}

let rafif=siswa("Rafif Faisal Ghozi",17,10)

let whissper=siswa("Whissper",15,120)


```

Dengan kode di atas kita telah melakukan sedikit perbaikan,jadi untuk method `siswa.makan`,`siswa.main` itu mengacu ke object literal dari `methodSiswa` dan object tersebut pula di simpan ke memori hanya satu kali,tidak seperti sebelumnnya...akan tetapi kekurangan dari kode di atas pula,ketika kita membuat perubahan seperti menambahkan,menghapus property atau method baru di `methodSiswa` mau tidak mau kita harus mendaftarkan/menginstasiasi property/object tersebut ke dalam `Function Declaration` siswa,jadi problem nya kita mengelola 2 object sekaligus,tetapi dengan menggunakannya fungsi/method bawaan dari javascript yaitu `Object.create()` kita tidak perlu mengkhawatirkan perubahan di method yang menjadi parameter dari `Object.create()` tersebut,jadi `Object.create()` pula hampir mirip dengan konsep turunan/inheritance di Class,dengan begini kita tidak perlu bekerja 2 kali pada object tersebut.Contoh:


```javascript

let methodSiswa={
	makan:function(porsi){
	this.energy+=porsi
	console.log(`SELAMAT DATANG ${this.nama},ENERGY ANDA SEKARANG 	${this.energy},SELAMAT MAKAN...!!`)
	},
	main:function(jam){
	this.energy-=jam
	console.log(`HALO ${this.nama} SELAMAT BERMAIN`)
	}
}

function siswa(nama,umur,energy){
	let siswa=Object.create(methodSiswa)
	siswa.nama=nama
	siswa.umur=umur
	siswa.energy
	return siswa
}

let rafif=siswa("Rafif Faisal Ghozi",17,10)

let whissper=siswa("Whissper",15,120)


```


### 2.PROTOTYPE

Jadi setelah kita mempelajari tentang teknik pembuatan object di javascript seperti `Object Literal`,`Function Declaration`,`Constructor Function`,`Object.create()`

Dan terakhir pula kita telah mengatasi masalah-masalah,tetapi asal kita ketahui sebelumnya kita telah membuat object dengan `Function Declaration` dengan perbaikan,akan tetapi teknik tersebut masih di bilang sedikit kurang,masalahnya adalah kita jadi membuat dua object yaitu `methodSiswa` sebagai parent dan object siswa,dengan adanya `Prototype` sendiri kita bisa lebih mengefektifkan lagi pembuat object ini,jadi nantinya kita akan membuat satu object saja yaitu siswa dan `methodSiswa` sendiri akan kita hapus.

Untuk bisa melakukan yang di sebut dengan prototype kita harus menggunakan `Constructor Function`,sebenarnya `ConstructOr Function` sendiri tidak jauh beda dengan `Function Declaration`,untuk mengetahui di belakang layar dari `Constructor Function` sendiri bisa kita perhatikan kode di bawah ini:

```javascript

function siswa(nama,umur,energy){
	let this=Object.create(siswa.prototype) //Di Belakang Layar
	this.nama=nama
	this.umur=umur
	this.energy=energy
	this.makan=function(porsi){
		this.energy+=porsi
		console.log(`SELAMAT DATANG ${this.nama},ENERGY ANDA SEKARANG ${this.energy},SELAMAT MAKAN...!!`)
		}
	this.main=function(jam){
		this.energy-=jam
		console.log(`HALO ${this.nama} SELAMAT BERMAIN`)
	}
	
	return this //Di Belakang Layar

}

```

Jadi singkatnnya kita akan memanfaatkan method prototype ini untuk bisa kita gunakan,jadi kita tidak perlu membuat method lain seperti `methodSiswa`,untuk contoh prototype sendiri bisa kita lihat kode di bawah ini:

```javascript

	siswa.prototype.makan=function(porsi){
		this.energy+=porsi
		console.log(`SELAMAT DATANG ${this.nama},ENERGY ANDA SEKARANG ${this.energy},SELAMAT MAKAN...!!`)
	}

	siswa.prototype.main=function(jam){
		this.energy-=jam
		console.log(`HALO ${this.nama} SELAMAT BERMAIN`)
	}
	
	function siswa(nama,umur,energy){
		this.nama=nama
		this.umur=umur
		this.energy=energy
	}

	let rafif=new siswa("Rafif Faisal Ghozi",17,10)

	let whissper=new siswa("Whissper",15,120)

```

Jadi di belakang layar sendiri `Constructor Function` sendiri mirip dengan `Function Declaration`,Perbedaannya sendiri di bagian `let this=Object.create(siswa.prototype)` jadi sebenarnya si `Constructor Function` sendiri memanggil sebuah method prototype yang bisa di bilang menjadi parent defaultnya.sebenarnnya prototype sendiri adalah belakang layar dari fungsi class.bisa di bilang kode di atas sama dengan kode di bawah ini:

```javascript

class siswa{

	constructor(nama,umur,energy){
		this.nama=nama
		this.umur=umur
		this.energy=energy
	}

	makan(porsi){
		this.energy+=porsi
		console.log(`SELAMAT DATANG ${this.nama},ENERGY ANDA SEKARANG ${this.energy},SELAMAT MAKAN...!!`)
	}

	main(jam){
		this.energy-=jam
		console.log(`HALO ${this.nama} SELAMAT BERMAIN`)
	}

}

```

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