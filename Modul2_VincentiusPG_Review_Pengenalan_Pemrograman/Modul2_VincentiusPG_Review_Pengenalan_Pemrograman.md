<h1 align="center">Laporan Praktikum Modul 2 <br>Review Pengenalan Pemrograman</h1>
<p align="center">Vincentius Pastica Gunawan - 103112430014</p>

## Dasar Teori
Pemrograman dengan bahasa Go (Golang) mengacu pada penggunaan Go sebagai alat untuk membangun aplikasi yang efisien, skalabel, dan mudah dikelola. Go dirancang dengan sintaks yang sederhana namun kuat, mendukung pemrograman berorientasi prosedural dan memiliki fitur bawaan untuk pemrograman konkuren melalui goroutine. Dengan tipe data statis dan garbage collector, Go memastikan manajemen memori yang lebih aman dan efisien. Selain itu, Go memiliki pustaka standar yang kaya serta sistem paket yang memudahkan pengelolaan dependensi. Bahasa ini sering digunakan dalam pengembangan aplikasi berbasis cloud, layanan mikro (microservices), serta sistem yang membutuhkan performa tinggi dan keandalan, seperti server backend dan alat pemrosesan data.

## Unguided

### Soal Latihan 2A

#### Soal 1

> Telusuri program berikut dengan cara mengkompilasi dan mengeksekusi program. Silakan masukan data yang sesuai sebanyak yang diminta program. Perhatikan keluaran yang diperoleh. Coba terangkan apa sebenarnya yang dilakukan program tersebut?

```go
package main

import "fmt"

func main() {

    var satu, dua, tiga string
    var temp string

    fmt.Print("Masukan input string: ")
    fmt.Scanln(&satu)

    fmt.Print("Masukan input string: ")
    fmt.Scanln(&dua)

    fmt.Print("Masukan input string: ")
    fmt.Scanln(&tiga)

    fmt.Println("Output awal = " + satu + " " + dua + " " + tiga)

    temp = satu
    satu = dua
    dua = tiga
    tiga = temp

    fmt.Println("Output akhir = " + satu + " " + dua + " " + tiga)

}
```

Program ini adalah program sederhana dalam bahasa Go yang meminta pengguna memasukkan tiga kata (string). Setelah itu, program menampilkan kata-kata tersebut sesuai urutan input. Kemudian, program melakukan pertukaran nilai antara ketiga kata tersebut: kata pertama dipindah ke kata kedua, kata kedua ke kata ketiga, dan kata ketiga ke kata pertama. Hasilnya, urutan kata akan berubah. Misalnya, jika inputnya adalah "A", "B", "C", output akhirnya akan menjadi "B", "C", "A". Program ini menunjukkan cara sederhana untuk menukar nilai menggunakan variabel sementara (temp).

#### Soal 2

>Tahun kabisat adalah tahun yang habis dibagi 400 atau habis dibagi 4 tetapi tidak habis dibagi 100. Buatlah sebuah program yang menerima input sebuah bilangan bulat dan memeriksa apakah bilangan tersebut merupakan tahun kabisat (true) atau bukan (false).

```go
package main

import "fmt"

func main() {
    var tahun int
    fmt.Print("Tahun: ")
    fmt.Scanln(&tahun)

    var kabisat bool

    if tahun%400 == 0 {
        kabisat = true
    } else if tahun%4 == 0 && tahun%100 != 0 {
        kabisat = true
    } else {
        kabisat = false
    }

    fmt.Print("Kabisat:", kabisat)
}
```

Program ini memeriksa apakah suatu tahun adalah tahun kabisat atau tidak menggunakan struktur `if-else`. Tahun kabisat adalah tahun yang habis dibagi 400 atau habis dibagi 4 tetapi tidak habis dibagi 100. Program meminta pengguna memasukkan tahun, lalu memeriksa kondisi tersebut: jika tahun habis dibagi 400, maka `true`; jika habis dibagi 4 tetapi tidak habis dibagi 100, maka `true`; selain itu, `false`. Hasilnya ditampilkan sebagai `true` (kabisat) atau `false` (bukan kabisat). Contohnya, tahun 2016 adalah kabisat (`true`), sedangkan 2018 bukan (`false`).

#### Soal 3

