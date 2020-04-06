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


