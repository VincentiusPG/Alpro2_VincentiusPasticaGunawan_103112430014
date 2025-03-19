<h1 align="center">Laporan Praktikum Modul 3 <br>Fungsi</h1>
<p align="center">Vincentius Pastica Gunawan - 103112430014</p>

## Dasar Teori
Pemrograman dengan bahasa Go (Golang) mengacu pada penggunaan Go sebagai alat untuk membangun aplikasi yang efisien, skalabel, dan mudah dikelola. Go dirancang dengan sintaks yang sederhana namun kuat, mendukung pemrograman berorientasi prosedural dan memiliki fitur bawaan untuk pemrograman konkuren melalui goroutine. Dengan tipe data statis dan garbage collector, Go memastikan manajemen memori yang lebih aman dan efisien. Selain itu, Go memiliki pustaka standar yang kaya serta sistem paket yang memudahkan pengelolaan dependensi. Bahasa ini sering digunakan dalam pengembangan aplikasi berbasis cloud, layanan mikro (microservices), serta sistem yang membutuhkan performa tinggi dan keandalan, seperti server backend dan alat pemrosesan data.

## Unguided

### Soal Latihan 3.5

#### Soal 1

> Minggu ini, mahasiswa Fakultas Informatika mendapatkan tugas dari mata kuliah matematika
> diskrit untuk mempelajari kombinasi dan permutasi. Jonas salah seorang mahasiswa, iseng
> untuk mengimplementasikannya ke dalam suatu program. Oleh karena itu bersediakah kalian
> membantu Jonas?

```go
package main

import "fmt"

func factorial(n int) int {
	if n == 0 || n == 1 {
		return 1
	}
	hasil := 1
	for i := 2; i <= n; i++ {
		hasil *= i
	}
	return hasil
}

func permutation(n, r int) int {
	if n < r {
		return 0
	}
	hasil := factorial(n) / factorial(n-r)
	return hasil
}

func combination(n, r int) int {
	if n < r {
		return 0
	}
	hasil := factorial(n) / (factorial(r) * factorial(n-r))
	return hasil
}

func main() {
	var a, b, c, d int
	fmt.Scan(&a, &b, &c, &d)

	if a >= c && b >= d {
		fmt.Println(permutation(a, c), combination(a, c))
		fmt.Println(permutation(b, d), combination(b, d))
	}
}
```

Program ini adalah sebuah aplikasi sederhana dalam bahasa Go yang menghitung **permutasi** dan **kombinasi** dari dua pasang bilangan yang diinput oleh pengguna. Program menggunakan fungsi `factorial` untuk menghitung nilai faktorial, yang kemudian digunakan dalam fungsi `permutation` dan `combination` untuk menghitung permutasi \( P(n, r) = \frac{n!}{(n-r)!} \) dan kombinasi \( C(n, r) = \frac{n!}{r! \cdot (n-r)!} \). Setelah pengguna memasukkan empat bilangan (`a`, `b`, `c`, `d`), program memeriksa apakah `a >= c` dan `b >= d`. Jika kondisi terpenuhi, program menghitung dan menampilkan permutasi serta kombinasi dari pasangan `(a, c)` dan `(b, d)`. Program ini berguna untuk memahami konsep dasar permutasi dan kombinasi dalam matematika.

#### Soal 2

>Diberikan tiga buah fungsi matematika yaitu 𝑓 (𝑥) = 𝑥# , 𝑔 (𝑥) = 𝑥 − 2 dan ℎ (𝑥) = 𝑥 + 1.
>Fungsi komposisi (𝑓𝑜𝑔𝑜ℎ)(𝑥) artinya adalah 𝑓(𝑔Gℎ(𝑥)H). Tuliskan 𝑓(𝑥), 𝑔(𝑥) dan ℎ(𝑥) dalam
>bentuk function.

```go
package main

import "fmt"

func f(x int) int { 
	hasil := x * x
	return hasil
}

func g(x int) int {
	hasil := x - 2
	return hasil
}

func h(x int) int {
	hasil := x + 1
	return hasil
}
 
func main() {
	var a, b, c int
	fmt.Scan(&a, &b, &c)

	fogoh := f(g(h(a)))
	gohof := g(h(f(b)))
	hofog := h(f(g(c)))

	fmt.Print(fogoh, "\n", gohof, "\n", hofog, "\n")
}
```

Program ini adalah sebuah aplikasi sederhana dalam bahasa Go yang mendemonstrasikan komposisi fungsi matematis. Terdapat tiga fungsi utama: `f(x)` yang mengembalikan kuadrat dari `x`, `g(x)` yang mengembalikan `x - 2`, dan `h(x)` yang mengembalikan `x + 1`. Program meminta pengguna memasukkan tiga bilangan (`a`, `b`, `c`), kemudian menghitung tiga komposisi fungsi berbeda: `f(g(h(a)))`, `g(h(f(b)))`, dan `h(f(g(c)))`. Hasil dari setiap komposisi fungsi tersebut dicetak ke layar secara berurutan. Program ini berguna untuk memahami konsep komposisi fungsi dalam matematika dan pemrograman.

#### Soal 3

>[Lingkaran] Suatu lingkaran didefinisikan dengan koordinat titik pusat (𝑐𝑥, 𝑐𝑦) dengan radius
>𝑟. Apabila diberikan dua buah lingkaran, maka tentukan posisi sebuah titik sembarang (𝑥, 𝑦)
>berdasarkan dua lingkaran tersebut.

```go
package main

import (
	"fmt"
	"math"
)

func jarak(a, b, c, d float64) float64 {
	hasil := math.Sqrt(math.Pow(a-c, 2) + math.Pow(b-d, 2))
	return hasil
}

func didalam(cx, cy, r, x, y float64) bool {
	hasil := jarak(cx, cy, x, y) <= r
	return hasil
}

func main() {
	var cx1, cy1, r1, cx2, cy2, r2, x, y float64
	var didalam1, didalam2 bool

	fmt.Scan(&cx1, &cy1, &r1)
	fmt.Scan(&cx2, &cy2, &r2)
	fmt.Scan(&x, &y)

	didalam1 = didalam(cx1, cy1, r1, x, y)
	didalam2 = didalam(cx2, cy2, r2, x, y)

	if didalam1 && didalam2 {
		fmt.Println("Titik di dalam lingkaran 1 dan 2")
	} else if didalam1 {
		fmt.Println("Titik di dalam lingkaran 1")
	} else if didalam2 {
		fmt.Println("Titik di dalam lingkaran 2")
	} else {
		fmt.Println("Titik di luar lingkaran 1 dan 2")
	}
}
```


Program ini adalah sebuah aplikasi dalam bahasa Go yang menentukan posisi suatu titik relatif terhadap dua lingkaran. Program menggunakan fungsi `jarak` untuk menghitung jarak antara dua titik dalam bidang kartesian dengan rumus Euclidean distance \( \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2} \), dan fungsi `didalam` untuk memeriksa apakah suatu titik berada di dalam lingkaran dengan membandingkan jarak titik ke pusat lingkaran terhadap jari-jari lingkaran. Pengguna diminta memasukkan koordinat pusat dan jari-jari dua lingkaran, serta koordinat titik yang ingin diperiksa. Program kemudian menentukan apakah titik tersebut berada di dalam lingkaran pertama, lingkaran kedua, keduanya, atau di luar kedua lingkaran, dan menampilkan hasilnya. Program ini berguna untuk memahami konsep geometri dasar dan operasi matematika dalam pemrograman.

