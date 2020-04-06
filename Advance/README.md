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







### 4.Arrow Function

Seperti yang kita ketahui dalam pembuatan function sendiri kita telah mencoba 2 cara pembuatan yaitu dengan menggunakan function declaration dan function expression/anonymous function

```javascript

	// Function Declaration
	
	function tampilPesan1(nama){
	alert(`Halo ${nama}`)
	}
	tampilPesan1("Rafif Faisal Ghozi")
	
	// Function Expression/Anonymous Function

	let tampilPesan2=function(nama){
	alert(`Halo ${nama}`)
	}
	tampilPesan2("Rafif Faisal Ghozi")


```

Bentuk lain yang lebih ringkas dari function expression(MDN),Jadi dengan menggunakan `Arrow Function` sendiri lebih ringkas,Contoh perbandingannya dengan function expression sendiri bisa di lihat di bawah ini:


```javascript

	// Function Expression/Anonymous Function

	let tampilPesan1=function(nama){
	alert(`Halo ${nama}`)
	}
	tampilPesan1("Rafif Faisal Ghozi")

	// Arrow Function
	
	let tampilPesan2=(nama)=>{
	alert(`Halo ${nama}`)
	}
	
	tampilPesan2("Rafif Faisal Ghozi")

```

Akan tetapi `Arrow Function` sendiri punya perbedaan tersendiri,Akan tetapi sebelum kita kesana,kita akan mempelajari terlebih dahulu tentang pembuatan `Arrow Function` ini,sebenarnya kode di atas tentang `Arrow Function` bisa lebih ringkas/singkat lagi,coba perhatikan di bawah ini:

```javascript

	function tampilPesan2=nama=>`Halo ${nama}`
	
	alert(tampilPesan2("Rafif Faisal Ghozi"))

```
Jadi jika kita punya 1 parameter kita tidak perlu menggunakan `()` dan jika kode di dalam function tersebut tidak panjang kita tidak perlu menggunakan `{}` dan jika tidak menggunakan kurung kurawal sendiri nanti javascript akan mengasumsikannya `return`

Akan tetapi jika kita ingin mengembalikan sebuah object di `Arrow Function` sendiri kita harus membungkusnya dengan `({})`,contoh:

```javascript

	let siswa=['Rafif','Whissper','Kanon']

	let data=siswa.map(nama=>({nama,jmlHuruf:nama.length}) /* Di javascript terbaru pula jika kita mempunyai nama object yang sama dengan nilai properti nya kita tidak perlu menuliskan nama:nama hanya nama saja pula bisa*/
	
	console.log(data)// Jika ingin rapih kita juga bisa menggunakan console.table()

```

#### Apakah ada batasan pada arrow function ini ?

##### 1.Arrow function paling baik digunakan untuk fungsi non-method. Perhatikan contoh berikut:

```javascript

	'use strict';
	var obj = {
	  i: 10,
	  b: () => console.log(this.i, this),
	  c: function() {
	    console.log(this.i, this);
	  }
	}

	obj.b(); // prints undefined, Window {...} (or the global object)
	obj.c(); // prints 10, Object {...}


```

Dari contoh di atas bisa dilihat fungsi b() tidak bisa mengakses properti i, saat mengakses this, ia justru menghasilkan global object.

##### 2.Arrow function tidak bisa digunakan sebagai konstruktor dan akan terjadi error jika menggunakan new.

```javascript

	var Foo = () => {};
	var foo = new Foo(); // TypeError: Foo is not a constructor

```

##### 3.Arrow function tidak memiliki objek arguments.

```javascript

	var f = () => arguments[0] + n;
	f(2); // Uncaught ReferenceError: arguments is not defined

```

Untuk tambahan sendiri ada sebuah permasalah kecil,coba perhatikan kode di bawah ini:

```javascript

	const siswa=function(){
	
	this.nama="Rafif Faisal Ghozi"
	this.umur=17
	
	this.sayHello=function(){
	console.log(`Halo nama saya ${this.nama},dan saya ${this.umur} tahun`)
	}
	
	setInterval(function(){
	console.log(this.umur++)
	},500)
	
	}

```

Dengan kode di atas sendiri pada bagian `setInterval` karena function tersebut adalah function declaration jadi dia terkena hoisting dan `this.umur++` sendiri jadi mengambil ke global context tidak ke local context,karena di global context di ada `this.umur` maka tidak di ketahui jika di run pula akan menghasilkan `NaN(Not a Number)`,jadi untuk mengatasi hal tersebut kita menggunakan `Arrow Function`,perhatikan kode di bawah:

