<h1 align="center">Laporan Praktikum Modul 5 <br>Rekursif</h1>
<p align="center">Vincentius Pastica Gunawan - 103112430014</p>

## Dasar Teori
Rekursif adalah teknik dalam pemrograman di mana sebuah fungsi memanggil dirinya sendiri secara langsung atau tidak langsung untuk menyelesaikan masalah yang dapat dipecah menjadi sub-masalah serupa yang lebih kecil. Rekursif terdiri dari dua komponen utama: base case (kasus dasar) yang menghentikan pemanggilan rekursif ketika kondisi tertentu terpenuhi, dan recursive case (kasus rekursif) yang memecah masalah menjadi bagian lebih sederhana dan memanggil fungsi kembali. Rekursif umumnya digunakan untuk menyelesaikan masalah yang memiliki struktur berulang atau hierarkis seperti faktorial, deret Fibonacci, pencarian dalam struktur data (pohon/graph), serta algoritma divide-and-conquer (contoh: sorting merge sort dan quick sort). Kelebihan rekursif adalah kode yang lebih ringkas dan deklaratif, tetapi perlu hati-hati terhadap stack overflow jika rekursi terlalu dalam tanpa base case yang tepat atau masalah yang tidak efisien karena pemanggilan berulang.

## Unguided

### Soal Latihan Modul 5

#### Soal 1

