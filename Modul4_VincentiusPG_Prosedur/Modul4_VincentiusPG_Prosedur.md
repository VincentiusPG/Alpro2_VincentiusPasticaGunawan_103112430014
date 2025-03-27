<h1 align="center">Laporan Praktikum Modul 4 <br>Prosedur</h1>
<p align="center">Vincentius Pastica Gunawan - 103112430014</p>

## Dasar Teori
Pemrograman dengan bahasa Go (Golang) mengacu pada penggunaan Go sebagai alat untuk membangun aplikasi yang efisien, skalabel, dan mudah dikelola. Go dirancang dengan sintaks yang sederhana namun kuat, mendukung pemrograman berorientasi prosedural dan memiliki fitur bawaan untuk pemrograman konkuren melalui goroutine. Dengan tipe data statis dan garbage collector, Go memastikan manajemen memori yang lebih aman dan efisien. Selain itu, Go memiliki pustaka standar yang kaya serta sistem paket yang memudahkan pengelolaan dependensi. Bahasa ini sering digunakan dalam pengembangan aplikasi berbasis cloud, layanan mikro (microservices), serta sistem yang membutuhkan performa tinggi dan keandalan, seperti server backend dan alat pemrosesan data.

## Unguided

### Soal Latihan Modul 4

#### Soal 1

> Minggu ini, mahasiswa Fakultas Informatika mendapatkan tugas dari mata kuliah matematika
> diskrit untuk mempelajari kombinasi dan permutasi. Jonas salah seorang mahasiswa, iseng
> untuk mengimplementasikannya ke dalam suatu program. Oleh karena itu bersediakah kalian
> membantu Jonas?

```go
package main

import "fmt"

// Prosedur untuk menghitung nilai faktorial
func factorial(n int, hasil *int) {
    *hasil = 1
    for i := 2; i <= n; i++ {
        *hasil *= i
    }
}

// Prosedur untuk menghitung nilai permutasi
func permutation(n, r int, hasil *int) {
    var faktN, faktNR int
    
    if n < r {
        *hasil = 0
        return
    }
    
    factorial(n, &faktN)
    factorial(n-r, &faktNR)
    *hasil = faktN / faktNR
}

// Prosedur untuk menghitung nilai kombinasi
func combination(n, r int, hasil *int) {
    var faktN, faktR, faktNR int
    
    if n < r {
        *hasil = 0
        return
    }
    
    factorial(n, &faktN)
    factorial(r, &faktR)
    factorial(n-r, &faktNR)
    *hasil = faktN / (faktR * faktNR)
}

func main() {
    var a, b, c, d, permA, combA, permB, combB int
    fmt.Scan(&a, &b, &c, &d)

    if a >= c && b >= d {
        permutation(a, c, &permA)
        combination(a, c, &combA)
        permutation(b, d, &permB)
        combination(b, d, &combB)
        
        fmt.Println(permA, combA)
        fmt.Println(permB, combB)
    } else {
        fmt.Println("Input tidak valid")
    }
}
```

Kode ini merupakan program dalam bahasa Go yang menghitung **permutasi** dan **kombinasi** dari dua pasang input bilangan (`a, c` dan `b, d`) menggunakan pendekatan prosedural dengan parameter pointer. Program terdiri dari tiga prosedur utama: `factorial` (menghitung faktorial suatu bilangan), `permutation` (menghitung P(n, r) = n!/(n-r)!), dan `combination` (menghitung C(n, r) = n!/(r!(n-r)!)) yang semuanya menggunakan pointer untuk menyimpan hasil perhitungan. Di fungsi `main`, program membaca input pengguna, memvalidasi apakah `a ≥ c` dan `b ≥ d`, kemudian menghitung dan menampilkan hasil permutasi serta kombinasi untuk kedua pasang bilangan jika valid; jika tidak, program akan menampilkan pesan error "Input tidak valid". Program ini mengutamakan modularitas dengan memisahkan logika perhitungan ke dalam prosedur-prosedur terpisah.

#### Soal 2

>Kompetisi pemrograman tingkat nasional berlangsung ketat. Setiap peserta diberikan 8 soal
>yang harus dapat diselesaikan dalam waktu 5 jam saja. Peserta yang berhasil menyelesaikan
>soal paling banyak dalam waktu paling singkat adalah pemenangnya.
>Buat program gema yang mencari pemenang dari daftar peserta yang diberikan. Program harus
>dibuat modular, yaitu dengan membuat prosedur hitungSkor yang mengembalikan total soal
>dan total skor yang dikerjakan oleh seorang peserta, melalui parameter formal. Pembacaan
>nama peserta dilakukan di program utama, sedangkan waktu pengerjaan dibaca di dalam
>prosedur.
>prosedure hitungSkor(in/out soal, skor : integer)
>Setiap baris masukan dimulai dengan satu string nama peserta tersebut diikuti dengan adalah
>8 integer yang menyatakan berapa lama (dalam menit) peserta tersebut menyelesaikan soal.
>Jika tidak berhasil atau tidak mengirimkan jawaban maka otomatis dianggap menyelesaikan
>dalam waktu 5 jam 1 menit (301 menit).
>Satu baris keluaran berisi nama pemenang, jumlah soal yang diselesaikan, dan nilai yang
>diperoleh. Nilai adalah total waktu yang dibutuhkan untuk menyelesaikan soal yang berhasil
>diselesaikan.