```javascript

	const siswa=function(){
	
	this.nama="Rafif Faisal Ghozi"
	this.umur=17
	
	this.sayHello=function(){
	console.log(`Halo nama saya ${this.nama},dan saya ${this.umur} tahun`)
	}
	
	setInterval(()=>{
	console.log(this.umur++)
	},500)
	
	}

```

Karena singkatnya `Arrow Function` sendiri tidak mengenal yang namanya konsep `this`,jadi untuk di `this.umur` sendiri di atas nantinya dia akan mengambil ke lexical scope,karena seperti yang saya jelaskan sebelumnya constructor function sendiri di belakang layar seperti ini:

```javascript

	const siswa=function(){
	//let this={} 	
	
	this.nama="Rafif Faisal Ghozi"
	this.umur=17
	
	this.sayHello=function(){
	console.log(`Halo nama saya ${this.nama},dan saya ${this.umur} tahun`)
	}
	
	setInterval(function(){
	console.log(this.umur++)
	},500)
	
	//return this	
	
	}

```

Contoh pengimplementasian `Arrow Function`,perhatikan kode di bawah ini:

```javascript

	let box=document.querySelector('.box')

	box.addEventListener('click',function(){
	
	let satu='.size'
	let dua='.caption'	

	if(this.classList.contains('.size')){
	[satu,dua]=[dua,satu]
	/*Untuk menukar nilai di javascript terbaru menggunakan di atas,jika biasanya kita memerlukan variable baru untuk menampung sementara,seperti ini:
	satu=temp
	satu=dua	
	dua=temp
	*/
	}
	
	this.classList.toggle('.size')
	
	setTimeout(()=>{ // Menggunakan Arrow Function 
	this.classList.toggle('.caption')
	},600)

	})

```







### 5.Higher Order Function

