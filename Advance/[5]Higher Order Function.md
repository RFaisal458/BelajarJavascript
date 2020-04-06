### 5.Higher Order Function

Function yang beroperasi pada function yang lain.Baik itu di gunakan dalam argument,maupun sebagai return value(https://eloquentjavascript.net)

Pada dasarnya sendiri pada javascript sendiri function di sebut dengan `First Class Function` inti dari javascript sendiri adalah function,Dan di javascript pula function di perlakukan sebagai object

Javascript memperlakukan function sebagai object(sitepoint.com)

Jadi di javascript function itu bisa menjadi argument atau return value dari sebuah function,Coba perhatikan kode di bawah ini:

```javascript

	function kerjakanTugas(pelajaran,selesai){
	console.log("Mulai mengerjakan tugas ${matakuliah}...")
	selesai()
	}
	
	function selesai(){
	alert('Selesai mengerjakan tugas')
	}

	kerjakanTugas("B.Inggris",selesai)

```

Nah..jadi kode di atas kita menjadikan function `selesai` sendiri sebagai argument dari function `kerjakanTugas`,sekarang function `kerjakanTugas` sendiri bisa kita sebut dengan `HigherOrderFunction`,karena menerima argument dari sebuah function yaitu function `selesai`

Dan jika kita mempunyai function sebagai argument seperti function `selesai` sendiri,maka argument tersebut kita sebut dengan `Callback`,untuk contoh `HigherOrderFunction` yang mengembalikan nilai function bisa kita lihat di bawah ini:

```javascript

	function ucapkanSalam(waktu){
	return function(nama){
	console.log(`Selamat ${waktu},Semoga harimu menyenangkan ${nama}`)
	}	
	}

	let selamatPagi=ucapkanSalam("pagi")
	selamatPagi("Rafif Faisal Ghozi")

```

Terus apa sih fungsi dari `HigherOrderFunction` ??jawabannya banyak alasannya salah satunya untuk membuat yang namanya `Abtraksi`

Agar kode yang kita buat itu lebih sederhana atau bisa lebih simple,karena sebenarnya dengan menggunakan function kita menyembunyikan kerumitan

Semakin besar sebuah program,Semakin tinggi kompleksitasnya,semakin membingungkan programmernya(eloquentjavascript.net)

Ada dua cara untuk merancang sebuah software:Cara pertama adalah untuk membuat programmnya se-sederhana mungkin sehingga jelas-jelas tidak ada kekurangannya.dan cara lainnya adalah untuk membuat programnya se-komplek mungkin sehingga tidak ada kekurangan yang jelas(C.A.R.Hoare,1980 ACM Turing Award Lecture)

```javascript

	function repeatLog(n){
	for(let i=0;i<n;i++){
	console.log(i)
	}
	}
	repeatLog(10)

```

Jadi dengan menggunakan function sendiri tidak hanya membuat perulangan di atas menjadi dinamis tetapi lebih sederhana dan mudah untuk di panggil,Atau jika kita ingin mengubah aksinya tidak ingin `console.log()`,coba perhatikan kode di bawah ini:

```javascript

	function repeat(n,action){
	for(let i=0;i<n;i++){
	action(i)
	}		

	}
	
	repeat(10,console.log)
	repeat(20,alert)

```

Dengan kita sering menggunakan membuat function kita akan mendekati yang namanya `Functional Programming`

#### Contoh Higher Order Function

Sebelum mulai, diketahui kita memiliki array yang akan melakukan fungsi-fungsi higher-order ini.

```javascript

var source = [1,2,3,4,5]

```


##### -Array.prototype.map()

Looping pada semua elemen array, dan menjalankan operasi pada masing-masing elemen array. Hasilnya adalah array dengan panjang (length) yang sama namun isinya berupa hasil dari operasi pada masing-masing elemen array yang bersesuaian.

Contoh:

```javascript

var dikaliDua = source.map(function(currentValue, currentIndex){
   return currentValue * 2;
});

console.log(dikaliDua); // [2, 4, 6, 8, 10]

```

##### -Array.prototype.filter()

Looping pada semua elemen array, setiap elemen yang memenuhi kondisi akan dimasukkan ke dalam array hasil fungsi filter, array sumber akan tetap utuh.

Contoh:

```javascript

var filterGanjil = source.filter(function(currentValue, currentIndex){
   return currentValue % 2 === 1;
});

console.log(filterGanjil); // [1, 3, 5]

```

##### -Array.prototype.reduce()

Looping pada semua elemen array, dan menjalankan operasi pada elemen array. Hasil operasi pada elemen ke-i, akan dijadikan parameter untuk operasi pada elemen berikutnya (i+1), sehingga hasil operasi reduce adalah akumulasi operasi pada semua elemen, bukan array. Pendeknya, value yang tadinya banyak (array) menjadi satu saja.

Contoh:

```javascript

var ditotalin = source.reduce(function(previousValue, currentValue, currentIndex){
   return previousValue + currentValue;
});

console.log(ditotalin); // 15

```

Untuk reduce, bisa ditambahkan parameter kedua yaitu initial value sebagai nilai permulaan sebelum reduce dieksekusi.

Contoh:

```javascript

var ditotalin = source.reduce(function(previousValue, currentValue, currentIndex){
   return previousValue + currentValue;
}, 5);

console.log(ditotalin); // 20

```

##### -Array.prototype.forEach()

Looping pada semua elemen array, dan menjalankan operasi yang kita berikan.

Contoh:

```javascript

source.forEach(function(currentValue, currentIndex){
   console.log("index", currentIndex, "isinya", currentValue);
});

// index 0 isinya 1
// index 1 isinya 2
// index 2 isinya 3
// index 3 isinya 4
// index 4 isinya 5

```

##### -Array.prototype.reduceRight()

Sama seperti reduce, hanya saja dilakukan mulai dari elemen terakhir.

Contoh:

```javascript

var ditotalinDariKanan = source.reduceRight(function(previousValue, currentValue, currentIndex){
   return previousValue + currentValue;
});

console.log(ditotalinDariKanan); // 15

```

Sama seperti reduce, reduceRight juga bisa ditambahkan parameter kedua sebagai initial value.


Nah, bagaimana kalau mau digabung? Contohnya, setelah difilter, ingin dilakukan map. Caranya adalah dengan method/function chaining, caranya seperti ini:

```javascript

 var filterGanjilLaluKaliDua = source
   .filter(function(currentValue, currentIndex){
      return currentValue % 2 === 1;
   })
   .map(function(currentValue, currentIndex){
      return currentValue * 2;
   });

console.log(filterGanjilLaluKaliDua); // [2, 6, 10]

```

Tapi ingat, chaining di atas bisa dilakukan karena hasil dari filter adalah array, jadi masih memiliki method map. Kalau awalnya, misalnya, di­-reduce, hasilnya bukanlah array sehingga tidak memiliki method map.

Contoh kasus dari implementasi fungsi-fungsi di atas:

```html

<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>

<h3>My Videos</h3>

<ul>
    <li data-duration="15:27">Teknik Pomodoro</li>
    <li data-duration="11:18">JAVASCRIPT LANJUTAN | Higher Order Functions</li>
    <li data-duration="21:40">JAVASCRIPT LANJUTAN | This Pada Arrow Function</li>
    <li data-duration="19:38">Website Penipu</li>
    <li data-duration="12:10">JAVASCRIPT LANJUTAN | Arrow Function</li>
    <li data-duration="20:43">JAVASCRIPT LANJUTAN | Closure</li>
    <li data-duration="14:30">#TANYAPADIKA EP005</li>
    <li data-duration="26:38">JAVASCRIPT LANJUTAN | Execution Context</li>
    <li data-duration="17:33">JAVASCRIPT LANJUTAN | Prototype</li>
    <li data-duration="10:39">JAVASCRIPT LANJUTAN | Object.create()</li>
    <li data-duration="17:31">JAVASCRIPT LANJUTAN | Object (Revisited)</li>
    <li data-duration="14:25">5 Tips Bertanya Ketika Error</li>
</ul>

<h3>My Playlist</h3>

    <ol>
        <li>
            <h4>Javascript Lanjutan</h4>
            <p>Jumlah Video : <span class="jumlah-video"></span></p>
            <p>Total Durasi : <span class="total-durasi"></span></p>
        </li>
    </ol>


<script type="text/javascript" src="script.js"></script>
</body>
</html>

```

```javascript

//Ambil Semua Element Video
let elVideo=Array.from(document.querySelectorAll("[data-duration]"))

//Pilih Hanya Yang 'JAVASCRIPT LANJUTAN'
let javascriptLanjutan=elVideo.filter((currentValue,currentIndex)=>currentValue.textContent.includes('JAVASCRIPT LANJUTAN'))

//Ambil Durasi Masing-Masing Video
.map((currentValue,currentIndex)=>currentValue.dataset.duration)

//Ubah Durasi Menjadi Float,Ubah Menit Menjadi Menit
.map((currentValue,currentIndex)=>{
	//10:18 [10,18] split
	let parts=currentValue.split(":").map(item=>parseFloat(item))
	return (parts[0] * 60) + parts[1]
})

//Jumlahkan Semua Detik
.reduce((previousValue,currentValue)=>previousValue+currentValue)

//Ubah Formatnya Jam Menit Detik
let jam=Math.floor(javascriptLanjutan/3600)
javascriptLanjutan= javascriptLanjutan - jam * 3600 //Untuk mendapatkan sisa dari detik di atas 8292
let menit=Math.floor(javascriptLanjutan / 60)
let detik=javascriptLanjutan - menit * 60

//Simpan Ke DOM
document.querySelector(".total-durasi").textContent=`${jam} Jam,${menit} Menit,${detik} Detik`
document.querySelector(".jumlah-video").textContent=elVideo.filter((currentValue,currentIndex)=>currentValue.textContent.includes("JAVASCRIPT LANJUTAN")).length

```

#### Rumus Menghitung Satuan Waktu

untuk satuan waktu dapat kita gunakan tangga  

```
jam

      menit

                detik

```

pada tangga ini, turun 1 tangga dikali 60, sebaliknya naik 1 tangga dibagi 60

#### Pembahasan

dari pendahuluan sdh diberikan tangga, dan penjelasan jika turun 1 tangga dikali 60 dan jika naik 1 tangga dibagi 60

contoh soal,

2 menit = ... detik

dari menit diubah menjadi detik, lihat tangga dari menit ke detik turun 1 tangga artinya kita kali 60

2 menit = 2 x 60 detik

             = 120 detik

contoh soal ke-2

180 detik = ... menit

dari detik dirubah menjadi menit, lihat tangga dari detik ke menit naik 1 tangga artinya kita bagi 60

180 detik = 180 : 60 menit

                = 3 menit

Kesimpulan
mengubah menit menjadi detik dengan cara dikali 60



