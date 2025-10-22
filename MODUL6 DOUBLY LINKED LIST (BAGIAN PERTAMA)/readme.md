# <h1 align="center">LAPORAN PRAKTIKUM MODUL 6 <br> DOUBLY LINKED LIST (BAGIAN PERTAMA)</h1>
<p align="center">HISYAM NURDIATMOKO - 103112400049</p>

## Dasar Teori

### Doubly Linked List

Doubly Linked List adalah sebuah senarai berantai di mana setiap elemennya memiliki dua suksesor, yaitu penunjuk ke elemen sebelumnya (prev) dan penunjuk ke elemen sesudahnya (next). Struktur ini juga menggunakan dua penunjuk utama, yaitu first yang menunjuk ke elemen pertama dan last yang menunjuk ke elemen terakhir. Setiap elemen terdiri dari tiga bagian: info untuk menyimpan data, penunjuk next, dan penunjuk prev. Keunggulan dari struktur ini adalah kemudahan dalam melakukan proses akses elemen karena dapat melakukan iterasi maju maupun mundur. Sebuah Doubly Linked List dianggap kosong jika penunjuk first bernilai Nil.

## Guided

### Guided 1

#### doublylinkedlist.cpp

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

void insertDepan(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->prev = nullptr;
    newNode->next = head;

    if (head != nullptr)
        head->prev = newNode;
    else
        tail = newNode;

    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan.\n";
}

void insertBelakang(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    newNode->prev = tail;

    if (tail != nullptr)
        tail->next = newNode;
    else
        head = newNode;

    tail = newNode;
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int data) {
    Node* current = head;
    while (current != nullptr && current->data != target)
        current = current->next;
    
    if (current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = current->next;
    newNode->prev = current;

    if (current->next != nullptr)
        current->next->prev = newNode;
    else
        tail = newNode;

    current->next = newNode;
    cout << "Data " << data << " berhasil disisipkan setelah " << target << ".\n";
}

void hapusDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = head;
    head = head->next;

    if (head != nullptr)
        head->prev = nullptr;
    else
        tail = nullptr;

    cout << "Data " << temp->data << " dihapus dari depan.\n";
    delete temp;
}

void hapusBelakang() {
    if (tail = nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = tail;
    tail = tail->prev;

    if (tail != nullptr)
        tail->next = nullptr;
    else
        head = nullptr;

    cout << "Data " << temp->data << " dihapus dari belakang.\n";
    delete temp;
}

void hapusData(int target) {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* current = head;
    while (current != nullptr && current->data != target)
        current = current->next;

    if (current == head)
        hapusDepan();
    else if (current == tail)
        hapusBelakang();
    else {
        current->prev->next = current->next;
        current->next->prev = current->prev;
        cout << "Data " << target << " dihapus.\n";
        delete current;
    }
}

void updateData(int oldData, int newData) {
    Node* current = head;
    while (current != nullptr && current->data != oldData)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << oldData << " tidak ditemukan.\n";
        return;
    }

    current->data = newData;
    cout << "Data " << oldData << " diubah menjadi " << newData << ".\n";
}

void tampilDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari depan): ";
    Node* current = head;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->next;
    }
    cout << "\n";
}

// ====================================
// Fungsi: Tampilkan dari belakang
// ====================================
void tampilBelakang() {
    if (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari belakang): ";
    Node* current = tail;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->prev;
    }
    cout << "\n";
}