Function yang beroperasi pada function yang lain.Baik itu di gunakan dalam argument,maupun sebagai return value(https://eloquentjavascript.net)

Pada dasarnya sendiri pada javascript sendiri function di sebut dengan `First Class Function` inti dari javascript sendiri adalah function,Dan di javascript pula function di perlakukan sebagai object

Javascript memperlakukan function sebagai object(sitepoint.com)

Jadi di javascript function itu bisa menjadi argument atau return value dari sebuah function,Coba perhatikan kode di bawah ini:

```javascript

	function kerjakanTugas(pelajaran,selesai){
	console.log("Mulai mengerjakan tugas ${matakuliah}...")
	selesai()
	}
	
	function selesai(){
	alert('Selesai mengerjakan tugas')
	}

	kerjakanTugas("B.Inggris",selesai)

```

Nah..jadi kode di atas kita menjadikan function `selesai` sendiri sebagai argument dari function `kerjakanTugas`,sekarang function `kerjakanTugas` sendiri bisa kita sebut dengan `HigherOrderFunction`,karena menerima argument dari sebuah function yaitu function `selesai`

Dan jika kita mempunyai function sebagai argument seperti function `selesai` sendiri,maka argument tersebut kita sebut dengan `Callback`,untuk contoh `HigherOrderFunction` yang mengembalikan nilai function bisa kita lihat di bawah ini:

```javascript

	function ucapkanSalam(waktu){
	return function(nama){
	console.log(`Selamat ${waktu},Semoga harimu menyenangkan ${nama}`)
	}	
	}

	let selamatPagi=ucapkanSalam("pagi")
	selamatPagi("Rafif Faisal Ghozi")

```

Terus apa sih fungsi dari `HigherOrderFunction` ??jawabannya banyak alasannya salah satunya untuk membuat yang namanya `Abtraksi`

Agar kode yang kita buat itu lebih sederhana atau bisa lebih simple,karena sebenarnya dengan menggunakan function kita menyembunyikan kerumitan

Semakin besar sebuah program,Semakin tinggi kompleksitasnya,semakin membingungkan programmernya(eloquentjavascript.net)

Ada dua cara untuk merancang sebuah software:Cara pertama adalah untuk membuat programmnya se-sederhana mungkin sehingga jelas-jelas tidak ada kekurangannya.dan cara lainnya adalah untuk membuat programnya se-komplek mungkin sehingga tidak ada kekurangan yang jelas(C.A.R.Hoare,1980 ACM Turing Award Lecture)

```javascript

	function repeatLog(n){
	for(let i=0;i<n;i++){
	console.log(i)
	}
	}
	repeatLog(10)

```

Jadi dengan menggunakan function sendiri tidak hanya membuat perulangan di atas menjadi dinamis tetapi lebih sederhana dan mudah untuk di panggil,Atau jika kita ingin mengubah aksinya tidak ingin `console.log()`,coba perhatikan kode di bawah ini:

```javascript

	function repeat(n,action){
	for(let i=0;i<n;i++){
	action(i)
	}		

	}
	
	repeat(10,console.log)
	repeat(20,alert)

```

Dengan kita sering menggunakan membuat function kita akan mendekati yang namanya `Functional Programming`

#### Contoh Higher Order Function

Sebelum mulai, diketahui kita memiliki array yang akan melakukan fungsi-fungsi higher-order ini.

```javascript

var source = [1,2,3,4,5]

```


##### -Array.prototype.map()

Looping pada semua elemen array, dan menjalankan operasi pada masing-masing elemen array. Hasilnya adalah array dengan panjang (length) yang sama namun isinya berupa hasil dari operasi pada masing-masing elemen array yang bersesuaian.

Contoh:

```javascript

var dikaliDua = source.map(function(currentValue, currentIndex){
   return currentValue * 2;
});

console.log(dikaliDua); // [2, 4, 6, 8, 10]

```

##### -Array.prototype.filter()

Looping pada semua elemen array, setiap elemen yang memenuhi kondisi akan dimasukkan ke dalam array hasil fungsi filter, array sumber akan tetap utuh.

Contoh:

```javascript

var filterGanjil = source.filter(function(currentValue, currentIndex){
   return currentValue % 2 === 1;
});

console.log(filterGanjil); // [1, 3, 5]

```

##### -Array.prototype.reduce()

Looping pada semua elemen array, dan menjalankan operasi pada elemen array. Hasil operasi pada elemen ke-i, akan dijadikan parameter untuk operasi pada elemen berikutnya (i+1), sehingga hasil operasi reduce adalah akumulasi operasi pada semua elemen, bukan array. Pendeknya, value yang tadinya banyak (array) menjadi satu saja.

Contoh:

```javascript

var ditotalin = source.reduce(function(previousValue, currentValue, currentIndex){
   return previousValue + currentValue;
});

console.log(ditotalin); // 15

```

Untuk reduce, bisa ditambahkan parameter kedua yaitu initial value sebagai nilai permulaan sebelum reduce dieksekusi.

Contoh:

```javascript

var ditotalin = source.reduce(function(previousValue, currentValue, currentIndex){
   return previousValue + currentValue;
}, 5);

console.log(ditotalin); // 20

```

##### -Array.prototype.forEach()

Looping pada semua elemen array, dan menjalankan operasi yang kita berikan.

Contoh:

```javascript

source.forEach(function(currentValue, currentIndex){
   console.log("index", currentIndex, "isinya", currentValue);
});

// index 0 isinya 1
// index 1 isinya 2
// index 2 isinya 3
// index 3 isinya 4
// index 4 isinya 5

```

##### -Array.prototype.reduceRight()

Sama seperti reduce, hanya saja dilakukan mulai dari elemen terakhir.

Contoh:

```javascript

var ditotalinDariKanan = source.reduceRight(function(previousValue, currentValue, currentIndex){
   return previousValue + currentValue;
});

console.log(ditotalinDariKanan); // 15

```

Sama seperti reduce, reduceRight juga bisa ditambahkan parameter kedua sebagai initial value.


Nah, bagaimana kalau mau digabung? Contohnya, setelah difilter, ingin dilakukan map. Caranya adalah dengan method/function chaining, caranya seperti ini:

```javascript

 var filterGanjilLaluKaliDua = source
   .filter(function(currentValue, currentIndex){
      return currentValue % 2 === 1;
   })
   .map(function(currentValue, currentIndex){
      return currentValue * 2;
   });

console.log(filterGanjilLaluKaliDua); // [2, 6, 10]

```

Tapi ingat, chaining di atas bisa dilakukan karena hasil dari filter adalah array, jadi masih memiliki method map. Kalau awalnya, misalnya, di­-reduce, hasilnya bukanlah array sehingga tidak memiliki method map.

Contoh kasus dari implementasi fungsi-fungsi di atas:

```html

<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>

<h3>My Videos</h3>

<ul>
    <li data-duration="15:27">Teknik Pomodoro</li>
    <li data-duration="11:18">JAVASCRIPT LANJUTAN | Higher Order Functions</li>
    <li data-duration="21:40">JAVASCRIPT LANJUTAN | This Pada Arrow Function</li>
    <li data-duration="19:38">Website Penipu</li>
    <li data-duration="12:10">JAVASCRIPT LANJUTAN | Arrow Function</li>
    <li data-duration="20:43">JAVASCRIPT LANJUTAN | Closure</li>
    <li data-duration="14:30">#TANYAPADIKA EP005</li>
    <li data-duration="26:38">JAVASCRIPT LANJUTAN | Execution Context</li>
    <li data-duration="17:33">JAVASCRIPT LANJUTAN | Prototype</li>
    <li data-duration="10:39">JAVASCRIPT LANJUTAN | Object.create()</li>
    <li data-duration="17:31">JAVASCRIPT LANJUTAN | Object (Revisited)</li>
    <li data-duration="14:25">5 Tips Bertanya Ketika Error</li>
</ul>

<h3>My Playlist</h3>

    <ol>
        <li>
            <h4>Javascript Lanjutan</h4>
            <p>Jumlah Video : <span class="jumlah-video"></span></p>
            <p>Total Durasi : <span class="total-durasi"></span></p>
        </li>
    </ol>


<script type="text/javascript" src="script.js"></script>
</body>
</html>

```

```javascript

//Ambil Semua Element Video
let elVideo=Array.from(document.querySelectorAll("[data-duration]"))

//Pilih Hanya Yang 'JAVASCRIPT LANJUTAN'
let javascriptLanjutan=elVideo.filter((currentValue,currentIndex)=>currentValue.textContent.includes('JAVASCRIPT LANJUTAN'))

//Ambil Durasi Masing-Masing Video
.map((currentValue,currentIndex)=>currentValue.dataset.duration)

//Ubah Durasi Menjadi Float,Ubah Menit Menjadi Menit
.map((currentValue,currentIndex)=>{
	//10:18 [10,18] split
	let parts=currentValue.split(":").map(item=>parseFloat(item))
	return (parts[0] * 60) + parts[1]
})

//Jumlahkan Semua Detik
.reduce((previousValue,currentValue)=>previousValue+currentValue)

//Ubah Formatnya Jam Menit Detik
let jam=Math.floor(javascriptLanjutan/3600)
javascriptLanjutan= javascriptLanjutan - jam * 3600 //Untuk mendapatkan sisa dari detik di atas 8292
let menit=Math.floor(javascriptLanjutan / 60)
let detik=javascriptLanjutan - menit * 60

//Simpan Ke DOM
document.querySelector(".total-durasi").textContent=`${jam} Jam,${menit} Menit,${detik} Detik`
document.querySelector(".jumlah-video").textContent=elVideo.filter((currentValue,currentIndex)=>currentValue.textContent.includes("JAVASCRIPT LANJUTAN")).length

```

#### Rumus Menghitung Satuan Waktu

untuk satuan waktu dapat kita gunakan tangga  

```
jam

      menit

                detik

```

pada tangga ini, turun 1 tangga dikali 60, sebaliknya naik 1 tangga dibagi 60

#### Pembahasan

dari pendahuluan sdh diberikan tangga, dan penjelasan jika turun 1 tangga dikali 60 dan jika naik 1 tangga dibagi 60

contoh soal,

2 menit = ... detik

dari menit diubah menjadi detik, lihat tangga dari menit ke detik turun 1 tangga artinya kita kali 60

2 menit = 2 x 60 detik

             = 120 detik

contoh soal ke-2

180 detik = ... menit

dari detik dirubah menjadi menit, lihat tangga dari detik ke menit naik 1 tangga artinya kita bagi 60

180 detik = 180 : 60 menit

                = 3 menit

Kesimpulan
mengubah menit menjadi detik dengan cara dikali 60







### 6.Template Literals / Template String

Salah satu yang sering kita lakukan saat membuat aplikasi adalah menggabungkan string dengan hasil ekspresi, misalnya untuk menampilkan pesan error atau informasi. Misalnya menulis halaman "Selamat datang, Rafif Faisal Ghozi", di mana kata "Rafif Faisal Ghozi" diambil dari data pengguna yang login ke aplikasi. Pada javascript ES5, kita menulisnya seperti ini:

```javascript

var nama = "Rafif Faisal Ghozi";

var pesan = "Selamat datang," + nama + "!";

console.log(pesan); // "Selamat datang, Rafif Faisal Ghozi!"

```

Nah, sekarang kita bisa menggunakan template literal ini sehingga kita bisa mengurangi penggunaan simbol operator tambah. Kita bisa menulis kalimat yang sama tanpa menggunakan simbol operator tambah, hanya saja kita harus menggunakan backtick ```(`)```, lokasi tombolnya pada keyboard ada di sebelah kiri angka 1. Contohnya:

```javascript

