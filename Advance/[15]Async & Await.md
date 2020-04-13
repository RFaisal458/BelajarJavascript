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