<h1 align="center">Laporan Praktikum Modul 7 <br>Struktur & array</h1>
<p align="center">Vincentius Pastica Gunawan - 103112430014</p>

## Dasar Teori
Struktur (_struct_) dan array adalah dua jenis struktur data yang sering digunakan dalam pemrograman untuk menyimpan dan mengelola data. _Struct_ memungkinkan pengelompokan beberapa variabel dengan tipe data berbeda dalam satu kesatuan, sehingga cocok untuk merepresentasikan objek dengan berbagai atribut, seperti data mahasiswa yang terdiri dari nama (_string_), umur (_integer_), dan IPK (_float_). Sementara itu, array adalah kumpulan elemen dengan tipe data yang sama yang disimpan dalam satu variabel dan diakses menggunakan indeks, seperti daftar angka atau daftar nama. Perbedaan utama antara keduanya terletak pada fleksibilitas tipe data—_struct_ dapat berisi berbagai tipe data, sedangkan array hanya dapat menyimpan satu tipe data tertentu. Dengan memahami dan menggunakan kedua struktur ini, pemrogram dapat mengelola data secara lebih efisien sesuai dengan kebutuhan program.
## Unguided

### Soal Latihan Modul 7

#### Soal 1

> Suatu lingkaran didefinisikan dengan koordinat titik pusat (𝑐𝑥, 𝑐𝑦) dengan radius 𝑟. Apabila diberikan dua buah lingkaran, maka tentukan posisi sebuah titik sembarang (𝑥, 𝑦) berdasarkan dua lingkaran tersebut. Gunakan tipe bentukan titik untuk menyimpan koordinat, dan tipe bentukan lingkaran untuk menyimpan titik pusat lingkaran dan radiusnya. Masukan terdiri dari beberapa tiga baris. Baris pertama dan kedua adalah koordinat titik pusat dan radius dari lingkaran 1 dan lingkaran 2, sedangkan baris ketiga adalah koordinat titik sembarang. Asumsi sumbu x dan y dari semua titik dan juga radius direpresentasikan dengan bilangan bulat. Keluaran berupa string yang menyatakan posisi titik "Titik di dalam lingkaran 1 dan 2", "Titik di dalam lingkaran 1", "Titik di dalam lingkaran 2", atau "Titik di luar lingkaran 1 dan 2".

| No  | Masukan                    | Keluaran                          |
| --- | -------------------------- | --------------------------------- |
| 1   | 1 1 5<br>8 8 4<br>2 2      | Titik di dalam lingkaran 1        |
| 2   | 1 2 3<br>4 5 6<br>7 8      | Titik di dalam lingkaran 2        |
| 3   | 5 10 15<br>-15 4 20<br>0 0 | Titik di dalam lingkaran 1 dan 2  |
| 4   | 1 1 5<br>8 8 4<br>15 20    | Titik di dalam lingkaran 1 dan 2  |