var nama = "Rafif Faisal Ghozi";

var pesan = `Selamat datang, ${nama}!`;

console.log(pesan); // "Selamat datang, Rafif Faisal Ghozi!"

```

kalau ingin ada backtick di dalam template ini, bisa di-escape dengan backslash..

```javascript

`\`` === '`' // --> true

```

Kelebihan dari `Template Literals` sendiri sebagai berikut:

##### - Multi Line

Dengan menggunakan `Template Literals` sendiri kita tidak perlu khawatir akan perpindahan baris,jika biasanya kita menuliskan seperti ini:

```javascript

console.log('string text line 1\n' +
'string text line 2');
// "string text line 1
// string text line 2"


```

Dengan `Template Literals`

```javascript

console.log(`string text line 1
string text line 2`);
// "string text line 1
// string text line 2"


```

#### - Expression Interpolation

Jika biasa jika kita membuat expresi seperti ini:

```javascript

let a = 5;
let b = 10;
console.log('Fifteen is ' + (a + b) + ' and\nnot ' + (2 * a + b) + '.');
// "Fifteen is 15 and
// not 20."

```

Dengan menggunakan `Template Literal` sendiri jadi seperti ini:

```javascript

let a = 5;
let b = 10;
console.log(`Fifteen is ${a + b} and
not ${2 * a + b}.`);
// "Fifteen is 15 and
// not 20."