>Buat program Bola yang menerima input jari-jari suatu bola (bilangan bulat). Tampilkan Volume dan Luas kulit bola. 𝑣𝑜𝑙𝑢𝑚𝑒𝑏𝑜𝑙𝑎 = 4 3 𝜋𝑟 3 dan 𝑙𝑢𝑎𝑠𝑏𝑜𝑙𝑎 = 4𝜋𝑟 2 (π ≈ 3.1415926535).

```go
package main

import "fmt"

func main() {
    var jariJari int
    fmt.Print("Jejari = ")
    fmt.Scanln(&jariJari)
    pi := 3.1415926535

    volume := (4.0 / 3.0) * pi * float64(jariJari*jariJari*jariJari)

    luasKulit := 4 * pi * float64(jariJari*jariJari)

    fmt.Printf("Bola dengan jejari %d memiliki volume %.4f dan luas kulit %.4f\n", jariJari, volume, luasKulit)
}
```


Program ini menghitung volume dan luas kulit bola berdasarkan jari-jari yang dimasukkan oleh pengguna. Program menggunakan rumus volume bola \( \frac{4}{3} \pi r^3 \) dan luas kulit bola \( 4\pi r^2 \), dengan nilai π (pi) sekitar 3.1415926535. Pengguna diminta memasukkan jari-jari bola, lalu program menghitung volume dan luas kulitnya secara manual tanpa menggunakan fungsi matematika tambahan. Hasilnya ditampilkan dengan format 4 angka di belakang koma. Contohnya, jika jari-jari yang dimasukkan adalah 5, program akan menampilkan volume 523.5988 dan luas kulit 314.1593. Program ini sederhana dan hanya menggunakan package `fmt` untuk input dan output.

#### Soal 4

>Dibaca nilai temperatur dalam derajat Celsius. Nyatakan temperatur tersebut dalam Fahrenheit 𝐶𝑒𝑙𝑠𝑖𝑢𝑠 = (𝐹𝑎ℎ𝑟𝑒𝑛ℎ𝑒𝑖𝑡 − 32) × 5/9 𝑅𝑒𝑎𝑚𝑢𝑟 = 𝐶𝑒𝑙𝑐𝑖𝑢𝑠 × 4/5 𝐾𝑒𝑙𝑣𝑖𝑛 = (𝐹𝑎ℎ𝑟𝑒𝑛ℎ𝑒𝑖𝑡 + 459.67) × 5/9

```go
package main

import "fmt"

func main() {
    var celsius float64
    fmt.Print("Temperatur Celsius: ")
    fmt.Scanln(&celsius)

    fahrenheit := (celsius * 9/5) + 32

    reamur := celsius * 4/5

    kelvin := celsius + 273.15

    fmt.Println("Derajat Reamur: ", int(reamur))
    fmt.Println("Derajat Fahrenheit: ", int(fahrenheit))
    fmt.Println("Derajat Kelvin: ", int(kelvin))
}
```


Program ini mengonversi suhu dari Celsius ke Fahrenheit, Reamur, dan Kelvin. Pengguna memasukkan suhu dalam Celsius, lalu program menghitung nilai konversinya menggunakan rumus:  
- Fahrenheit: \( (Celsius \times \frac{9}{5}) + 32 \)  
- Reamur: \( Celsius \times \frac{4}{5} \)  
- Kelvin: \( Celsius + 273.15 \)  

Hasilnya ditampilkan dalam bilangan bulat menggunakan `fmt.Print`. Contoh, jika input Celsius adalah 50, outputnya adalah Reamur: 40, Fahrenheit: 122, dan Kelvin: 323. Program ini sederhana dan hanya menggunakan `fmt` untuk input dan output.

#### Soal 5

>Tipe karakter sebenarnya hanya apa yang tampak dalam tampilan. Di dalamnya tersimpan dalam bentuk biner 8 bit (byte) atau 32 bit (rune) saja. Buat program ASCII yang akan membaca 5 buat data integer dan mencetaknya dalam format karakter. Kemudian membaca 3 buah data karakter dan mencetak 3 buah karakter setelah karakter tersebut (menurut tabel ASCII) Masukan terdiri dari dua baris. Baris pertama berisi 5 buah data integer. Data integer mempunyai nilai antara 32 s.d. 127. Baris kedua berisi 3 buah karakter yang berdampingan satu dengan yang lain (tanpa dipisahkan spasi). Keluaran juga terdiri dari dua baris. Baris pertama berisi 5 buah representasi karakter dari data yang diberikan, yang berdampingan satu dengan lain, tanpa dipisahkan spasi. Baris kedua berisi 3 buah karakter (juga tidak dipisahkan oleh spasi).

