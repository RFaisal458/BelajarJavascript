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