```

#### - Nesting Templates

Dalam kebanyakan kasus sendiri,template bersarang sangat mudah di gunakan dan mudah untuk di manipulasi dengan `Template Literal`,jadi kita bisa melakukan operator `Ternary` di dalam `Template Literal` sendiri,Perhatikan contoh di bawah ini:

```javascript


	const student = {
	  name: 'Kristine',
	  food: 'Chipotle',
	  city: 'Scottsdale'
	};

	
	const html = `
	<div>
	  <h1>Name: ${student.name}</h1>
	  <h3>Location: ${student.city}</h3>
	  ${student.food ? `<h3>Food: ${student.food}</h3>` : ''}
	</div>
	`


```

#### - Tagged Template Literals

Bentuk yang lebih kompleks dari `Template Literals`,Memungkinkan kita untuk membaca template literals melalui sebuah function(MDN Web Docs)

Jadi `Tagged Template Literals` sendiri adalah bentuk lanjutan atau bisa kita sebut advance dari `Template Literals`,Dengan menggunkan `Tagged Template Literals` sendiri kita jadi bisa mem-parsing sebuah string ke sebuah function

Dan untuk argument pertama pada functionnya nanti mengandung/berisi sebuah array of string,perhatikan contoh di bawah ini:

```javascript

	let nama="Rafif Faisal Ghozi"
	let umur=17

	function coba(string,...values){/* jika juga bisa menggunakan rest arguments untuk menggantikan nama dan umur,jika biasanya seperti ini:coba(string,nama,umur) kita bisa menggantinya seperti yang di atas*/
		//string[0]=Halo,nama saya
		//string[1]=,saya
		//string[2]=.tahun
		let str=""

		string.forEach((currentValue,currentIndex)=>{
			str+=`${currentValue}${values[currentIndex]||''}`
		})

		return str

		// return string.reduce((previousValue,currentValue,currentIndex)=>`${previousValue}${currentValue}${values[currentIndex]||''}`)

	}

	let output=coba `Halo,nama saya ${nama},saya ${umur}.tahun`

	console.log(output)

```

Dengan menggunakan `Tagged Template Literals` sendiri,kita jadi bisa memanipulasi lebih jauh lagi,untuk contoh perhatikan di bawah ini:

```javascript

	let nama="Rafif Faisal Ghozi"
	let umur=17
	let email="faisalghozi458@gmail.com"

	function highLight(string,...values){/* jika juga bisa menggunakan rest arguments untuk menggantikan nama dan umur,jika biasanya seperti ini:coba(string,nama,umur) kita bisa menggantinya seperti yang di atas*/
		//string[0]=Halo,nama saya
		//string[1]=,saya
		//string[2]=.tahun
		let str=""

		string.forEach((currentValue,currentIndex)=>{
			str+=`${currentValue}<span style="background-color:'salmon'">${values[currentIndex]||''}</span>`
		})

		return str

		// return string.reduce((previousValue,currentValue,currentIndex)=>`${previousValue}${currentValue}${values[currentIndex]||''}`)

	}

	let output=highLight `Halo,nama saya ${nama},saya ${umur}.tahun`

	document.body.innerHtml=output