```go
package main

import (
	"fmt"
	"math"
)

type Titik struct {
	x, y int
}

type Lingkaran struct {
	pusat  Titik
	radius int
}

// Fungsi untuk menghitung jarak antara dua titik
func jarak(p, q Titik) float64 {
	return math.Sqrt(math.Pow(float64(p.x-q.x), 2) + math.Pow(float64(p.y-q.y), 2))
}

// Fungsi untuk mengecek apakah titik berada di dalam lingkaran
func didalam(c Lingkaran, p Titik) bool {
	return jarak(c.pusat, p) <= float64(c.radius)
}

// Fungsi untuk mengecek apakah dua lingkaran bersinggungan
func bersinggungan(l1, l2 Lingkaran) bool {
	d := jarak(l1.pusat, l2.pusat)
	sumRadius := float64(l1.radius + l2.radius)
	return d <= sumRadius && d >= math.Abs(float64(l1.radius-l2.radius))
}

func main() {
	var (
		cx1, cy1, r1 int
		cx2, cy2, r2 int
		x, y         int
	)

	fmt.Scan(&cx1, &cy1, &r1)
	fmt.Scan(&cx2, &cy2, &r2)
	fmt.Scan(&x, &y)

	// Membuat objek lingkaran dan titik
	lingkaran1 := Lingkaran{Titik{cx1, cy1}, r1}
	lingkaran2 := Lingkaran{Titik{cx2, cy2}, r2}
	titik := Titik{x, y}

	// Mengecek posisi titik
	didalam1 := didalam(lingkaran1, titik)
	didalam2 := didalam(lingkaran2, titik)
	salingBersinggungan := bersinggungan(lingkaran1, lingkaran2)

	// Menentukan keluaran
	if didalam1 && didalam2 {
		fmt.Println("Titik di dalam kedua lingkaran")
	} else if didalam1 {
		fmt.Println("Titik di dalam lingkaran 1")
	} else if didalam2 {
		fmt.Println("Titik di dalam lingkaran 2")
	} else {
		fmt.Println("Titik di luar kedua lingkaran")
	}

	if salingBersinggungan {
		fmt.Println("Lingkaran 1 dan Lingkaran 2 saling bersinggungan")
	} else {
		fmt.Println("Lingkaran 1 dan Lingkaran 2 tidak bersinggungan")
	}
}

```

Program ini bertujuan untuk menentukan apakah sebuah titik berada di dalam salah satu atau kedua lingkaran serta mengecek apakah dua lingkaran saling bersinggungan. Program dimulai dengan mendefinisikan dua struktur, yaitu `Titik` untuk merepresentasikan koordinat (x, y) dan `Lingkaran` yang berisi pusat (sebuah `Titik`) serta jari-jari. Fungsi `jarak` digunakan untuk menghitung jarak antara dua titik menggunakan rumus Euclidean. Fungsi `didalam` menentukan apakah sebuah titik berada di dalam lingkaran dengan membandingkan jaraknya dari pusat lingkaran dengan radiusnya. Fungsi `bersinggungan` mengevaluasi apakah dua lingkaran saling bersinggungan dengan membandingkan jarak antara pusatnya dengan jumlah dan selisih radiusnya. Di dalam fungsi `main`, program menerima input dari pengguna berupa koordinat pusat dan radius dua lingkaran serta koordinat sebuah titik. Setelah itu, program memeriksa posisi titik terhadap kedua lingkaran dan mengevaluasi apakah kedua lingkaran bersinggungan, lalu mencetak hasilnya.
![[Pasted image 20250402152106.png]]

#### Soal 2

>Sebuah array digunakan untuk menampung sekumpulan bilangan bulat. Buatlah program yang digunakan untuk mengisi array tersebut sebanyak N elemen nilai. Asumsikan array memiliki kapasitas penyimpanan data sejumlah elemen tertentu. Program dapat menampilkan beberapa informasi berikut: a. Menampilkan keseluruhan isi dari array. b. Menampilkan elemen-elemen array dengan indeks ganjil saja. c. Menampilkan elemen-elemen array dengan indeks genap saja (asumsi indek ke-0 adalah genap). d. Menampilkan elemen-elemen array dengan indeks kelipatan bilangan x. x bisa diperoleh dari masukan pengguna. e. Menghapus elemen array pada indeks tertentu, asumsi indeks yang hapus selalu valid. Tampilkan keseluruhan isi dari arraynya, pastikan data yang dihapus tidak tampil f. Menampilkan rata-rata dari bilangan yang ada di dalam array. g. Menampilkan standar deviasi atau simpangan baku dari bilangan yang ada di dalam array tersebut. h. Menampilkan frekuensi dari suatu bilangan tertentu di dalam array yang telah diisi tersebut.

