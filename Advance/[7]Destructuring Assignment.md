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