```

#### Penggunaan Lain Dari Tagged Template Literals

##### - Escaping / Sanitize HTML Tags

`Tagged Template Literals` pula bisa kita gunakan untuk mem-filter sebuah string agar menjadi aman,Atau bisa kita sebut untuk menghindari serangan dari XSS(Cross-Site-Scripting),atau juga kita bisa untuk menghindari kata-kata kasar kita bisa mem-filternya

```javascript

	function sanitize(strings,...values){

	return DOMPurify.sanitize(aboutMe);

	}

	const name="petyr baelish"
	const aboutMe=`I love to do evil <img src="http://unsplash.it/100/100?random" onload="alert('I hacked you.Haha');">`

	const html=sanitize `
	<h3>${name}</h3>
	<p>${aboutMe}</p>
	`

```

##### - Translation & Intertionalization

Dengan `Tagged Template Literals` juga kita bisa melakukan yang namanya tranlation atau biasa kita lihat sepert google translate,contoh kode di bawah ini dengan menggunakan libraries lain kita bisa melakukan translate:

```javascript

	console.log(i18n`Hello ${ name }, you have ${ amount }:c in your bank account.`)
	// Hallo Steffen, Sie haben US$ 1,250.33 auf Ihrem Bankkonto.

```
https://github.com/skolmer/es2015-i18n-tag


##### - Styled Components

Sebenarnya contoh ini ketika kita menggunakan react

```javascript

	const Title = styled.h1`
	  font-size: 1.5em;
	  text-align: center;
	  color: palevioletred;
	`;


```
https://www.styled-components.com/docs/basics#getting-started








### 7.Destructuring Variable / Destructuring Assignment

Expression pada javascript yang membuat kita dapat `Membongkar` nilai dari array atau property dari object `variable` yang terpisah(MDN Web Docs)

Belajar bahasa pemrograman akan sering berkutat dengan yang namanya memanipulasi data. memasukkan sebuah variabel ke dalam array/object atau sebaliknya.

Destructuring assignment adalah ekspresi javascript yang memungkinkan untuk membagi atau memecah nilai dari sebuah array atau objek ke dalam variabel yang berbeda. Fitur ini hampir mirip dengan fitur yang ada pada bahasa pemrograman lain seperti Perl dan Python.


#### Array Destructuring 

```javascript

	let angka=[1,2,3]

	// Tidak menggunakan Destructuring
	
	// let a=angka[0]
	// let b=angka[1]
	// let c=angka[2]

	// Dengan menggunakan Destructuring

	let [a,b,c]=angka

	console.log(a)
	console.log(b)
	console.log(c)

```

Pada contoh pertama, kita mempunyai variabel numbers dengan tipe data array yang mempunyai nilai 1,2,3. Kemudian dengan destructuring assignment, kita bisa memecah variabel tersebut ke dalam variabel a,b,c hanya dengan satu baris kode. Jika tanpa destructuring assignment, kita perlu menuliskan dua langkah/baris kode. seperti yang tertulis juga pada kode di atas.

##### Swap Items

Membalik atau menukar sebuah nilai antar variabel menjadi lebih mudah dan simpel menggunakan destructuring assignment.

```javascript

	let a = 5
	let b = 10
	let [a, b] = [b, a]
	console.log(a) // 10
	console.log(b) // 5

```

Kita bisa mengabaikan(ignore) beberapa value yang tidak ingin dipecah ke variabel lain.

```javascript

	let a = [1,2,3];
	let [b,,c] = a;
	console.log(b); // 1
	console.log(c); // 3

```

##### Return Value Pada Function

```javascript

	function angka(){
		return [1,2,3]
	}

	let [a,b,c]=angka()
	
	console.log(a) // 1
	console.log(b) // 2
	console.log(c) // 3


```

##### Rest Parameter

```javascript

	let numbers = [1,2,3,4];
	let [firstNumber, ...otherNumber] = numbers;
	console.log(firstNumber); // 1
	console.log(otherNumber); // [2,3,4]

