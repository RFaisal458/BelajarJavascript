### 9.Spread Operator

Memecah (expand / unpack) iterables menjadi single element
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)

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