// ====================================
// MAIN PROGRAM (MENU INTERAKTIF)
// ====================================
int main() {
    int pilihan, data, target, oldData, newData;

    do {
        cout << "\n===== MENU DOUBLE LINKED LIST =====\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah Data\n";
        cout << "4. Hapus Depan\n";
        cout << "5. Hapus Belakang\n";
        cout << "6. Hapus Data Tertentu\n";
        cout << "7. Update Data\n";
        cout << "8. Tampil dari Depan\n";
        cout << "9. Tampil dari Belakang\n";
        cout << "0. Keluar\n";
        cout << "===================================\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> data;
                insertSetelah(target, data);
                break;
            case 4:
                hapusDepan();
                break;
            case 5:
                hapusBelakang();
                break;
            case 6:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> target;
                hapusData(target);
                break;
            case 7:
                cout << "Masukkan data lama: ";
                cin >> oldData;
                cout << "Masukkan data baru: ";
                cin >> newData;
                updateData(oldData, newData);
                break;
            case 8:
                tampilDepan();
                break;
            case 9:
                tampilBelakang();
                break;
            case 0:
                cout << "👋 Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }

    } while (pilihan != 0);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/guided.png)

program C++ ini adalah implementasi dari struktur data doubly linked list yang memungkinkan pengelolaan data secara dinamis. Melalui menu interaktif berbasis teks, pengguna dapat melakukan berbagai operasi dasar seperti menambah data (di depan, di belakang, atau setelah data lain), menghapus data (dari depan, belakang, atau data spesifik), dan memperbarui data. Keunikan dari doubly linked list ini ditunjukkan dengan adanya fungsi untuk menampilkan isi list dari dua arah, yaitu dari depan ke belakang (head ke tail) dan dari belakang ke depan (tail ke head), yang dimungkinkan karena setiap elemen (node) memiliki penunjuk ke elemen sebelum (prev) dan sesudahnya (next).

## Unguided

### Soal 1

buatlah searcing untuk mencari nama pembeli pada unguided sebelumnya