```go
package main

import (
	"fmt"
	"math"
)

// Mengisi array sesuai dengan jumlah yang dimasukkan
func isiArray(jumlah int) []int {
	array := make([]int, jumlah)
	for i := 0; i < jumlah; i++ {
		fmt.Printf("Masukkan elemen ke-%d: ", i+1)
		fmt.Scan(&array[i])
	}
	fmt.Println("Array yang telah dimasukkan:", array)
	return array
}

// Mengelompokkan array menjadi genap dan ganjil berdasarkan index bukan nilai
func ganjilGenap(array []int) ([]int, []int) {
	genap, ganjil := []int{}, []int{}
	for i := 0; i < len(array); i++ {
		if i%2 == 0 {
			genap = append(genap, array[i])
		} else {
			ganjil = append(ganjil, array[i])
		}
	}
	return genap, ganjil
}

// Menampilkan elemen dengan indeks kelipatan
func kelipatan(array []int, bilangan int) []int {
	hasil := []int{}
	for i := bilangan; i < len(array); i += bilangan {
		hasil = append(hasil, array[i])
	}
	return hasil
}

// Menghapus elemen berdasarkan indeks
func hapusIndeks(array []int, indeks int) []int {
	if indeks < 0 || indeks >= len(array) {
		fmt.Println("Indeks tidak ditemukan")
		return array
	}
	return append(array[:indeks], array[indeks+1:]...)
}

// Menghitung rata-rata
func rataRata(array []int) float64 {
	if len(array) == 0 {
		return 0
	}
	total := 0
	for _, val := range array {
		total += val
	}
	return float64(total) / float64(len(array))
}

// Menghitung simpangan baku
func simpanganBaku(array []int) float64 {
	if len(array) == 0 {
		return 0
	}
	rata := rataRata(array)
	var jumlah float64
	for _, val := range array {
		jumlah += math.Pow(float64(val)-rata, 2)
	}
	return math.Sqrt(jumlah / float64(len(array)))
}

// Menghitung frekuensi
func frekuensi(array []int, angka int) int {
	jumlah := 0
	for _, val := range array {
		if val == angka {
			jumlah++
		}
	}
	return jumlah
}

func main() {
	var jumlah, bilangan, indeks, angka int

	fmt.Print("Masukkan jumlah elemen array: ")
	fmt.Scan(&jumlah)

	if jumlah <= 0 {
		fmt.Println("Program berhenti karena jumlah elemen adalah <= 0.")
		return
	}

	// Menampilkan isi, rata-rata, dan simpangan baku
	array := isiArray(jumlah)
	fmt.Printf("\nRata-rata: %.2f\n", rataRata(array))
	fmt.Printf("Simpangan baku: %.2f\n", simpanganBaku(array))

	// Menampilkan indeks genap dan ganjil
	genap, ganjil := ganjilGenap(array)
	fmt.Println("\nElemen pada indeks genap:", genap)
	fmt.Println("Elemen pada indeks ganjil:", ganjil)

	// Menampilkan elemen dengan indeks kelipatan
	fmt.Print("\nMasukkan nilai kelipatan x: ")
	fmt.Scan(&bilangan)
	hasilKelipatan := kelipatan(array, bilangan)
	if len(hasilKelipatan) > 0 {
		fmt.Println("Elemen dengan indeks kelipatan", bilangan, ":", hasilKelipatan)
	} else {
		fmt.Println("Tidak ada elemen dengan indeks kelipatan", bilangan)
	}

	// Menghapus elemen
	fmt.Print("\nMasukkan indeks yang ingin dihapus: ")
	fmt.Scan(&indeks)
	array = hapusIndeks(array, indeks)
	fmt.Println("Array setelah penghapusan:", array)

	// Menampilkan rata-rata dan simpangan setelah penghapusan
	if len(array) > 0 {
		fmt.Printf("\nRata-rata setelah penghapusan: %.2f\n", rataRata(array))
		fmt.Printf("Simpangan setelah penghapusan: %.2f\n", simpanganBaku(array))
	} else {
		fmt.Println("\nArray kosong setelah penghapusan, tidak bisa menghitung rata-rata dan simpangan baku.")
	}

	// Mencari frekuensi dari bilangan yang ada di array
	fmt.Print("\nMasukkan bilangan untuk mencari frekuensi: ")
	fmt.Scan(&angka)
	fmt.Printf("Frekuensi bilangan %d dalam array: %d\n", angka, frekuensi(array, angka))
}

```

