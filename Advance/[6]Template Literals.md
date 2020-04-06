### 6.Template Literals / Template String

Salah satu yang sering kita lakukan saat membuat aplikasi adalah menggabungkan string dengan hasil ekspresi, misalnya untuk menampilkan pesan error atau informasi. Misalnya menulis halaman "Selamat datang, Rafif Faisal Ghozi", di mana kata "Rafif Faisal Ghozi" diambil dari data pengguna yang login ke aplikasi. Pada javascript ES5, kita menulisnya seperti ini:

```javascript

var nama = "Rafif Faisal Ghozi";

var pesan = "Selamat datang," + nama + "!";

console.log(pesan); // "Selamat datang, Rafif Faisal Ghozi!"

```

Nah, sekarang kita bisa menggunakan template literal ini sehingga kita bisa mengurangi penggunaan simbol operator tambah. Kita bisa menulis kalimat yang sama tanpa menggunakan simbol operator tambah, hanya saja kita harus menggunakan backtick ```(`)```, lokasi tombolnya pada keyboard ada di sebelah kiri angka 1. Contohnya:

```javascript

var nama = "Rafif Faisal Ghozi";

var pesan = `Selamat datang, ${nama}!`;

console.log(pesan); // "Selamat datang, Rafif Faisal Ghozi!"

```

kalau ingin ada backtick di dalam template ini, bisa di-escape dengan backslash..

```javascript

`\`` === '`' // --> true

```

Kelebihan dari `Template Literals` sendiri sebagai berikut:

##### - Multi Line

Dengan menggunakan `Template Literals` sendiri kita tidak perlu khawatir akan perpindahan baris,jika biasanya kita menuliskan seperti ini:

```javascript

console.log('string text line 1\n' +
'string text line 2');
// "string text line 1
// string text line 2"


```

Dengan `Template Literals`

```javascript

console.log(`string text line 1
string text line 2`);
// "string text line 1
// string text line 2"


```

#### - Expression Interpolation

Jika biasa jika kita membuat expresi seperti ini:

```javascript

let a = 5;
let b = 10;
console.log('Fifteen is ' + (a + b) + ' and\nnot ' + (2 * a + b) + '.');
// "Fifteen is 15 and
// not 20."

```

Dengan menggunakan `Template Literal` sendiri jadi seperti ini:

```javascript

let a = 5;
let b = 10;
console.log(`Fifteen is ${a + b} and
not ${2 * a + b}.`);
// "Fifteen is 15 and
// not 20."

```

#### - Nesting Templates

Dalam kebanyakan kasus sendiri,template bersarang sangat mudah di gunakan dan mudah untuk di manipulasi dengan `Template Literal`,jadi kita bisa melakukan operator `Ternary` di dalam `Template Literal` sendiri,Perhatikan contoh di bawah ini:

```javascript


	const student = {
	  name: 'Kristine',
	  food: 'Chipotle',
	  city: 'Scottsdale'
	};

	
	const html = `
	<div>
	  <h1>Name: ${student.name}</h1>
	  <h3>Location: ${student.city}</h3>
	  ${student.food ? `<h3>Food: ${student.food}</h3>` : ''}
	</div>
	`


```

#### - Tagged Template Literals

Bentuk yang lebih kompleks dari `Template Literals`,Memungkinkan kita untuk membaca template literals melalui sebuah function(MDN Web Docs)

Jadi `Tagged Template Literals` sendiri adalah bentuk lanjutan atau bisa kita sebut advance dari `Template Literals`,Dengan menggunkan `Tagged Template Literals` sendiri kita jadi bisa mem-parsing sebuah string ke sebuah function

Dan untuk argument pertama pada functionnya nanti mengandung/berisi sebuah array of string,perhatikan contoh di bawah ini:

```javascript

	let nama="Rafif Faisal Ghozi"
	let umur=17

	function coba(string,...values){/* jika juga bisa menggunakan rest arguments untuk menggantikan nama dan umur,jika biasanya seperti ini:coba(string,nama,umur) kita bisa menggantinya seperti yang di atas*/
		//string[0]=Halo,nama saya
		//string[1]=,saya
		//string[2]=.tahun
		let str=""

		string.forEach((currentValue,currentIndex)=>{
			str+=`${currentValue}${values[currentIndex]||''}`
		})

		return str

		// return string.reduce((previousValue,currentValue,currentIndex)=>`${previousValue}${currentValue}${values[currentIndex]||''}`)

	}

	let output=coba `Halo,nama saya ${nama},saya ${umur}.tahun`

	console.log(output)

```

Dengan menggunakan `Tagged Template Literals` sendiri,kita jadi bisa memanipulasi lebih jauh lagi,untuk contoh perhatikan di bawah ini:

```javascript

	let nama="Rafif Faisal Ghozi"
	let umur=17
	let email="faisalghozi458@gmail.com"

	function highLight(string,...values){/* jika juga bisa menggunakan rest arguments untuk menggantikan nama dan umur,jika biasanya seperti ini:coba(string,nama,umur) kita bisa menggantinya seperti yang di atas*/
		//string[0]=Halo,nama saya
		//string[1]=,saya
		//string[2]=.tahun
		let str=""

		string.forEach((currentValue,currentIndex)=>{
			str+=`${currentValue}<span style="background-color:'salmon'">${values[currentIndex]||''}</span>`
		})

		return str

		// return string.reduce((previousValue,currentValue,currentIndex)=>`${previousValue}${currentValue}${values[currentIndex]||''}`)

	}

	let output=highLight `Halo,nama saya ${nama},saya ${umur}.tahun`

	document.body.innerHtml=output

```

#### Penggunaan Lain Dari Tagged Template Literals

##### - Escaping / Sanitize HTML Tags

`Tagged Template Literals` pula bisa kita gunakan untuk mem-filter sebuah string agar menjadi aman,Atau bisa kita sebut untuk menghindari serangan dari XSS(Cross-Site-Scripting),atau juga kita bisa untuk menghindari kata-kata kasar kita bisa mem-filternya

```javascript

	function sanitize(strings,...values){

	return DOMPurify.sanitize(aboutMe);

	}

	const name="petyr baelish"
	const aboutMe=`I love to do evil <img src="http://unsplash.it/100/100?random" onload="alert('I hacked you.Haha');">`

	const html=sanitize `
	<h3>${name}</h3>
	<p>${aboutMe}</p>
	`

```

##### - Translation & Intertionalization

Dengan `Tagged Template Literals` juga kita bisa melakukan yang namanya tranlation atau biasa kita lihat sepert google translate,contoh kode di bawah ini dengan menggunakan libraries lain kita bisa melakukan translate:

```javascript

	console.log(i18n`Hello ${ name }, you have ${ amount }:c in your bank account.`)
	// Hallo Steffen, Sie haben US$ 1,250.33 auf Ihrem Bankkonto.

```
https://github.com/skolmer/es2015-i18n-tag


##### - Styled Components

Sebenarnya contoh ini ketika kita menggunakan react

```javascript

	const Title = styled.h1`
	  font-size: 1.5em;
	  text-align: center;
	  color: palevioletred;
	`;


```
https://www.styled-components.com/docs/basics#getting-started