```go
package main

import "fmt"

func main() {
    var a, b, c, d, e int
    fmt.Scan(&a, &b, &c, &d, &e)

    fmt.Printf("%c%c%c%c%c\n", a, b, c, d, e)

    var char1, char2, char3 rune
    fmt.Scanf("%c%c%c", &char1, &char2, &char3)

    fmt.Printf("%c%c%c\n", char1+3, char2+3, char3+3)
}```


Program ini membaca 5 angka integer dan mengonversinya ke karakter ASCII, lalu menampilkannya sebagai satu string. Kemudian, program membaca 3 karakter dan menampilkan 3 karakter berikutnya berdasarkan tabel ASCII dengan menambahkan 3 ke nilai ASCII karakter tersebut. Contoh, input `66 97 103 117 115` dan `SNO` menghasilkan output `Bagus` dan `TOP`. Program menggunakan `fmt.Scanf` untuk membaca karakter dan `fmt.Printf` untuk menampilkan hasilnya.

### Soal Latihan 2B

#### Soal 1

> Siswa kelas IPA di salah satu sekolah menengah atas di Indonesia sedang mengadakan praktikum kimia. Di setiap percobaan akan menggunakan 4 tabung reaksi, yang mana susunan warna cairan di setiap tabung akan menentukan hasil percobaan. Siswa diminta untuk mencatat hasil percobaan tersebut. Percobaan dikatakan berhasil apabila susunan warna zat cair pada gelas 1 hingga gelas 4 secara berturutan adalah ‘merah’, ‘kuning’, ‘hijau’, dan ‘ungu’ selama 5 kali percobaan berulang. Buatlah sebuah program yang menerima input berupa warna dari ke 4 gelas reaksi sebanyak 5 kali percobaan. Kemudian program akan menampilkan true apabila urutan warna sesuai dengan informasi yang diberikan pada paragraf sebelumnya, dan false untuk urutan warna lainnya.

```go
package main

import "fmt"

func main() {

	var gelas1, gelas2, gelas3, gelas4 string
	var berhasil bool

	berhasil = true

	for i := 1; i <= 5; i++ {
		fmt.Print("Percobaan ", i, ": ")
		fmt.Scan(&gelas1, &gelas2, &gelas3, &gelas4)

		if !(gelas1 == "merah" && gelas2 == "kuning" && gelas3 == "hijau" && gelas4 == "ungu") {
			berhasil = false
		}
	}

	fmt.Print("Berhasil: ", berhasil)

}
```


Program di atas meminta pengguna untuk memasukkan warna dari empat gelas sebanyak lima kali. Jika semua percobaan memiliki urutan warna merah, kuning, hijau, ungu, maka program mencetak "Berhasil: true", jika ada satu saja yang berbeda, maka mencetak "Berhasil: false".

#### Soal 2

> Suatu pita (string) berisi kumpulan nama-nama bunga yang dipisahkan oleh spasi dan ‘– ‘, contoh pita diilustrasikan seperti berikut ini. Pita: mawar – melati – tulip – teratai – kamboja – anggrek Buatlah sebuah program yang menerima input sebuah bilangan bulat positif (dan tidak nol) N, kemudian program akan meminta input berupa nama bunga secara berulang sebanyak N kali dan nama tersebut disimpan ke dalam pita. (Petunjuk: gunakan operasi penggabungan string dengan operator “+” ). Tampilkan isi pita setelah proses input selesai.

```go
package main

import "fmt"

func main() {
	var bunga, rangkaian string
	var total int

	for {
		fmt.Print("Masukkan bunga ke-", total+1, ": ")
		fmt.Scan(&bunga)

		if bunga == "selesai" {
			break
		}

		if total > 0 {
			rangkaian += " - "
		}
		rangkaian += bunga
		total++
	}

	fmt.Println("Rangkaian pita:", rangkaian)
	fmt.Println("Total bunga:", total)
}
```