```cpp
#include <iostream>
#include <string>

using namespace std;

struct Pembeli {
    string nama;
    string pesanan;
};

struct Node {
    Pembeli data;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

Node* createNode(Pembeli data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}

void tambahAntrian(Pembeli data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
        tail = newNode;
    } else {
        tail->next = newNode;
        tail = newNode;
    }
    cout << "pembeli \"" << data.nama << "\" berhasil ditambahkan ke antrian.\n";
}

void layaniAntrian() {
    if (head == nullptr) {
        cout << "antrian kosong.\n";
        return;
    }

    Node* temp = head;
    cout << "melayani \"" << temp->data.nama << "\" dengan pesanan \"" << temp->data.pesanan << "\".\n";

    head = head->next;
    delete temp;

    if (head == nullptr) {
        tail = nullptr;
    }
}

void tampilkanAntrian() {
    if (head == nullptr) {
        cout << "antrian kosong!\n";
        return;
    }

    Node* temp = head;
    cout << "isi antrian saat ini:\n";
    int nomor = 1;
    while (temp != nullptr) {
        cout << nomor << ". nama: " << temp->data.nama << ", pesanan: " << temp->data.pesanan << "\n";
        temp = temp->next;
        nomor++;
    }
}

void cariPembeli(string namaDicari) {
    if (head == nullptr) {
        cout << "antrian kosong!\n";
        return;
    }

    Node* temp = head;
    int posisi = 1;
    bool ditemukan = false;

    while (temp != nullptr) {
        if (temp->data.nama == namaDicari) {
            cout << "pembeli ditemukan pada antrian ke-" << posisi << ":\n";
            cout << "  -> nama: " << temp->data.nama << ", pesanan: " << temp->data.pesanan << "\n";
            ditemukan = true;
        }
        temp = temp->next;
        posisi++;
    }

    if (!ditemukan) {
        cout << "pembeli dengan nama \"" << namaDicari << "\" tidak ditemukan di antrian\n";
    }
}

int main() {
    int pilihan;
    Pembeli dataPembeli;

    do {
        cout << "\nMENU ANTRIAN\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Antrian\n";
        cout << "3. Tampilkan Antrian\n";
        cout << "4. Cari Pembeli\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "masukkan nama pembeli: ";
                cin.ignore();
                getline(cin, dataPembeli.nama);
                cout << "masukkan pesanan: ";
                getline(cin, dataPembeli.pesanan);
                tambahAntrian(dataPembeli);
                break;
            case 2:
                layaniAntrian();
                break;
            case 3:
                tampilkanAntrian();
                break;
            case 4: {
                if (head == nullptr) {
                    cout << "antrian kosong\n";
                } else {
                    string namaDicari;
                    cout << "masukkan nama pembeli yang ingin dicari: ";
                    cin.ignore();
                    getline(cin, namaDicari);
                    cariPembeli(namaDicari);
                }
                break;
            }
            case 0:
                cout << "tengkyu\n";
                break;
            default:
                cout << "pilihan tidak valdi\n";
        }
    } while (pilihan != 0);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/soal1.png)

program C++ ini merupakan implementasi dari sistem antrean (queue) menggunakan struktur data singly linked list untuk mengelola data pembeli dan pesanan mereka. Program ini bekerja berdasarkan prinsip First-In, First-Out (FIFO), di mana pembeli yang pertama datang akan dilayani terlebih dahulu. Melalui menu interaktif, pengguna dapat melakukan beberapa operasi dasar seperti menambahkan pembeli baru ke akhir antrean (tambahAntrian), melayani (menghapus) pembeli dari awal antrean (layaniAntrian), menampilkan seluruh daftar antrean saat ini (tampilkanAntrian), serta mencari pembeli spesifik berdasarkan nama di dalam antrean.

### Soal 2

gunakan latihan pada pertemuan minggun ini dan tambahkan seardhing untuk mencari buku berdasarkan judul, penulis, dan ISBN

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Buku {
    string isbn;
    string judul;
    string penulis;
};

struct Node {
    Buku data;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

Node* createNode(Buku data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}

void tambahBuku(Buku data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
        tail = newNode;
    } else {
        tail->next = newNode;
        tail = newNode;
    }
    cout << "buku judul \"" << data.judul << "\" berhasil ditambahkan" << endl;
}

void hapusBuku(string isbn) {
    if (head == nullptr) {
        cout << "daftar buku kosong" << endl;
        return;
    }

    Node* temp = head;
    Node* prev = nullptr;

    if (temp != nullptr && temp->data.isbn == isbn) {
        head = temp->next;
        if (head == nullptr) {
            tail = nullptr;
        }
        cout << "buku dengan ISBN " << temp->data.isbn << " berhasil dihapus" << endl;
        delete temp;
        return;
    }

    while (temp != nullptr && temp->data.isbn != isbn) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "buku dengan ISBN " << isbn << " tidak ditemukan" << endl;
        return;
    }

    prev->next = temp->next;

    if (prev->next == nullptr) {
        tail = prev;
    }
    
    cout << "buku dengan ISBN " << temp->data.isbn << " berhasil dihapus" << endl;
    delete temp;
}

void perbaruiBuku(string isbn) {
     if (head == nullptr) {
        cout << "daftar buku kosong" << endl;
        return;
    }
    
    Node* temp = head;
    bool ditemukan = false;
    
    while (temp != nullptr) {
        if (temp->data.isbn == isbn) {
            cout << "masukkan judul buku baru: ";
            cin.ignore();
            getline(cin, temp->data.judul);
            cout << "masukkan penulis buku baru: ";
            getline(cin, temp->data.penulis);
            cout << "data buku dengan ISBN " << isbn << " berhasil diperbarui" << endl;
            ditemukan = true;
            break;
        }
        temp = temp->next;
    }
    
    if (!ditemukan) {
        cout << "buku dengan ISBN " << isbn << " tidak ditemukan" << endl;
    }
}

void lihatBuku() {
    if (head == nullptr) {
        cout << "daftar buku kosong" << endl;
        return;
    }

    Node* temp = head;
    cout << "\ndaftar Buku:\n";
    int nomor = 1;
    while (temp != nullptr) {
        cout << nomor << ". ISBN     : " << temp->data.isbn << "\n";
        cout << "   Judul    : " << temp->data.judul << "\n";
        cout << "   Penulis  : " << temp->data.penulis << "\n\n";
        temp = temp->next;
        nomor++;
    }
}

void cariBuku() {
    if (head == nullptr) {
        cout << "daftar buku kosong" << endl;
        return;
    }

    int pilihanCari;
    string query;
    cout << "\ncari buku berdasarkan\n";
    cout << "1. ISBN\n";
    cout << "2. Judul\n";
    cout << "3. Penulis\n";
    cout << "pilih: ";
    cin >> pilihanCari;
    
    cout << "masukkan kata kunci pencarian: ";
    cin.ignore();
    getline(cin, query);

    Node* temp = head;
    bool ditemukan = false;
    int nomor = 1;

    cout << "\nhasil pencarian:\n";
    while (temp != nullptr) {
        bool cocok = false;
        switch (pilihanCari) {
            case 1:
                if (temp->data.isbn == query) {
                    cocok = true;
                }
                break;
            case 2:
                if (temp->data.judul.find(query) != string::npos) {
                    cocok = true;
                }
                break;
            case 3:
                if (temp->data.penulis.find(query) != string::npos) {
                    cocok = true;
                }
                break;
            default:
                cout << "pilihan pencarian tidak valdi" << endl;
                return;
        }

        if (cocok) {
            if (!ditemukan) {
                 cout << "buku ditemukan:\n\n";
            }
            cout << nomor << ". ISBN     : " << temp->data.isbn << "\n";
            cout << "   Judul    : " << temp->data.judul << "\n";
            cout << "   Penulis  : " << temp->data.penulis << "\n\n";
            ditemukan = true;
            nomor++;
        }
        temp = temp->next;
    }

    if (!ditemukan) {
        cout << "buku dengan kata kunci \"" << query << "\" tidak ada" << endl;
    }
}

int main() {
    int pilihan;
    Buku dataBuku;
    string isbn;

    while (true) {
        cout << "\nMENU PERPUSTAKAAN\n";
        cout << "1. Tambah Buku\n";
        cout << "2. Hapus Buku\n";
        cout << "3. Perbarui Buku\n";
        cout << "4. Lihat Daftar Buku\n";
        cout << "5. Cari Buku\n";
        cout << "6. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "masukkan ISBN: ";
                cin >> dataBuku.isbn;
                cout << "masukkan judul: ";
                cin.ignore(); 
                getline(cin, dataBuku.judul);
                cout << "masukkan penulis: ";
                getline(cin, dataBuku.penulis);
                tambahBuku(dataBuku);
                break;
            case 2:
                cout << "masukkan ISBN buku yang akan dihapus: ";
                cin >> isbn;
                hapusBuku(isbn);
                break;
            case 3:
                cout << "masukkan ISBN buku yang akan diperbarui: ";
                cin >> isbn;
                perbaruiBuku(isbn);
                break;
            case 4:
                lihatBuku();
                break;
            case 5:
                cariBuku();
                break;
            case 6:
                cout << "Ttengkyuu" << endl;
                return 0;
            default:
                cout << "pilihan tidak valdi" << endl;
        }
    }

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/soal2.png)

program C++ ini adalah sebuah sistem manajemen perpustakaan sederhana yang menggunakan struktur data singly linked list untuk mengelola koleksi buku. Melalui antarmuka menu berbasis teks, pengguna dapat melakukan operasi dasar seperti menambahkan buku baru ke dalam daftar, menghapus buku berdasarkan ISBN, memperbarui detail buku (judul dan penulis) yang sudah ada, serta menampilkan keseluruhan daftar buku. Selain itu, program ini juga menyediakan fitur pencarian buku yang fleksibel, memungkinkan pengguna untuk menemukan buku berdasarkan ISBN, judul, atau nama penulis.

## Referensi

Modul 5: Singly Linked List (Bagian Kedua) [Modul Praktikum]. Telkom University, Bandung.

[GeeksforGeeks. (2024). Singly Linked List.](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/) Diakses pada 18 Oktober 2025