```

Destructuring assignment juga bisa digunakan bersama spread operator seperti pada contoh di atas. Bisa kita liat, kita memecah nilai variabel numbers kedua variabel yang berbeda yaitu firstNumber yang mengambil nilai index pertama yaitu 1 dan otherNumber mengambil nilai lain dari variabel numbers menjadi sebuah variabel array baru (otherNumbers) dengan nilai [2,3,4]


#### Object Destructuring

```javascript

	let me = {
		name: "Rafif",
		age: 17
	};
	let {name,age} = me;
	console.log(name); // Rafif
	console.log(age); // 17

```

Untuk mengekstrak atau memecah variabel menggunakan destructuring assignment pada objek, berpatokan pada key objek itu. Semisal pada contoh di atas. kita ingin memecah variabel me menjadi 2 variabel berbeda yang masing-masing akan mengambil nilai dari key name dan age. maka kita menggunakan key tersebut untuk memecahnya. Jika kita hanya ingin mengambil nilai dari key age nya saja maka bisa bisa menuliskannya seperti ini.

```javascript

	let me={
		name:"Rafif",
		age:17
	}
	let {age}=me
	console.log(age) // 17 

```

Pada contoh di bawah ini sama seperti contoh sebelumnya, hanya saja kita memecah variabel tersebut dan memberikan nama baru untuk variabel-variabelnya. variabel nama mengambil nilai dari key “name” dan variabel umur mengambil nilai dari key “age”. output yang dihasilkan tetap sama.


```javascript

	let me={
		name:"Rafif",
		age:17
	}

	let {name:nama,age:umur}=me

	console.log(nama) // Rafif
	console.log(umur) // 17

```

Jika kita ingin mengkombinasikan destructuring assignment dengan spread operator untuk memecah nilai dari sebuah objek seperti ini:


```javascript

	let numbers = {
		a: 1,
		b: 2,
		c: 3,
		d: 4
	};
	let {a,b,...n} = numbers;
	console.log(a); //1
	console.log(b); //2
	console.log(n); // {c:3, d: 4}

```

Jika variabel yang akan diberi nilai dari pecahan variabel lain menggunakan destructuring assignment sudah dideklarasikan, maka untuk memecahnya kita harus menuliskannya di dalam sebuah blok atau dari contoh di atas ditulis di antara tanda kurung ().

```javascript

	let name,age;
	let me = {name: "Rafif", age: 17};
	/**
	* harus di tulis didalam blok/atau didalam tanda ()
	**/
	({name,age} = me); 
	console.log(name); // Rafif
	console.log(age); // 17

```

#### Destructuring Return Function

```javascript

	function penjumlahanPerkalian(a,b){
		return [a+b,a*b]
	}

	// Jika Tanpa Menggunakan Destructuring
	// let jumlah=penjumlahanPerkalian(2,3)[0]
	// let kali=penjumlahanPerkalian(2,3)[1]

	//Dengan Destructuring

	let [jumlah,kali]=penjumlahanPerkalian(2,3)
	console.log(jumlah)
	console.log(kali)




```

Jika kita perhatikan kode di atas sendiri tidak ada masalah akan tetapi bagaimana jika kita ingin menambahkan satu variable lagi yaitu variable bagi,akan tetapi return value dari function nya hanya mengembalikan 2 array saja

```javascript

	function penjumlahanPerkalian(a,b){
		return [a+b,a*b]
	}

	// Jika Tanpa Menggunakan Destructuring
	// let jumlah=penjumlahanPerkalian(2,3)[0]
	// let kali=penjumlahanPerkalian(2,3)[1]

	//Dengan Destructuring

	let [jumlah,kali,bagi="tidak ada"]=penjumlahanPerkalian(2,3)
	console.log(jumlah)
	console.log(kali)

```

Dengan kode di atas kita bisa melakukan pengisian nilai default jika sebuah array nya tidak memenuhi,sekarang jika kita perhatikan lagi jika kita melakukan `Destructuring Array` urutan si array dengan pemberian nilai/assignment nya harus sama,terus bagaimana jika data nya berantakan dan kita tidak tahu urutannya,nah...dengan menggunakan `Destructuring Object` sendiri kita bisa melakukannya dengan acak

```javascript

	function kalkulasi(a,b){
		return {
			tambah : a+b,
			kali : a*b
			kurang : a-b
			bagi : a/b
		}
	}

	// Jika Tanpa Menggunakan Destructuring
	// let jumlah=penjumlahanPerkalian(2,3)[0]
	// let kali=penjumlahanPerkalian(2,3)[1]

	//Dengan Destructuring

	let {tambah,kurang,bagi,kali}=kalkulasi(2,3)
	console.log(jumlah)
	console.log(bagi)
	console.log(kali)
	console.log(kurang)