Program ini bertujuan untuk melakukan berbagai operasi pada array, seperti mengisi array, mengelompokkan elemen berdasarkan indeks genap atau ganjil, mencari elemen dengan indeks kelipatan tertentu, menghapus elemen berdasarkan indeks, serta menghitung rata-rata, simpangan baku, dan frekuensi suatu bilangan dalam array.

Pertama, pengguna diminta memasukkan jumlah elemen array. Jika jumlahnya lebih dari nol, program akan meminta pengguna untuk menginput elemen-elemen array. Setelah itu, program menghitung dan menampilkan rata-rata serta simpangan baku dari array yang telah dimasukkan. Kemudian, array dikelompokkan menjadi dua bagian berdasarkan indeksnya: indeks genap dan indeks ganjil.

Selanjutnya, pengguna diminta memasukkan nilai kelipatan tertentu untuk mencari elemen yang berada pada indeks kelipatan tersebut. Jika tidak ada elemen yang memenuhi kriteria, program akan menampilkan pesan yang sesuai. Pengguna juga dapat menghapus elemen dari array berdasarkan indeks yang diberikan, dengan validasi untuk memastikan indeks yang dimasukkan valid. Jika setelah penghapusan array menjadi kosong, program akan memberikan peringatan bahwa rata-rata dan simpangan baku tidak dapat dihitung.

Terakhir, pengguna dapat memasukkan bilangan tertentu untuk mencari jumlah kemunculannya dalam array. Semua fungsi dalam program ini telah dioptimalkan dengan penggunaan _loop_ yang lebih efisien dan validasi yang lebih ketat untuk menghindari error. Program ini memberikan pengalaman interaktif kepada pengguna untuk melakukan berbagai manipulasi pada array dengan cara yang mudah dipahami. 
![[Pasted image 20250402152917.png]]


#### Soal 3

>Sebuah program digunakan untuk menyimpan dan menampilkan nama-nama klub yang memenangkan pertandingan bola pada suatu grup pertandingan. Buatlah program yang digunakan untuk merekap skor pertandingan bola 2 buah klub bola yang berlaga. Pertama-tama program meminta masukan nama-nama klub yang bertanding, kemudian program meminta masukan skor hasil pertandingan kedua klub tersebut. Yang disimpan dalam array adalah nama-nama klub yang menang saja. Proses input skor berhenti ketika skor salah satu atau kedua klub tidak valid (negatif). Di akhir program, tampilkan daftar klub yang memenangkan pertandingan. Perhatikan sesi interaksi pada contoh berikut ini (teks bergaris bawah adalah input/read)

| Teks           | Masukan  |
| -------------- | -------- |
| Klub A:        | MU       |
| Klub B:        | INTER    |
| Pertandingan 1 | 2 0<br>  |
| Pertandingan 2 | 1 2<br>  |
| Pertandingan 3 | 2 2<br>  |
| Pertandingan 4 | 0 1<br>  |
| Pertandingan 5 | 3 2<br>  |
| Pertandingan 6 | 1 0<br>  |
| Pertandingan 7 | 5 2<br>  |
| Pertandingan 8 | 2 3<br>  |
| Pertandingan 9 | -1 2<br> |