Program ini meminta pengguna untuk memasukkan nama bunga satu per satu. Jika pengguna mengetik "selesai", program akan berhenti dan menampilkan rangkaian bunga yang telah dimasukkan dengan pemisah " - ", serta jumlah total bunga yang dimasukkan.

#### Soal 3

> Setiap hari Pak Andi membawa banyak barang belanjaan dari pasar dengan mengendarai sepeda motor. Barang belanjaan tersebut dibawa dalam kantong terpal di kiri-kanan motor. Sepeda motor tidak akan oleng jika selisih berat barang di kedua kantong sisi tidak lebih dari 9 kg. Buatlah program Pak Andi yang menerima input dua buah bilangan real positif yang menyatakan berat total masing-masing isi kantong terpal. Program akan terus meminta input bilangan tersebut hingga salah satu kantong terpal berisi 9 kg atau lebih.

```go
package main

import "fmt"

func main() {
	var beratKiri, beratKanan, selisih float32
	var tidakOleng bool

	for {
		fmt.Print("Masukkan berat belanjaan (kg) di kantong kiri dan kanan: ")
		fmt.Scan(&beratKiri, &beratKanan)

		if beratKiri >= 9 || beratKanan >= 9 {
			fmt.Println("Proses selesai. Kantong mencapai batas berat.")
			break
		}

		selisih = beratKiri - beratKanan
		if selisih < 0 {
			selisih = -selisih
		}

		tidakOleng = selisih <= 9
		fmt.Println("Sepeda motor stabil:", tidakOleng)
	}
}

```

Program ini meminta pengguna memasukkan berat belanjaan di kantong kiri dan kanan motor Pak Andi. Jika salah satu kantong mencapai 9 kg atau lebih, program berhenti. Selisih berat dihitung, dan motor dianggap stabil jika perbedaannya tidak lebih dari 9 kg. Program terus berjalan hingga batas berat tercapai.

#### Soal 4
> Diberikan sebuah persamaan sebagai berikut ini. 𝑓(𝑘) = (4𝑘 + 2) 2 (4𝑘 + 1)(4𝑘 + 3) Buatlah sebuah program yang menerima input sebuah bilangan sebagai K, kemudian menghitung dan menampilkan nilai f(K) sesuai persamaan di atas.

```go
package main

import "fmt"

func main() {
	var k int
	var hasil int

	fmt.Print("Masukkan nilai K: ")
	fmt.Scan(&k)

	hasil = (4*k + 2) * (4*k + 2) * (4*k + 1) * (4*k + 3)

	fmt.Println("Nilai f(K):", hasil)
}

```

Program ini menerima input K, lalu menghitung f(K) berdasarkan rumus yang diberikan dan menampilkan hasilnya.

### Soal Latihan 2C

#### Soal 1

> PT POS membutuhkan aplikasi perhitungan biaya kirim berdasarkan berat parsel. Maka, buatlah program BiayaPos untuk menghitung biaya pengiriman tersebut dengan ketentuan sebagai berikut! Dari berat parsel (dalam gram), harus dihitung total berat dalam kg dan sisanya (dalam gram). Biaya jasa pengiriman adalah Rp. 10.000,- per kg. Jika sisa berat tidak kurang dari 500 gram, maka tambahan biaya kirim hanya Rp. 5,- per gram saja. Tetapi jika kurang dari 500 gram, maka tambahan biaya akan dibebankan sebesar Rp. 15,- per gram. Sisa berat (yang kurang dari 1kg) digratiskan biayanya apabila total berat ternyata lebih dari 10kg.

```go
package main

import "fmt"

func main() {
	var beratGram, beratKg, sisaGram, biaya int

	fmt.Print("Masukkan berat parsel (gram): ")
	fmt.Scan(&beratGram)

	beratKg = beratGram / 1000
	sisaGram = beratGram % 1000

	biaya = beratKg * 10000

	if beratKg > 10 {
		sisaGram = 0 
	} else if sisaGram >= 500 {
		biaya += sisaGram * 5
	} else {
		biaya += sisaGram * 15
	}

	fmt.Println("Total berat:", beratKg, "kg", sisaGram, "gram")
	fmt.Println("Total biaya kirim: Rp.", biaya)
}

```