```go
package main

import "fmt"

// Prosedur untuk menghitung jumlah soal yang dijawab dan total skor
func hitungSkor(soal, skor *int) {
    var waktu int
    *soal = 0
    *skor = 0
    
    for i := 0; i < 8; i++ {
        fmt.Scan(&waktu)
        if waktu < 301 {
            *soal++
            *skor += waktu
        }
    }
}

// Prosedur untuk menentukan pemenang
func tentukanPemenang(nama string, soal, skor int, pemenang *string, maxSoal, minSkor *int) {
    if soal > *maxSoal || (soal == *maxSoal && skor < *minSkor) {
        *maxSoal = soal
        *minSkor = skor
        *pemenang = nama
    }
}

func main() {
    var nama, pemenang string
    var soal, skor int
    maxSoal := -1
    minSkor := 99999

    for {
        fmt.Scan(&nama)
        if nama == "Selesai" || nama == "selesai" {
            break
        }

        hitungSkor(&soal, &skor)
        tentukanPemenang(nama, soal, skor, &pemenang, &maxSoal, &minSkor)
    }

    if pemenang != "" {
        fmt.Println(pemenang, maxSoal, minSkor)
    } else {
        fmt.Println("Tidak ada peserta")
    }
}
```

Program ini merupakan sistem penilaian kompetisi pemrograman yang menentukan pemenang berdasarkan jumlah soal yang berhasil diselesaikan (dengan batas waktu <301 detik per soal) dan total waktu yang dibutuhkan. Kode menggunakan pendekatan prosedural dengan dua prosedur utama: `hitungSkor` yang menghitung jumlah soal terselesaikan dan total waktu peserta, serta `tentukanPemenang` yang membandingkan skor peserta untuk menentukan pemenang sementara. Program membaca input nama peserta dan waktu penyelesaian 8 soal, kemudian setelah menerima input "Selesai", akan menampilkan nama pemenang beserta jumlah soal yang diselesaikan dan total waktu yang digunakan, dengan prioritas peserta yang menyelesaikan lebih banyak soal, atau jika sama, yang memiliki waktu total lebih cepat. Program juga menangani kasus ketika tidak ada peserta yang mengikuti kompetisi.

#### Soal 3

>Skiena dan Revilla dalam Programming Challenges mendefinisikan sebuah deret bilangan. Deret dimulai dengan sebuah bilangan bulat n. Jika bilangan n saat itu genap, maka suku berikutnya adalah ½n, tetapi jika ganjil maka suku berikutnya bernilai 3n+1. Rumus yang sama digunakan terus menerus untuk mencari suku berikutnya. Deret berakhir ketika suku terakhir Halaman 9 | M o d u l P r a k t i k u m A l g o r i t m a P e m r o g r a m a n bernilai 1. Sebagai contoh jika dimulai dengan n=22, maka deret bilangan yang diperoleh adalah: 22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1 Untuk suku awal sampai dengan 1000000, diketahui deret selalu mencapai suku dengan nilai 1. Buat program skiena yang akan mencetak setiap suku dari deret yang dijelaskan di atas untuk nilai suku awal yang diberikan. Pencetakan deret harus dibuat dalam prosedur cetakDeret yang mempunyai 1 parameter formal, yaitu nilai dari suku awal. prosedure cetakDeret(in n : integer ) Masukan berupa satu bilangan integer positif yang lebih kecil dari 1000000. Keluaran terdiri dari satu baris saja. Setiap suku dari deret tersebut dicetak dalam baris yang dan dipisahkan oleh sebuah spasi.

```go
package main

import "fmt"

// Prosedur untuk mencetak deret Collatz dari suatu angka
func cetakDeretCollatz(n int) {
    fmt.Print("Deret Collatz: ")
    for n != 1 {
        fmt.Print(n, " → ")
        if n%2 == 0 {
            n /= 2
        } else {
            n = n*3 + 1
        }
    }
    fmt.Print(1) // Cetak angka terakhir (1)
}

func main() {
    var n int
    fmt.Print("Masukkan bilangan bulat positif (1-999): ")
    fmt.Scan(&n)

    if n > 0 && n < 1000 {
        cetakDeretCollatz(n)
    } else {
        fmt.Println("Input harus bilangan bulat antara 1-999")
    }
}
```


Program ini merupakan implementasi dari **Konjektur Collatz** yang mencetak deret bilangan dari sebuah input bilangan bulat positif (1-999), di mana setiap bilangan genap dibagi 2 dan bilangan ganjil diubah menjadi 3n+1, proses berlanjut hingga mencapai angka 1. Kode terdiri dari prosedur `cetakDeretCollatz` yang menangani logika pembentukan deret dengan format output rapi (misal: "7 → 22 → 11 → ... → 1") dan program utama yang memvalidasi input pengguna, menampilkan pesan error jika input di luar rentang valid, serta memberikan petunjuk input yang jelas. Program ini berguna untuk memvisualisasikan proses matematis dalam konjektur Collatz secara interaktif.