```go
package main

import (
	"fmt"
)

func main() {
	var klubA, klubB string
	var skorA, skorB int
	var hasil []string

	fmt.Print("Klub A: ")
	fmt.Scan(&klubA)
	fmt.Print("Klub B: ")
	fmt.Scan(&klubB)

	pertandingan := 1
	for {
		fmt.Printf("Pertandingan %d (masukkan skor negatif untuk berhenti): ", pertandingan)
		fmt.Scan(&skorA, &skorB)

		// Mengakhiri program jika skor negatif dimasukkan
		if skorA < 0 || skorB < 0 {
			fmt.Println("Pertandingan berakhir.")
			break
		}

		// Menentukan pemenang dan menyimpannya dalam slice
		if skorA > skorB {
			hasil = append(hasil, fmt.Sprintf("Pertandingan %d: %s Menang", pertandingan, klubA))
		} else if skorA < skorB {
			hasil = append(hasil, fmt.Sprintf("Pertandingan %d: %s Menang", pertandingan, klubB))
		} else {
			hasil = append(hasil, fmt.Sprintf("Pertandingan %d: Seri", pertandingan))
		}

		pertandingan++
	}

	// Menampilkan semua hasil setelah input selesai
	fmt.Println("\nHasil Pertandingan:")
	for _, pemenang := range hasil {
		fmt.Println(pemenang)
	}
}

```


Program ini digunakan untuk mencatat hasil pertandingan antara dua klub sepak bola yang dimasukkan oleh pengguna. Pengguna pertama-tama diminta untuk memasukkan nama kedua klub, lalu pertandingan berlangsung dalam bentuk perulangan di mana pengguna memasukkan skor kedua tim. Jika salah satu skor yang dimasukkan bernilai negatif, program akan berhenti dan menampilkan pesan "Pertandingan berakhir". Hasil dari setiap pertandingan disimpan dalam sebuah slice, dengan format yang menunjukkan nomor pertandingan dan pemenangnya (atau "Seri" jika skornya sama). Setelah semua pertandingan selesai, program menampilkan seluruh hasil pertandingan dalam urutan yang rapi.
![[Pasted image 20250402153928.png]]

#### Soal 4

Sebuah array digunakan untuk menampung sekumpulan karakter, Anda diminta untuk membuat sebuah subprogram untuk melakukan membalikkan urutan isi array dan memeriksa apakah membentuk palindrom.

```go
package main

import "fmt"

const NMAX int = 127
type tabel [NMAX]rune

func isiArray(t *tabel, n *int) {
	*n = 0
	var c rune
	fmt.Println("Masukkan teks (akhiri dengan titik '.'): ")
	for *n < NMAX {
		fmt.Scanf("%c", &c)
		if c == '.' {
			break
		}
		if c != '\n' && c != ' ' {  // Menghindari karakter spasi dan newlines
			t[*n] = c
			*n++
		}
	}
}

func cetakArray(t tabel, n int) {
	for i := 0; i < n; i++ {
		fmt.Printf("%c", t[i])
	}
	fmt.Println()
}

func balikanArray(t *tabel, n int) {
	for i := 0; i < n/2; i++ {
		t[i], t[n-1-i] = t[n-1-i], t[i]
	}
}

func palindrom(t tabel, n int) bool {
	for i := 0; i < n/2; i++ {
		if t[i] != t[n-1-i] {
			return false
		}
	}
	return true
}

func main() {
	var tab tabel
	var m int

	isiArray(&tab, &m)

	fmt.Println("\nTeks asli: ")
	cetakArray(tab, m)

	balikanArray(&tab, m)

	fmt.Println("\nReverse teks: ")
	cetakArray(tab, m)

	fmt.Println("\nApakah Palindrom? ", palindrom(tab, m))
}


[^1]```

Program ini meminta pengguna untuk memasukkan sebuah teks, yang kemudian disimpan dalam array bertipe `rune` dan diproses untuk memeriksa apakah teks tersebut merupakan palindrom atau tidak. Pengguna diminta untuk mengakhiri input dengan titik ('.'). Program kemudian mencetak teks yang dimasukkan, membalikkan teks tersebut, dan menampilkannya kembali. Selain itu, program juga memeriksa apakah teks asli merupakan palindrom, yaitu teks yang tetap sama jika dibaca dari belakang. Fitur pembalikan teks dan pemeriksaan palindrom dilakukan menggunakan fungsi yang sesuai. Perubahan pada kode ini meliputi penanganan karakter spasi dan newline, serta memastikan inputan yang dimasukkan lebih terstruktur.
![[Pasted image 20250402154043.png]]