Program ini meminta input berat parsel dalam gram, lalu menghitung total kg dan sisa gram. Biaya dihitung berdasarkan aturan: Rp. 10.000 per kg, tambahan biaya sesuai sisa gram, dan jika berat lebih dari 10 kg, sisa gram digratiskan.

#### Soal 2

> Jawablah pertanyaan-pertanyaan berikut: 
> a. Jika nam diberikan adalah 80.1, apa keluaran dari program tersebut? Apakah eksekusi program tersebut sesuai spesifikasi soal? 
> b. Apa saja kesalahan dari program tersebut? Mengapa demikian? Jelaskan alur program seharusnya! 
> c. Perbaiki program tersebut! Ujilah dengan masukan: 93.5; 70.6; dan 49.5. Seharusnya keluaran yang diperoleh adalah ‘A’, ‘B’, dan ‘D’.

##### Kode Awal
```go
package main
import “fmt”
func main() {
 var nam float64
 var nmk string
 fmt.Print(“Nilai akhir mata kuliah: “)
 fmt.Scanln(&nam)
 if nam > 80 {
 nam = “A”
 }
 if nam > 72.5 {
 nam = “AB”
 }
 if nam > 65 {
 nam = “B”
 }
 if nam > 57.5 {
 nam = “BC”
 }
 if nam > 50 {
 nam = “C”
 }
 if nam > 40 {
 nam = “D”
 } else if nam <= 40 {
 nam = “E”
 }
 fmt.Println(“Nilai mata kuliah: “, nmk)
}
```

##### Kode Setelah Perbaikan
```go
package main

import "fmt"

func main() {
	var nam float64
	var nmk string

	fmt.Print("Nilai akhir mata kuliah: ")
	fmt.Scanln(&nam)

	if nam > 80 {
		nmk = "A"
	} else if nam > 72.5 {
		nmk = "AB"
	} else if nam > 65 {
		nmk = "B"
	} else if nam > 57.5 {
		nmk = "BC"
	} else if nam > 50 {
		nmk = "C"
	} else if nam > 40 {
		nmk = "D"
	} else {
		nmk = "E"
	}

	fmt.Println("Nilai mata kuliah:", nmk)
}

```

Program ini meminta pengguna memasukkan nilai akhir mata kuliah, lalu menentukan nilai huruf berdasarkan rentang nilai yang telah ditentukan. Nilai huruf ditetapkan menggunakan struktur if-else if agar hanya satu kondisi yang berlaku. Setelah itu, program menampilkan nilai huruf yang sesuai dengan input yang diberikan.

#### Soal 3

> Sebuah bilangan bulat b memiliki faktor bilangan f > 0 jika f habis membagi b. Contoh: 2 merupakan faktor dari bilangan 6 karena 6 habis dibagi 2. Buatlah program yang menerima input sebuah bilangan bulat b dan b > 1. Program harus dapat mencari dan menampilkan semua faktor dari bilangan tersebut!
> Bilangan bulat b > 0 merupakan bilangan prima p jika dan hanya jika memiliki persis dua faktor bilangan saja, yaitu 1 dan dirinya sendiri. Lanjutkan program sebelumnya. Setelah menerima masukan sebuah bilangan bulat b > 0. Program tersebut mencari dan menampilkan semua faktor bilangan tersebut. Kemudian, program menentukan apakah b merupakan bilangan prima.

```go
package main

import "fmt"

func main() {
	var bilangan, faktor int

	fmt.Print("Masukkan bilangan: ")
	fmt.Scan(&bilangan)

	if bilangan <= 1 {
		fmt.Println("Bilangan harus lebih dari 1!")
		return
	}

	fmt.Print("Faktor: ")
	for i := 1; i <= bilangan; i++ {
		if bilangan%i == 0 {
			fmt.Print(i, " ")
			faktor++
		}
	}

	fmt.Println()
	if faktor == 2 {
		fmt.Println("Bilangan prima: Ya")
	} else {
		fmt.Println("Bilangan prima: Tidak")
	}
}
```


Program ini menerima input bilangan bulat **b > 1**, lalu mencari dan menampilkan semua faktor dari bilangan tersebut. Setelah itu, program menentukan apakah bilangan tersebut merupakan bilangan **prima** dengan memeriksa jumlah faktornya. Jika hanya memiliki **dua faktor** (1 dan dirinya sendiri), maka bilangan tersebut **prima**, jika tidak, maka bukan prima.

