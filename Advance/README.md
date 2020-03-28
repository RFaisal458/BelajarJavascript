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
