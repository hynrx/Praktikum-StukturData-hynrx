
# <h1 align="center">Laporan Praktikum Modul 1 <br> Code Blocks IDE & Pengenalan Bahasa C++</h1>
<p align="center">HISYAM NURDIATMOKO - 103112400049</p>

## Dasar Teori

Bahasa C++ merupakan bahasa pengembangan dari C yang diciptakan oleh Bjarne Stroustrup, di mana struktur programnya secara fundamental terdiri dari fungsi utama main() dan deklarasi pustaka seperti <iostream> untuk operasi dasar. Di dalam program, digunakan identifier sebagai nama untuk variabel yang menyimpan data dengan tipe tertentu seperti int untuk bilangan bulat atau float untuk desimal dan juga konstanta untuk nilai yang tetap. Interaksi dengan pengguna difasilitasi oleh fungsi input cin dan output cout , sementara alur eksekusi program dikendalikan melalui struktur kondisional seperti if-else atau switch untuk pengambilan keputusan serta perulangan (for, while) untuk menjalankan blok kode berulang kali. Seluruh manipulasi data ini dilakukan dengan berbagai operator, mulai dari aritmatika (+, -), logika (&&, ||), hingga increment (++) dan decrement (--).

## Guided

### Aritmatika

```cpp
#include <iostream>
using namespace std;
int main()
{
    int W, X, Y;
    float Z;
    X = 7;
    Y = 3;
    W = 1;
    Z = (X + Y) / (Y + W);
    cout << "Nilai z = " << Z << endl;
    return 0;
}
```
> Output
> ![Screenshot bagian x](output/aritmatika.png)

program C++ ini bertujuan untuk melakukan sebuah perhitungan aritmatika sederhana dan menampilkan hasilnya ke layar. Kode tersebut pertama-tama mendeklarasikan tiga variabel integer W, X, dan Y yang masing-masing diberi nilai 1, 7, dan 3, serta satu variabel float Z untuk menampung hasil akhir. Operasi utamanya adalah Z = (X + Y) / (Y + W), yang secara matematis menjadi 10 / 4. Karena pembagian ini dilakukan antara dua bilangan bulat, C++ akan melakukan integer division yang hasilnya membuang sisa desimal, sehingga 10 / 4 menghasilkan 2, bukan 2.5. Nilai 2 ini kemudian disimpan ke dalam variabel Z dan dicetak ke layar, sehingga output program adalah "Nilai z = 2".

## Unguided

### Soal 1

copy paste soal nomor 1 disini

```go
package main

func main() {
	fmt.Println("Kode kalian disini")
	fmt.Println("JANGAN MASUKIN >>SCREENSHOT<< KODE KALIAN DISINI")
	fmt.Println("KALAU ADA -20 POIN LAPRAK")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal1.png)
> %% Untuk mencantumkan screenshot, tidak boleh ada spasi di urlnya `()`, penamaan file bebas asal gak sara dan mudah dipahami aja,, dan jangan lupa hapus komen ini yah%%

Penjelasan ttg kode kalian disini

### Soal 2

soal nomor 2A

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2A")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2A.png)

penjelasan kode

Kalau adalanjutan di lanjut disini aja

soal nomor 2B

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2B")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2B.png)

penjelasan bedanya sesuai soal

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)
