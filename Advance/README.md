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

let siswa=siswa("Rafif Faisal Ghozi",17,10)

let siswa2=siswa("Whissper",15,120)

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

let siswa=new siswa("Rafif Faisal Ghozi",17,10)

let siswa2=new siswa("Whissper",15,120)


```

#### - OBJECT.CREATE()

object literal sendiri mempunyai problem/masalah yaitu kurang cocok untuk membuat object yang banyak

function declaration sendiri juga mempunyai problem/masalah,ketika ada property atau method yang tidak di pakai,property dan method tersebut tetap tersimpan kedalam memori,jadi kurang efektif...
tetapi untuk mengatasi hal tersebut kita bisa menggunakan bantuan dari object literal pada function declaration.Contoh:

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

let siswa=siswa("Rafif Faisal Ghozi",17,10)

let siswa2=siswa("Whissper",15,120)


```

dengan kode di atas kita telah melakukan sedikit perbaikan,jadi untuk method siswa.makan,siswa.main itu mengacu ke object literal dari methodSiswa dan object tersebut pula di simpan ke memori hanya satu kali,tidak seperti sebelumnnya...akan tetapi kekurangan dari kode di atas pula,ketika kita membuat perubahan seperti menambahkan,menghapus property atau method baru di methodSiswa mau tidak mau kita harus mendaftarkan/menginstasiasi property/object tersebut ke dalam function declaration siswa,jadi problem nya kita mengelola 2 object sekaligus,tetapi dengan menggunakannya fungsi/method bawaan dari javascript yaitu `Object.create()` kita tidak perlu mengkhawatirkan perubahan di method yang menjadi parameter dari `Object.create()` tersebut,jadi `Object.create()` pula hampir mirip dengan konsep turunan/inheritance di Class,dengan begini kita tidak perlu bekerja 2 kali pada object tersebut.Contoh:


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

let siswa=siswa("Rafif Faisal Ghozi",17,10)

let siswa2=siswa("Whissper",15,120)


```