```

Dengan menggunakan `Destructuring Object` sendiri kita tidak perlu khawatir akan urutannya


#### Destructuring Function Arguments

```javascript

	let Siswa={
		nama:"Rafif",
		umur:17	
	}

	function cetakSiswa(nama,umur){
		return `Halo ${nama},Kamu berumur ${umur}.tahun`
	}

	console.log(cetakSiswa(Siswa.nama,Siswa.umur))

```

Jika tidak menggunakan `Destructuring` sendiri bisa kita lihat pada kode di atas,masalahnya sendiri bagaimana jika dari object `Siswa` sangat kompleks,nah..dengan menggunakan destructuring sendiri kita akan lebih simple

```javascript

	let Siswa={
		nama:"Rafif",
		umur:17	
	}

	function cetakSiswa({nama,umur}){
		return `Halo ${nama},Kamu berumur ${umur}.tahun`
	}

	console.log(cetakSiswa(Siswa))

``` 

Terus bagaimana jika ada object yang bersarang ??perhatikan kode di bawah ini:

```javascript

	let Siswa={
		nama:"Rafif",
		umur:17,
		hobi:{
			kesatu:"ngoding",
			kedua:"memancing"
		}	
	}

	function cetakSiswa({nama,umur,hobi:{kesatu,kedua}}){
		return `Halo ${nama},Hobi pertama kamu ${kesatu},Kamu berumur ${umur}.tahun`
	}

	console.log(cetakSiswa(Siswa))

```

Jadi kode di atas sendiri `Destructuring` di dalam `Destructuring`,setelah kita memecah object `Siswa` kita juga memecah object yang bersarangnnya yaitu `hobi`









### 8.Perulangan Baru Di Javascript(For...Of VS For...In)

#### For...Of

Creates a loop iterating over `iterable object`
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)

Jadi adalah sebuah looping yang di buat untuk mengulang atau menulusuri sebuah object yang `Iterable`,
contoh object yang `Iterable` dan dapat di looping dengan `For...Of` sendiri bisa di lihat di bawah ini:

###### - String
###### - Array
###### - Arguments
###### - NodeList
###### - TypedArray
###### - Map
###### - Set
###### - User-Defined Iterables

```javascript

	
	// Array
	let angka=[1,2,3]

	for(let a of angka){
		console.log(a)
	}

	// String
	let nama="Rafif"

	for(let n of nama){
		console.log(n)
	}

	// NodeList
	let liNama=document.querySelectorAll('.nama')

	for(let l of liNama){
		console.log(l)
	}


	function coba(){
		for(let arg of arguments){
			console.log(arg)
		}
	}

	coba(1,2,3,4,5)



```

Perlu kita ketahui juga bahwa `For...Of` tidak mempunyai indek argumentnya tidak seperti `forEach()` sendiri,jadi untuk mengatasinya sendiri kita bisa melakukan seperti ini:

```javascript

	let angka=[1,2,3]

	// Dengan forEach()
	/*
	angka.forEach((currentValue,currentIndex)=>console.log(currentValue,currentIndex))
	*/

	// Dengan For...Of
	for(let a of angka.enteries()){
		console.log(a) // Output:[0,1],[1,2],[3,2]
	}


```

Dan perlu kita ketahui juga bahwa `Arguments` sendiri pada function itu berbeda dengan `Array` walaupun sama mempunyai key dan value akan tetapi `Prototype` nya sendiri berbeda,perhatikan contoh kasus di bawah ini yang tidak bisa di atasi oleh method seperti `forEach` dan `reduce`:

```javascript

	function tambah(){
		let i=0;
		for(let arg of arguments){
			i+=arg
		}
		return i
	}

	console.log(tambah(1,2,3,4,5))


```

#### For...In

Creates a loop only iterating over `enumerable`
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)

Jadi looping ini di gunakan hanya untuk mengulang `Enumerable`,`Enumerable` di sini maksudnya adalah property pada sebuah object

```javascript

	let Siswa={
		nama:"Rafif",
		umur:17,
		email:"faisalghozi458@gmail.com"
	}

	for(let s in Siswa){
		console.log(`key-${s}`) // Untuk mengambil key/index
		console.log(`value-${Siswa[s]}`) // Untuk mengambil value/isi
	}


```