> Deret fibonacci adalah sebuah deret dengan nilai suku ke-0 dan ke-1 adalah 0 dan 1, dan nilai
> suku ke-n selanjutnya adalah hasil penjumlahan dua suku sebelumnya. Secara umum dapat
> diformulasikan 𝑆( = 𝑆(+. + 𝑆(+# . Berikut ini adalah contoh nilai deret fibonacci hingga suku
> ke-10. Buatlah program yang mengimplementasikan fungsi rekursif pada deret fibonacci
> tersebut.

```go
package main

import "fmt"

// Fungsi untuk menghitung bilangan Fibonacci secara rekursif
func fibonacci(n int) int {
	if n < 2 {
		return n
	}
	return fibonacci(n-1) + fibonacci(n-2)
}

// Fungsi rekursif untuk mencetak deret Fibonacci tanpa menggunakan return
func cetakFibonacci(i, n int) {
	fmt.Print(fibonacci(i), " ")
	if i < n {
		cetakFibonacci(i+1, n)
	}
}

func main() {
	var n int
	fmt.Scan(&n)
	cetakFibonacci(0, n)
}
```

Kode ini menghitung dan mencetak deret Fibonacci menggunakan rekursi dalam bahasa Go. Fungsi `fibonacci(n)` secara rekursif menghitung bilangan Fibonacci ke-`n`, dengan kondisi dasar `fibonacci(0) = 0` dan `fibonacci(1) = 1`, sedangkan untuk `n ≥ 2`, nilainya dihitung sebagai `fibonacci(n-1) + fibonacci(n-2)`. Fungsi `cetakFibonacci(i, n)` digunakan untuk mencetak deret Fibonacci dari `0` hingga `n` tanpa menggunakan `return`, dengan mencetak hasil `fibonacci(i)` lalu memanggil dirinya sendiri untuk `i+1` hingga `n` tercapai. Dalam fungsi `main()`, program meminta input `n` dari pengguna lalu memanggil `cetakFibonacci(0, n)`, yang akan mencetak deret Fibonacci dari `0` hingga `n`. Meskipun rekursi membuat kode lebih sederhana, pendekatan ini kurang efisien untuk nilai `n` besar karena perhitungan ulang yang berlebihan.

#### Soal 2

>Buatlah sebuah program yang digunakan untuk menampilkan pola bintang berikut ini dengan
>menggunakan fungsi rekursif. N adalah masukan dari user.
	

| No  | Masukan | Keluaran                        |
| --- | ------- | ------------------------------- |
| 1   | 5       | *<br>**<br>***<br>****<br>***** |
| 2   | 1       | *                               |
| 3   | 3       | *<br>**<br>***                  |


```go
package main

import "fmt"

// Digunakan untuk mencetak bintang sebanyak nilai n
func bintang(n int) {
	if n > 0 {
		fmt.Print("*")
		bintang(n - 1)
	}
}

// Mengatur baris dari output yang akan tampil
func pola(n, baris int) {
	if baris <= n {
		bintang(baris)
		fmt.Println()
		pola(n, baris+1)
	}
}

func main() {
	var n int
	fmt.Print("Masukkan jumlah baris pola: ")
	fmt.Scan(&n)

	if n > 0 {
		pola(n, 1)
	} else {
		fmt.Println("Masukkan bilangan positif.")
	}
}
```

Program ini merupakan implementasi pola segitiga bintang menggunakan pendekatan rekursif dalam bahasa Go, di mana pengguna diminta memasukkan jumlah baris (`n`) sebagai input, kemudian program akan mencetak pola segitiga siku-siku dengan tinggi `n` baris yang terdiri dari bintang (`*`). Program terdiri dari dua fungsi rekursif utama: `bintang(n)` yang mencetak sejumlah `n` bintang secara horizontal dengan memanggil dirinya sendiri hingga mencapai base case (`n ≤ 0`), dan `pola(n, baris)` yang mengatur pencetakan per baris secara vertikal dengan memanggil `bintang(baris)` untuk setiap baris dan rekursi hingga `baris > n`. Program juga melakukan validasi input untuk memastikan nilai `n` positif, menjadikannya contoh sederhana namun lengkap untuk demonstrasi rekursi dalam pembuatan pola.

#### Soal 3

>Buatlah program yang mengimplementasikan rekursif untuk menampilkan faktor bilangan dari
suatu N, atau bilangan yang apa saja yang habis membagi N.
Masukan terdiri dari sebuah bilangan bulat positif N.
Keluaran terdiri dari barisan bilangan yang menjadi faktor dari N (terurut dari 1 hingga N ya).

| No  | Masukan | Keluaran      |
| --- | ------- | ------------- |
| 1   | 5       | 1 5           |
| 2   | 12      | 1 2 3 4  6 12 |


```go
package main

import "fmt"

// Fungsi rekursif untuk mencetak faktor bilangan
func faktorBilangan(n, i int) {
    if i > n/2 {  // Optimasi: tidak perlu cek lebih dari n/2
        fmt.Print(n) // n selalu faktor dari dirinya sendiri
        return
    }
    if n%i == 0 {
        fmt.Print(i, " ")
    }
    faktorBilangan(n, i+1)
}

func main() {
    var n int
    fmt.Print("Masukkan bilangan bulat positif: ")
    fmt.Scan(&n)
    
    if n <= 0 {
        fmt.Println("Input harus bilangan bulat positif")
        return
    }
    
    fmt.Printf("Faktor dari %d: ", n)
    faktorBilangan(n, 1)
    fmt.Println() // Tambah newline di akhir
}
```


Program ini merupakan implementasi pencarian faktor bilangan menggunakan pendekatan rekursif dalam bahasa Go, di mana pengguna diminta memasukkan sebuah bilangan bulat positif (n) sebagai input, kemudian program akan mencetak semua faktor dari bilangan tersebut secara berurutan. Fungsi rekursif faktorBilangan(n, i) bekerja dengan memeriksa secara berulang apakah nilai i merupakan faktor dari n (dengan operasi modulus n%i == 0) mulai dari i = 1 hingga i = n/2 (optimasi untuk mengurangi jumlah iterasi), kemudian secara terpisah mencetak nilai n itu sendiri sebagai faktor terakhir. Program juga dilengkapi dengan validasi input untuk memastikan bilangan yang dimasukkan positif serta format output yang lebih informatif dengan menampilkan label hasil, menjadikannya contoh sederhana namun efektif untuk demonstrasi konsep rekursi dan operasi matematika dasar dalam pemrograman.
