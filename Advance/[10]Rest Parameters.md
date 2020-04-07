### 9.Rest Parameters

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

