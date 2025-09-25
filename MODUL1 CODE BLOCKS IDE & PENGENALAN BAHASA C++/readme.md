
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

program C++ ini bertujuan untuk melakukan sebuah perhitungan aritmatika sederhana dan menampilkan hasilnya ke layar. Kode tersebut pertama-tama mendeklarasikan tiga variabel integer W, X, dan Y yang masing-masing diberi nilai 1, 7, dan 3, serta satu variabel float Z untuk menampung hasil akhir. Operasi utamanya adalah Z = (X + Y) / (Y + W), yang secara matematis menjadi 10 / 4. Karena pembagian ini dilakukan antara dua bilangan bulat, C++ akan melakukan integer division yang hasilnya membuang sisa desimal, sehingga 10 / 4 menghasilkan 2, bukan 2.5. Nilai 2 ini kemudian disimpan ke dalam variabel Z dan dicetak ke layar, sehingga output program adalah "Nilai z = 2"

### Fungsi

```cpp
#include <iostream>
using namespace std;

// Prosedur: hanya menampilkan hasil, tidak mengembalikan nilai
void tampilkanHasil(double p, double l)
{
    cout << "\n=== Hasil Perhitungan ===" << endl;
    cout << "Panjang : " << p << endl;
    cout << "Lebar   : " << l << endl;
    cout << "Luas    : " << p * l << endl;
    cout << "Keliling: " << 2 * (p + l) << endl;
}

// Fungsi: mengembalikan nilai luas
double hitungLuas(double p, double l)
{
    return p * l;
}

// Fungsi: mengembalikan nilai keliling
double hitungKeliling(double p, double l)
{
    return 2 * (p + l);
}

int main()
{
    double panjang, lebar;

    cout << "Masukkan panjang: ";
    cin >> panjang;
    cout << "Masukkan lebar  : ";
    cin >> lebar;

    // Panggil fungsi
    double luas = hitungLuas(panjang, lebar);
    double keliling = hitungKeliling(panjang, lebar);

    cout << "\nDihitung dengan fungsi:" << endl;
    cout << "Luas      = " << luas << endl;
    cout << "Keliling  = " << keliling << endl;

    // Panggil prosedur
    tampilkanHasil(panjang, lebar);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/fungsi.png)

program C++ ini menunjukkan perbedaan antara fungsi (function) dan prosedur (procedure) dengan menghitung luas serta keliling persegi panjang. Program ini meminta pengguna untuk memasukkan nilai panjang dan lebar. Kemudian, program menggunakan dua fungsi terpisah, hitungLuas dan hitungKeliling, yang masing-masing mengembalikan satu nilai (luas dan keliling) untuk disimpan dalam variabel. Hasil dari pemanggilan fungsi ini kemudian ditampilkan ke layar. Setelah itu, program memanggil sebuah prosedur bernama tampilkanHasil yang menerima nilai panjang dan lebar, lalu melakukan semua perhitungan dan menampilkannya langsung di dalam prosedur itu sendiri tanpa mengembalikan nilai apa pun

### Kondisi

```cpp
#include <iostream>
using namespace std;
// int main()
// {
//     double tot_pembelian, diskon;
//     cout << "total pembelian: Rp";
//     cin >> tot_pembelian;
//     diskon = 0;
//     if (tot_pembelian >= 100000)
//         diskon = 0.05 * tot_pembelian;
//     cout << "besar diskon = Rp" << diskon;
// }

// int main()
// {
//     double tot_pembelian, diskon;
//     cout << "total pembelian: Rp";
//     cin >> tot_pembelian;
//     diskon = 0;
//     if (tot_pembelian >= 100000)
//         diskon = 0.05 * tot_pembelian;
//     else
//         diskon = 0;
//     cout << "besar diskon = Rp" << diskon;
// }

int main()
{
    int kode_hari;
    cout << "Menentukan hari kerja/libur\n"<<endl;
    cout << "1=Senin 3=Rabu 5=Jumat 7=Minggu "<<endl;
    cout << "2=Selasa 4=Kamis 6=Sabtu "<<endl;
    cin >> kode_hari;
    switch (kode_hari)
    {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        cout<<"Hari Kerja";
        break;
    case 6:
    case 7:
        cout<<"Hari Libur";
        break;
    default:
        cout<<"Kode masukan salah!!!";
    }
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/kondisi.png)

program C++ ini berfungsi untuk menentukan apakah suatu hari adalah hari kerja atau hari libur berdasarkan kode angka yang dimasukkan oleh pengguna. Awalnya, program akan menampilkan menu pilihan kode hari dari 1 (Senin) hingga 7 (Minggu). Kemudian, program akan meminta pengguna memasukkan sebuah kode hari. Menggunakan struktur switch-case, program akan mengevaluasi kode tersebut. Jika pengguna memasukkan angka 1, 2, 3, 4, atau 5, program akan mengeksekusi case yang sama dan mencetak "Hari Kerja". Jika angka yang dimasukkan adalah 6 atau 7, program akan mencetak "Hari Libur". Jika pengguna memasukkan angka lain di luar rentang 1-7, program akan menjalankan case default dan menampilkan pesan kesalahan "Kode masukan salah!!!"

### Perulangan

```cpp
#include <iostream>
using namespace std;
// int main()
// {
//     int jum;
//     cout << "jumlah perulangan: ";
//     cin >> jum;
//     for (int i = 0; i < jum; i++)
//     {
//         cout << "saya sahroni\n";
//     }
//     return 1;
// }

// while
int main()
{
    int i = 1;
    int jum;
    cin >> jum;
    do
    {
        cout << "bahlil ke-" << (i + 1) << endl;
        i++;
    } while (i < jum);
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/perulangan.png)

program C++ ini menggunakan perulangan do-while untuk mencetak kalimat "bahlil ke-" secara berulang sesuai dengan jumlah yang dimasukkan oleh pengguna. Awalnya, program menginisialisasi variabel i dengan nilai 1, lalu meminta pengguna untuk memasukkan nilai jum (jumlah perulangan). Berbeda dengan loop while biasa, do-while akan menjalankan blok kode di dalamnya **setidaknya satu kali** sebelum memeriksa kondisi while (i < jum). Di setiap iterasi, program akan mencetak "bahlil ke-" diikuti oleh nilai (i + 1) dan menaikkan nilai i. Perulangan akan terus berlanjut selama nilai i masih lebih kecil dari jum

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
