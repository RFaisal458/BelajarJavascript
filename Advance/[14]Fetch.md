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