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

Function yang beroperasi pada function yang lain.Baik itu di gunakan dalam argument,maupun sebagai return value( https://eloquentjavascript.net)

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

##### Spread Parameter

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
( https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)

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
( https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)

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







### 9.Spread Operator

Memecah (expand / unpack) iterables menjadi single element
( https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)

Seperti yang kita ketahui bahwa `iterable` sendiri ada :

###### - String
###### - Array
###### - Arguments
###### - NodeList
###### - TypedArray
###### - Map
###### - Set
###### - User-Defined Iterables

```javascript

	 let nama=['Rafif','Faisal','Ghozi']
	 console.log(...nama) // Spread Operator
	 console.log(...nama[0]) // Outputnya R a f i f

```
Jadi singkatnya `Spread Operator` sendiri memecah sebuah `iterable` menjadi tiap-tiap element,harap di perhatikan bukan menjadi variable tapi menjadi tiap-tiap element

`Spread Operator` sendiri mempunyai berberapa fungsi di antaranya sendiri seperti di bawah ini :

#### Menggabung Array

Sebenarnya kita juga bisa menggabung array dengan sebuah method dari array sendiri yaitu `Array.prototype.concat()`,tapi dengan `Spread Operator` kita bisa lebih flesibel jika kita ingin menyisipkan sebuah array baru

```javascript

	let nama=['Rafif','Faisal','Ghozi']
	let nama2=['Whissper','Zero']
	let gabungNama=[...nama,"Baru",...nama2]

	console.log(gabungNama)

```

`Spread Operator` juga bisa di gunakan untuk meng-copy sebuah array,tapi sebelumnya perhatikan kode di bawah ini:

```javascript

	let nama=['Rafif','Faisal','Ghozi']
	let siswa=nama
	siswa[0]="Whissper"
	console.log(siswa) // Output:['Whissper','Faisal','Ghozi']
	console.log(nama) // Output:['Whissper','Faisal','Ghozi']

```

Jika kita perhatikan kode di atas sendiri,jika di lihat sekilas kita juga seperti melakukan copy sebuah array,akan tetapi sebenarnya kode di atas pula tidak meng-copy sebuah array akan tetapi membuat sebuah referensi,jadi ketika kita melakukan perubahan pada array `siswa` maka array `nama` pula akan berubah

Nah...dengan menggunakan `Spread Operator` sendiri kita bisa melakukan benar-benar copy tidak me-reference

```javascript

	let nama=['Rafif','Faisal','Ghozi']
	let siswa=[...nama]
	siswa[0]="Whissper"
	console.log(siswa) // Output:['Whissper','Faisal','Ghozi']
	console.log(nama) // Output:['Rafif','Faisal','Ghozi']

```

Untuk lebih bisa memahami lagi tentang `Spread Operator` perhatikan studi kasus di bawah ini yang akan membuat text animasi yang ketika di hover :

```html

	<!DOCTYPE html>
		<html>
		<head>
		    <title>TEXT ANIMATION</title>
		</head>
		<style type="text/css">
		    body{
		        margin:0;
		        padding:0;
		        background-color:salmon;
		    }
		    h1{
		        text-align: center;
		        font-family:arial;
		        font-size:80px;
		        color:white;
		        margin-top:30%;
		        transition:.3s
		    }
		    span{
		        display:inline-block;
		        cursor:pointer;
		        transition:.3s
		    }

		    h1 span:hover{
		        transform: scale(2) translateY(-20px);
		    }

		</style>
		<body>

		    <h1>RAFIF</h1>

		</body>
		<script type="text/javascript" src="script.js"></script>
	</html>


```

```javascript

	let nama=document.querySelector('h1')
	let el=nama.textContent
	let pecah=[...el].map((currentValue,currentIndex)=>`<span class="nama">${currentValue}</span>`).join("")

	nama.innerHTML=pecah


```







### 10.Rest Parameters

Merepresentasikan argument pada function dengan jumlah yang tidak terbatas menjadi sebuah array
( https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/rest_parameters )

```javascript

	function myFunc(a,b,...myArgs){ // ...myArgs tidak boleh berada pada urutan pertama harus di akhir
		console.log(myArgs) // [1,2,3,4,5]
	}
	myFunc(1,2,3,4,5)

```

Di atas sendiri adalah contoh dari penggunaan `Rest Parameter`,jika kita perhatikan `Rest Parameter` sendiri tidak boleh berada di awal urutan jika memaksakan akan muncul error seperti ini `Uncaught SyntaxError: Rest parameter must be last formal parameter`

Singkatnnya `Rest Parameter` mengubah parameter yang tadinya variable menjadi sebuah array,jika kita ingin memanggil angka `1` dalam kode di atas kita hanya tinggal menuliskannya seperti ini `console.log(myArgs[0])`


Di sini saya akan memberikan contoh penggunaan dari `Rest Parameter` dalam kode program yang pernah kita buat sebelumnya

```javascript

	function jumlahkan(...angka){
		let sum=0
		for(let a of angka){
			sum+=a
		}
		return sum

		// Jika menggunakan Reduce
		// angka.reduce((previousValue,currentValue)=>previousValue+currentValue) 

	}

	console.log(jumlahkan(1,2,3,4,5))


```

`Rest Parameter` juga dapat di gunakan pada `Array Destructuring` dan juga `Object Destructuring`,perhatikan kode di bawah ini:

```javascript

	// Array Destructuring Dengan Rest Parameter

	let kelompok=['Rafif','Whissper','Ghozi','Faisal']
	let [ketua,wakilketua,...anggota]=kelompok
	console.log(ketua) // Rafif
	console.log(wakilketua) // Whissper
	console.log(anggota) // ['Ghozi','Faisal']



	// Object Destructuring Dengan Rest Parameter

	let team={
		pm:"Rafif",
		frontEnd1:"Whissper",
		frontEnd2:"Ghozi",
		devOps:"Faisal"
	}

	let [pm,devOps,...myTeam]=team
	console.log(pm) // Rafif
	console.log(devOps) // Faisal
	console.log(myTeam) // ['Whissper','Ghozi']

```

Untuk lebih sedikit komplek dan lebih paham perhatikan kode bawah ini untuk mengetahui sebuah type data dari sebuah nilai :

```javascript

	function filterBy(type,...values){
		return values.filter((currentValue,currentIndex)=>typeof currentValue === type)
	}

	console.log(filterBy('number',1,2,"Rafif",true,2.3,false))

```

Jadi untuk penjelas kode di atas sendiri kita mengambil parameter ke satu sendiri menjadi sebuah patokan type sedangkan sisa dari parameter sendiri kita menjadi patokan untuk nilainya...








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








### 12.Callback

Function yang di kirimkan sebagai parameter pada function yang lain
( https://developer.mozilla.org/en-US/docs/Glossary/Callback_function )

Function yang di eksekusi setelah fungsi lain selesai di jalankan
( https://codeburst.io/javascript-what-the-heck-is-a-callback-aba4da2deced )

#### Syncronous Callback

```javascript

	function halo(nama){
		alert(`Halo ${nama}`)
	}

	function tampilkanPesan(callback){ // Higher Order Function
		let nama=prompt("Masukan Nama :")
		callback(nama)
	}

	tampilkanPesan(halo) // Mengisi parameter function tampilkanPesan dengan function halo

```

Sebenarnya tanpa kita sadari kita telah menggunakan `Callback` pada artikel `Higher Order Function`,jadi kesimpulannya `Higher Order Function` sendiri parameternya pasti mempunyai sebuah `Callback`

Kode di atas pula bisa kita ringkas kembali atau singkat kembali menggunakan `Arrow Function` menjadi seperti ini:

```javascript

	function tampilkanPesan(callback){ // Higher Order Function
		let nama=prompt("Masukan Nama :")
		callback(nama)
	}

	tampilkanPesan(nama=>alert(`Halo ${nama}`))

```
Nah..dan ini yang disebut dengan `Syncronous Callback`,jadi peng-eksekusian programnnya secara berurutan


#### Asyncronous Callback

Permasalahan di `Syncronous Callback` sendiri adalah peng-eksekusian programmnya yang berurutan,akan tetapi bagaimana jika ada sebuah function yang mempunyai jangka waktu running yang sangat lama,jadi mau tidak mau kita harus menunggu function itu selesai,perhatikan kode di bawah ini:

```javascript

		// Syncronous Callback

		let siswa=[
		{
		nama:"Rafif",
		umur:17,
		hobi:"ngoding"
		},
		{
		nama:"Ghozi",
		umur:17,
		hobi:"memancing"
		},
		{
		nama:"Whissper",
		umur:15,
		hobi:"lari"
		},
	]

	console.log("mulai")
	siswa.forEach(currentValue=>{
		for(let i=0;i<1000000;i++){
			let date=new Date()
		}
		console.log(currentValue.nama)
	})
	console.log("selesai")


```

Jadi untuk mengubah kode di atas menjadi `Asyncronous Callback` kita bisa menggunakan `Ajax`,jadi misalkan kita mempunyai file `JSON` yang berisi data `siswa` seperti ini:

```json
	// siswa.json
		[
		{
		"nama":"Rafif",
		"umur":17,
		"hobi":"ngoding"
		},
		{
		"nama":"Ghozi",
		"umur":17,
		"hobi":"memancing"
		},
		{
		"nama":"Whissper",
		"umur":15,
		"hobi":"lari"
		},
	]

```

```javascript

	function getDataSiswa(url,success,error){
		let xhr=new XMLHttpRequest()
		xhr.onreadystatechange=function(){
			if(this.readyState===4 && this.status===200){
				return success(JSON.parse(this.responseText))
			}
			if(this.status===404){
				error()
			}

		}
		xhr.open('GET',url)
		xhr.send()

	}

	console.log("mulai")
	getDataSiswa("siswa.json",result=>{
		result.forEach(currentValues=>console.log(currentValues.nama))
		},
		()=>{})
	console.log("selesai")

```

Sekarang dengan menggunakan `Ajax` sendiri kita tidak perlu menunggu fungsi `getDataSiswa` selesai di jalankan karena sudah `Asyncronous`,jadi sekarang urutan outputnya seperti ini:

```

mulai
selesai
Rafif
Ghozi
Whissper

```
Sekarang kita akan mencoba seperti di atas tapi menggunakan bantuan sebuah library yaitu `Jquery`,tapi sebelumnya kita harus memanggil `Jquery` tersebut,jika sudah coba perhatikan kode di bawah ini:

```javascript

	console.log('mulai')
	$.ajax({
		url:"siswa.json",
		data:{},
		dataType:"JSON",
		success:(result)=>{
			result.forEach(currentValue=>console.log(currentValue.nama))
		},
		error:e=>console.log(e.responseText)
	})
	console.log('selesai')

```


Perlu di perhatikan pula ketika kita membuat sebuah `Ajax` kita harus menyimpannya ke sebuah web server,jika tidak kita akan terkena `CORS(CrossOriginResourceSharing)`

Apa itu CORS? CORS memiliki kepanjangan cross-origin resource sharing yang bisa diartikan "berbagi resource dari asal yang berbeda". Agak aneh ya kalo ditranslate ke bahasa Indonesia.


Tapi intinya adalah bolehnya berbagi resource, misalnya endpoint web service / API endpoint supaya bisa diakses oleh origin yang berbeda. Sementara apa itu origin? origin bisa kita bayangkan sebagai asal dari request, yaitu domain request.


Misalnya, API berada di domain `http://aplikasi-saya.com/api/users`, kemudian ada aplikasi lain di domain `http://aplikasi-kamu.com` yang melakukan ajax request ke endpoint `aplikasi-saya.com` jika terjadi error CORS itu berarti `aplikasi-saya.com` tidak mengizinkan request dari domain `aplikasi-kamu.com`, umumnya secara default hanya mengizinkan request dari domain / origin yang sama yakni `aplikasi-saya.com`, inilah yang disebut dengan `SAME-ORIGIN policy` atau kebijakan yang hanya membolehkan request ke resource hanya dari domain yang sama.


Nah kalo begini yang salah siapa? hmm tidak ada yang salah sih, tapi apa yang harus dilakukan jika terjadi CORS begini? jika kamu punya akses ke server `aplikasi-saya.com` tentu kamu bisa melakukan konfigurasi supaya request bisa dilakukan oleh domain lain, atau menggunakan metode whitelist, yaitu kita konfigurasi supaya server `aplikasi-saya.com` mengizinkan dari origin / domain-domain tertentu yang kita daftarkan

Untuk lebih memahami penggunaan dari `Callback` sendiri di bawah ini ada sebuah program yang menampilkan daftar film yang di ambil menggunakan `Ajax` dari suatu `API`:


```html

	<!DOCTYPE html>
	<html lang="en">
	  <head>
	    <!-- Required meta tags -->
	    <meta charset="utf-8">
	    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

	    <!-- Bootstrap CSS -->
	    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">

	    <title>Belajar Javascript Advance</title>
	  </head>
	  <body>

	    <div class="container">
	      
	      <div class="row">
	        <div class="col-lg mt-5">
	        <h1>Nekode Movies</h1>

	        <div class="input-group mb-3">
	          <input type="text" class="form-control search-input" placeholder="Search Movies...">
	          <div class="input-group-append">
	            <button class="btn btn-secondary" type="button" id="search-button">Search</button>
	          </div>
	        </div>


	        </div>
	      </div>

	      <div class="row nekode-movies">
	        
	        
	      </div>


	    </div>



	    <!-- Modal -->
	    <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
	      <div class="modal-dialog modal-dialog-centered modal-lg" role="document">
	        <div class="modal-content">
	          <div class="modal-header">
	            <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
	            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
	              <span aria-hidden="true">&times;</span>
	            </button>
	          </div>
	          <div class="modal-body">
	           
	            


	          </div>
	          <div class="modal-footer">
	            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
	          </div>
	        </div>
	      </div>
	    </div>




	    <!-- Optional JavaScript -->
	    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
	    <script src="jquery-3.1.1.min.js"></script>
	    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>
	    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js" integrity="sha384-ChfqqxuZUCnJSK3+MXmPNIyE6ZbWh2IMqE241rYiqJxyMiZ6OW/JmZQ5stwEULTy" crossorigin="anonymous"></script>
	    <script type="text/javascript" src="script.js"></script>
	  </body>
	</html>

```

Dan untuk bagian javascript nya sendiri di sini saya menyediakan dua pilihan yaitu menggunakan `Jquery` dan `Vanilla Javascript/Javascript Murni`

```javascript
	
	// Vanilla Javascript

	function myFunc(key,success){
		let xhr=new XMLHttpRequest()
		xhr.onreadystatechange=function(){
			if(this.readyState===4 && this.status===200){
				success(JSON.parse(this.responseText))
			}
		}
		url=`http://www.omdbapi.com/?apikey=3a62a019${key}`
		xhr.open('get',url)
		xhr.send()
	}


	

	// Untuk bagian search
	document.querySelector('#search-button').addEventListener('click',function(){
		let search=document.querySelector('.search-input').value
		if(search !== ''){



	myFunc(`&s=${search}`,result=>{
		let movies=result.Search
		let str='';
		movies.forEach(currentValue=>{
		str+=card(currentValue)
  	})
		document.querySelector(".nekode-movies").innerHTML=str

		// Untuk bagian detail
		let modal_button=document.querySelectorAll('.modal-detail-button')	
		for(let x=0;x<modal_button.length;x++){
			modal_button[x].addEventListener('click',function(){
				myFunc(`&i=${this.dataset.imdbid}`,result=>{
				document.querySelector('.modal-body').innerHTML=detail(result)	
			  	})
			})
		}


	})



		}
	})
	


	function card(data){
		return `<div class="col-md-4">
          <div class="card" style="width: 18rem;">
            <img class="card-img-top" src="${data.Poster}" alt="Card image cap">
            <div class="card-body">
              <h5 class="card-title">${data.Title}</h5>
              <h6 class="card-subtitle mb-2 text-muted">${data.Year}</h6>
              <a href="#" class="btn btn-primary modal-detail-button" data-toggle="modal" data-target="#exampleModal" data-imdbid=${data.imdbID}>Show Details</a>
            </div>
          </div>
        </div>
      </div>`
	}

	function detail(data){
		return `<div class="container-fluid">
              <div class="row">
                <div class="col-md-3">
                  <img src="${data.Poster}" class="img-fluid">
                </div>
                <div class="col-md">
                  <ul class="list-group">
                    <li class="list-group-item"><h4>${data.Title}</h4></li>
                    <li class="list-group-item"><strong>Director :</strong>${data.Director}</li>
                    <li class="list-group-item"><strong>Actors :</strong>${data.Actors}</li>
                    <li class="list-group-item"><strong>Writer :</strong>${data.Writer}</li>
                    <li class="list-group-item"><strong>Plot :</strong>${data.Plot}</li>
                  </ul>
                </div>
              </div>
            </div>`
	}

``` 
Perlu di perhatikan pula saat button `Detail` di klik pada `Vanilla Javascript` sendiri untuk bisa menangkap buttonnya kita melakukan `Looping` karena button dari `Detail` sendiri banyak,Tidak seperti `Jquery` kita langsung saja seperti di bawah ini:

```javascript

		// Jquery

		$('#search-button').on('click',function(){

		$.ajax({
		url:`http://www.omdbapi.com/?apikey=3a62a019&s=${$('.search-input').val()}`,
		data:{},
		dataType:'JSON',
		success:result=>{
			let movies=result.Search
			let str=''
			movies.forEach(currentValue=>str+=card(currentValue))
			$('.nekode-movies').html(str)

			$('.modal-detail-button').on('click',function(){

				$.ajax({
					url:`http://www.omdbapi.com/?apikey=3a62a019&i=${$(this).data('imdbid')}`,
					data:{},
					dataType:'JSON',
					success:result=>{
						$('.modal-body').html(detail(result))
					},
					error:err=>console.log(err.responseText)
				})

			})

		},
		error:err=>console.log(err.responseText)
	})



	})
	



	function card(data){
		return `<div class="col-md-4">
          <div class="card" style="width: 18rem;">
            <img class="card-img-top" src="${data.Poster}" alt="Card image cap">
            <div class="card-body">
              <h5 class="card-title">${data.Title}</h5>
              <h6 class="card-subtitle mb-2 text-muted">${data.Year}</h6>
              <a href="#" class="btn btn-primary modal-detail-button" data-toggle="modal" data-target="#exampleModal" data-imdbid=${data.imdbID}>Show Details</a>
            </div>
          </div>
        </div>
      </div>`
	}

	function detail(data){
		return `<div class="container-fluid">
              <div class="row">
                <div class="col-md-3">
                  <img src="${data.Poster}" class="img-fluid">
                </div>
                <div class="col-md">
                  <ul class="list-group">
                    <li class="list-group-item"><h4>${data.Title}</h4></li>
                    <li class="list-group-item"><strong>Director :</strong>${data.Director}</li>
                    <li class="list-group-item"><strong>Actors :</strong>${data.Actors}</li>
                    <li class="list-group-item"><strong>Writer :</strong>${data.Writer}</li>
                    <li class="list-group-item"><strong>Plot :</strong>${data.Plot}</li>
                  </ul>
                </div>
              </div>
            </div>`
	}

```








### 13.Promise

Promise adalah salah fitur terbaru dari `ES6`. Jika anda sebelumnya sudah pernah menggunakan .then maka anda sudah menggunakan promise. Mari kita mulai dari analogi sederhana. `Anda janjian ketemuan dengan salah satu kolega anda, tiba-tiba kolega tersebut bertanya anda sudah dimana ? Ada beberapa kemungkinan jawaban disini : dalam perjalanan, sudah sampai atau janjinya di batalkan`.

Dalam dunia promise analogi di atas juga sama, ketika melakukan request asynchronous seperti `Ajax`, maka ada 3 kemungkinan state/keadaan :

##### `- Pending ( Sedang Dalam Proses )`
##### `- Fullfilled ( Berhasil )`
##### `- Rejected ( Gagal )`

Lalu bagaimana implementasinya dalam javascript ? Untuk sekarang ingat saja bahwa promise itu adalah object. Object yang merepresentasikan state/keadaan diatas.

#### Callback VS Promise

Promise umumnya digunakan sebagai alternative callback. Salah satu tantangan di callback adalah callback hell. Disebut neraka ketika ada callback didalam callback didalam callback lagi dan di dalam callback lagi. Problemnya adalah kode sulit dibaca dan penanganan error nya juga menjadi sulit. Disaat seperti ini maka promise menjadi solusi.

Sebelum mendalami promise sebaiknya pahamilah terlebih dahulu konsep callback. Promise bukan untuk menggantikan callback, karena promise akan selalu berjalan asynchronous sedangkan callback bisa digunakan untuk synchronous maupun asynchronous. Benefit utama dari promise adalah membuat code lebih readable dan manajemen error yang lebih baik.

Beberapa hal penting perbedaan callback dan promise adalah :

##### - `Callback` adalah function sedangkan `Promise` adalah object
##### - `Callback` di kirim melalui parameter,sedangkan `Promise` mengembalikan object
##### - `Callback` di gunakan untuk menghandle success dan failure,sedangkan `Promise` tidak
##### - `Callback` dapat di gunakan untuk beberapa event sekaligus,sedangkan `Promise` hanya untuk satu event

Untuk membuat promise cukup dengan memanggil constructor nya :

```javascript

	let janjian=new Promise()
	console.log(janjian)

```

Sampai disini output dari code atas adalah Promise `{ <pending> }`

Lalu bagaimana untuk mengatur state `Fullfilled` dan `Reject` ?
Untuk state ini gunakan salah satu listener, `resolve()` atau `reject()`

```javascript

	let janji=true
	let janjian=new Promise((resolve,reject)=>{
		// Salah satu dari 2 callback berikut
		// resolve('Berhasil')
		// reject(new Error('Janji di batalkan'))
		if(janji){
			resolve("Janji di tepati")
		}else{
			reject(new Error("Janji di batalkan"))
		}
	})


	janjian.
		then(response=>console.log("Berhasil "+response)).// Parameter response dari Resolve yang di atas
		catch(response=>console.log("Gagal "+response)) // Parameter response dari Reject yang di atas

```
Output kode di atas pula akan seperti ini `Promise {<resolved>: "Berhasil"}`

jadi singkatnya `Promise` sendiri mempunyai 3 `Callback` yaitu resolve,reject,finally

Dan aksi yang di gunakannya `then` dan `catch`,jika `then` sendiri untuk `resolve` yaitu berhasil dan `catch` sendiri untuk `reject` yaitu jika gagal

Dan untuk lebih kasus yang sedikit nyata kita akan menggunakan fungsi `Asyncronous` yaitu `setTimeout()`

```javascript

	let janji=true
	let janjian=new Promise((resolve,reject)=>{

		if(janji){
			setTimeout(()=>{
				resolve('Di tepati setelah berberapa waktu')
			},2000)
		}else{
			setTimeout(()=>{
				reject('Tidak di tepati setelah berberapa waktu')
			},2000)
		}

	})

	console.log('mulai')

	console.log(janjian. // Untuk baris ini pas promise nya dalam proses (Pending)
		then(()=>console.log(janjian) // Untuk baris ini pas promise nya selesai di jalankan
			))

	//Kalau kita menulisnnya seperti ini pendingnya tidak terlihat jadi agar kita mengetahui sedang pending kita melakukan seperti yang di atas
	// janjian.
	// 	then(response=>console.log("Berhasil "+response)).
	// 	catch(response=>console.log("Gagal "+response)) 

	console.log('selesai')


```

Dan untuk state `finally` sendiri adalah ketika kita selesai pending maka state ini yang terlebih dahulu di eksekusi dan kemudian ke bagian selanjutnnya `then` atau `catch`

```javascript



	let janji=true
	let janjian=new Promise((resolve,reject)=>{

		if(janji){
			setTimeout(()=>{
				resolve('Di tepati setelah berberapa waktu')
			},2000)
		}else{
			setTimeout(()=>{
				reject('Tidak di tepati setelah berberapa waktu')
			},2000)
		}

	})

	console.log('mulai')

	janjian.
		finally(response=>console.log("Selesai menunggu")).// finally terlebih dahulu kemudian ke then
		then(response=>console.log("Berhasil "+response)).// karena variable janji di atas true
		catch(response=>console.log("Gagal "+response)) 

	console.log('selesai')



```

#### Promise.all()

Method ini sendiri gunakan ketika kita melakukan 2 request dan ingin menggabungkannya kita bisa menggunakan method `Promise.all()` dan perlu di perhatikan untuk parameternya kita bungkus ke sebuah `Array`,misalkan kita mempunyai 2 request ke `API` yang berbeda,kita simulasikan seperti contoh di bawah ini:

```javascript

	let film=new Promise((resolve,reject)=>{
		setTimeout(()=>{
		resolve([{
			nama:"Avanger",
			sutradara:"Rafif",
			thnRilis:2018
		}])
		},2000)
	})

	let cuaca=new Promise((resolve,reject)=>{
		setTimeout(()=>{
			resolve([{
				kota:"subang",
				temp:28,
				kondisi:"Cerah Berawan"
			}])
		},500)	
	})

	// Jika Tidak Menggunakan Promise.all()
	
	// film.then(response=>console.log(response))
	// cuaca.then(response=>console.log(response))

	// Menggunakan Promise.all()
	Promise.all([film,cuaca]).then(response=>{//parameter berbentuk array
	let [film,cuaca]=[...response]
	console.log(film)
	console.log(cuaca)
	}) // Karena bentuknya array kita bisa menggunakan spread operator

```

Jadi kesimpulannya dengan menggunakan `Promise` sendiri kita bisa menyelesaikan permasalah yaitu `Callback Hell`








### 14.Fetch

Sebuah method pada `API` javascript untuk mengambil `Resources` dari jaringan,dan mengembalikan `Promise` yang selesai `(Fullfilled)` ketika ada `response` yang tersedia

( https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch )

Mari kita coba request ke API public.

```javascript

	fetch('http://www.omdbapi.com/?apikey=3a62a019&s=harry potter').
		then(response=>response.json()). // # 1
		then(user=>console.log(response.Search)) // # 2

```

##### Tapi kenapa method `.then` di panggil 2 kali ??

Hal ini sering membuat bingung, apalagi bagi yang pertama kali mencoba `fetch`.

`1.Response fetch pada #1 hasilnya adalah object Response, untuk lebih detailnya adan bisa lihat disini. Untuk mendapat response dalam bentuk json() maka digunakan method Body.json()`

`2.Hasil dari method Body.json() dibaca pada #2. Selain json kita juga menerima respon dalam format plain text menggunakan method Body.text()`

Agar tidak pusing sebenarnya kode di atas pula sama seperti ini:

```javascript

	fetch('http://www.omdbapi.com/?apikey=3a62a019&s=harry potter').
	then(response=>response.json()
		.then(user=>console.log(response.Search))
		)

```

Jadi jika kita lihat kode di atas pula dia mempunyai `then` yang di dalamnya `then` lagi,tergantung teman-teman dalam memahami kode di atas lebih di mengerti yang mana....

#### Promise Chaining

Seperti namanya promise chaining berarti promise berantai. Berikut contoh kasus untuk menampilkan post dengan alur seperti berikut :

##### - request post
##### - request author berdasarkan Id post
##### - request comment berdasarkan Id post
##### - tampilkan hasil

dalam bentuk pseude-code kira-kira seperti ini :

```javascript

	getPost().
		then(getAuthor).
		then(getComment).
		then(showResult)

```

Berikut contoh Source codenya:

```javascript

	
	const getPost = () => fetch('https://jsonplaceholder.typicode.com/posts/1')
	const getAuthor = (id) => fetch('https://jsonplaceholder.typicode.com/users/' + id)
	const getComment = (id) => fetch('https://jsonplaceholder.typicode.com/users/' + id)

	getPost() // #1.fetch post
	.then(postResponse => postResponse.json()) // #2. get & return post json 
	.then(postResponse => getAuthor(postResponse.id) // #3. fetch author
	  .then(authorResponse => authorResponse.json()  // #4 get & return author json
	    .then(authorResponse => getComment(postResponse.id) // #5 fetch comment
	      .then(commentResponse => commentResponse.json()) // #6 get & return comment json
	      .then(commentResponse => {  // #7 time to combine all results
	          return ({postResponse,authorResponse,commentResponse}) // #8 combine & return all reponses
	        })
	    )
	  )
	  .then(results => { // #9 read all responses
	    console.log(results.postResponse)
	    console.log(results.authorResponse)
	    console.log(results.commentResponse)

	  }) 
	)
	.catch(error => console.log(error)) //# 10 error handling



```

Jika dirasa kode diatas sulit dibaca, mari kita per simple lagi dengan cara seperti berikut :

```javascript

	const getPost = () => fetch('https://jsonplaceholder.typicode.com/posts/1')
	const getAuthor = (id) => fetch('https://jsonplaceholder.typicode.com/users/' + id)
	const getComment = (id) => fetch('https://jsonplaceholder.typicode.com/users/' + id)

	var a = getPost().then(res => res.json()) // #1 get post
	var b = a.then(res => getAuthor(res.id)).then(res => res.json()) // #2 get author
	var c = a.then(res => getComment(res.id)).then(res => res.json()) //#3 get comment
	
	Promise.all([a,b,c]).then(results => {
	  console.log(results[0])
	  console.log(results[1])
	  console.log(results[2])
	})
	 

```

#### Promise.all

Promise.all sedikit lebih mudah, Cara kerjanya adalah menunggu hingga semua eksekusi promise selesai dan menghasil output dalam bentuk array. Sebagai contoh untuk kasus diatas menggunakan dengan Promise.all

```javascript

	const getPost = () => fetch('https://jsonplaceholder.typicode.com/posts/1')
	const getAuthor = (id) => fetch('https://jsonplaceholder.typicode.com/users/' + id)
	const getComment = (id) => fetch('https://jsonplaceholder.typicode.com/users/' + id)

	const a=getPost().then(response=>response.json())
	const b=a.then(response=>getAuthor(response.id)).then(response=>response.json())
	const c=a.then(response=>getComment(response.id)).then(response=>response.json())

	Promise.all([a,b,c]).
	then(results=>{
		console.log(results[0])
		console.log(results[1])
		console.log(results[2])
	})

```

#### Promise In Looping

Salah satu kasus menarik di promise adalah mengeksekusi beberapa promise dalam looping sesuai urutan. Untuk memproses promise dalam looping, gunakan array.map dan Promise.all

```javascript

	let doFetch=url=>fetch(url).then(response=>response.json())

	let urls =[
			  'https://jsonplaceholder.typicode.com/posts/1',
			  'https://jsonplaceholder.typicode.com/posts/2',
			  'https://jsonplaceholder.typicode.com/posts/3',
			  'https://jsonplaceholder.typicode.com/posts/4',
			]
	let promise=[]
	urls.map(currentValue=>{
		promise.push(doFetch(currentValue))
	})

	Promise.all(promise).
	then(results=>{
		console.log(results[0])
		console.log(results[1])
		console.log(results[2])
		console.log(results[3])
	})

```

#### Promise.race

Berbeda cara eksekusi promise sebelumnya.`Promice.race` hanya menghasilkan promise yang lebih dulu selesai. Sebagai contoh kasus mari kita ambil contoh olahraga kegemaran kita semua yaitu balap karung.

```javascript

	let peserta1 = new Promise(resolve => setTimeout(resolve, 30, 'Peserta 1.'))
	let peserta2 = new Promise(resolve => setTimeout(resolve, 20, 'Peserta 2.'))
	let peserta3 = new Promise(reject => setTimeout(reject, 50, 'Peserta 3.'))
	let peserta4 = new Promise(resolve => setTimeout(resolve, 100, 'Peserta 4.'))
	let peserta5 = new Promise(resolve => setTimeout(resolve, 90, 'Peserta 5.'))

	Promise.race([peserta1, peserta2, peserta3, peserta4, peserta5])
    .then(val => console.log('Balapan selesai,Pemenangnya adalah:', val))
    .catch(err => console.log('Balapan dihentikan karena : ', err));



```

Tapi bagaimana kalau satu peserta terjatuh ? ( ada promise yang reject )

```javascript

	let peserta1 = new Promise(resolve => setTimeout(resolve, 30, 'Peserta 1'))
	let peserta2 = new Promise((resolve,reject) => setTimeout(reject, 20, 'Peserta 2'))
	let peserta3 = new Promise(resolve => setTimeout(resolve, 50, 'Peserta 3'))
	let peserta4 = new Promise(resolve => setTimeout(resolve, 100, 'Peserta 4'))
	let peserta5 = new Promise(resolve => setTimeout(resolve, 90, 'Peserta 5'))
	 
	Promise.race([peserta1, peserta2, peserta3, peserta4, peserta5])
	    .then(val => console.log('Balapan selesai,Pemenangnya adalah:', val))
	    .catch(err => console.log('Balapan dihentikan karena : ', err));

```

`Output` : Balapan dihentikan karena : Peserta 2

Seharusnya jika peserta 2 terjatuh maka pemenang adalah peserta 1, tapi karena jiwa mereka ini sangat nasionalis terpaksa balapan dihentikan.

Tapi karena kebetulan ini adalah pertandingan piala dunia balap karung, peraturan balapnya di ubah. Pertandingan tetap dilanjutkan meskipun ada peserta yang terjatuh.

Untuk ini method promise di extend untuk mendeteksi promise yang reject.

```javascript

	Promise.seriousRace = function(promises) {
	  let indexPromises = promises.map((p, index) => p.catch(() => {throw index})) // Memeriksa apakah data valid
	  return Promise.race(indexPromises).catch(index => {
	    let p = promises.splice(index, 1)[0] // Untuk menghapus yang reject
	    p.catch(e => console.log( e +  ' terjatuh,ahh sudahlah lanjutkan saja'))
	    return Promise.seriousRace(promises)
	  })
	}

	let peserta1 = new Promise(resolve => setTimeout(resolve, 30, 'Peserta 1'))
	let peserta2 = new Promise((resolve,reject) => setTimeout(reject, 20, 'Peserta 2'))
	let peserta3 = new Promise(resolve => setTimeout(resolve, 50, 'Peserta 3'))
	let peserta4 = new Promise(resolve => setTimeout(resolve, 100, 'Peserta 4'))
	let peserta5 = new Promise(resolve => setTimeout(resolve, 90, 'Peserta 5'))
	 
	Promise.seriousRace([peserta1, peserta2, peserta3, peserta4, peserta5])
	  .then(val => console.log('Balapan selesai,Pemenangnya adalah:', val))
	  .catch(err => console.log('Balapan dihentikan karena : ', err))


```

`Output` :
Peserta 2 terjatuh,ahh sudahlah lanjutkan saja
Balapan selesai,Pemenangnya adalah: Peserta 1

Sumber:https://medium.com/coderupa/panduan-komplit-asynchronous-programming-pada-javascript-part-3-promise-819ce5d8b3c









### 15.Async,Await

Async/await adalah fitur yang hadir sejak ES2017. Fitur ini mempermudah kita dalam menangani proses asynchronous. Untuk memahami async/await sebaiknya anda harus memahami promise terlebih dahulu.

Ada 2 kata kunci disini yaitu async dan await, mari kita lihat contohnya :

```javascript

	async function hello(){
	result=await doAsync()
	console.log(result)
	}

```
Keterangan :

`async` → mengubah function menjadi asynchronous
`await` → menunda eksekusi hingga proses asynchronous selesai, dari kode di atas berarti console.log(result)

tidak akan di eksekusi sebelum prose doAsync( ) selesai. await juga bisa digunakan berkali-kali di dalam function

Sekarang mari kita coba untuk fetch dengan promise dan async/await

```javascript

		
	/* Promise */
	const endpoint ='https://jsonplaceholder.typicode.com/users/'

	function fetchWithPromise(id){
	  fetch(endpoint + id)
	  .then(response=>response.json())
	  .then(user=>console.log(user))
	}

	/* Async/Await */
	async function fetchWithAsyncAwait(id)  {
	  let response = await fetch(endpoint + id)
	  response = await response.json()
	  console.log(response)
	}

	fetchWithPromise(1) 
	fetchWithAsyncAwait(1)

```

Output nya sama tapi async/await lebih mudah dibaca. Lalu bagaimana dengan manajemen error nya ?

#### Async,Await Error Handling

Error handling pada async/await menggunakan `try…catch`

```javascript

	async function fetchWithAsyncAwait (id)  {
	  try {
	    let response = await fetch(endpoint + id)
	    response = await response.json()
	    console.log(response)
	  } catch (error) {
	    console.log('opps' + error)
	  }
	}

```

#### Async,Await Pattern

Ada beberapa pattern untuk membuat async/await :

```javascript

		// 1. Anonymous Async Function
	let main = (async function() {
	  let value = await doAsync();
	})();


	// 2. Async Function Declaration
	let main = async function() {
	  let value = await doAsync();
	};

	//3. Async Function Assignment
	let main = async () => {
	  let value = await doAsync();
	};

	//4. Async Function as Argument
	document.body.addEventListener('click', async function() {
	  let value = await doAsync();
	});


	//5 Object & Class Methods
	let obj = {
	  async method() {
	    let value = await doAsync();
	  }
	};

	class MyClass {
	  async myMethod() {
	    let value = await doAsync();
	  }
	}

```

#### Serial & Paralel

Pada saat mengeksekusi beberapa proses asynchronous, ada kalanya kita harus memilih eksekusi secara serial atau parallel. Serial biasanya digunakan jika kita ingin mengeksekusi proses asynchronous secara berurutan. Sedangkan paralel jika ingin di eksekusi secara bersamaan, dalam hal ini urutan tidak menjadi prioritas tapi hasil dan performa.

```javascript

	const firstPromise= () => (new Promise((resolve,reject) => {
	  setTimeout(() =>{ resolve('first Promise')},1000) 
	}))

	const secondPromise = () => ( new Promise((resolve,reject) =>{
	  setTimeout(() =>{ resolve('second Promise')},1000) 
	}))

	const thirdPromise = () => ( new Promise((resolve,reject) =>{
	  setTimeout(() =>{ resolve('third Promise')},1000) 
	}))
	 
	async function asyncParalel() {
	  let a =firstPromise()
	  let b= secondPromise()
	  let c= thirdPromise()
	  console.log('done')
	}
	 
	async function asyncSerial() {
	   let a= await firstPromise()
	   let b= await secondPromise()
	   let c= await thirdPromise()
	   console.log('done')
	}

```

#### Promise.all & Promise.race Dalam Async,Await

Salah satu favorite saya di promise adalah promise.all dan promise.race. Karena async/await di desain untuk bekerja dengan promise, maka dengan mudah bisa kita gunakan pada async/await, contohnya :

```javascript

	// 1. Anonymous Async Function
	let main = (async function() {
	  let value = await doAsync();
	})();


	// 2. Async Function Declaration
	let main = async function() {
	  let value = await doAsync();
	};

	//3. Async Function Assignment
	let main = async () => {
	  let value = await doAsync();
	};

	//4. Async Function as Argument
	document.body.addEventListener('click', async function() {
	  let value = await doAsync();
	});


	//5 Object & Class Methods
	let obj = {
	  async method() {
	    let value = await doAsync();
	  }
	};

	class MyClass {
	  async myMethod() {
	    let value = await doAsync();
	  }
	}


```