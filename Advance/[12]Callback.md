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