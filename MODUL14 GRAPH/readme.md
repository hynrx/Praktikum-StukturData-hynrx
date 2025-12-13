# <h1 align="center">LAPORAN PRAKTIKUM MODUL 14 <br> GRAPH </h1>
<p align="center">HISYAM NURDIATMOKO - 103112400049</p>

## Dasar Teori

### GRAPH

Multi Linked List merupakan sebuah struktur data dinamis yang terdiri dari sekumpulan list yang berbeda namun memiliki keterhubungan satu sama lain. Dalam struktur ini, setiap elemen di dalam list memiliki kemampuan untuk membentuk list tersendiri, yang secara umum dikategorikan menjadi dua bagian utama, yaitu list induk (parent) dan list anak (child). Implementasi dari struktur ini dapat dilihat pada kasus data kepegawaian, di mana terdapat list pegawai sebagai list induk yang menunjuk pada satu buah list anak, sehingga menciptakan relasi data yang terstruktur antara entitas utama dan sub-entitasnya.

Dalam pengoperasian manipulasi data, Multi Linked List memiliki prosedur khusus terutama pada operasi penyisipan (insert) dan penghapusan (delete). Untuk operasi penambahan elemen induk, konsep yang digunakan sama dengan operasi insert pada struktur data Singly, Doubly, maupun Circular Linked List pada umumnya. Berbeda halnya dengan penambahan elemen anak, di mana proses ini mewajibkan program untuk mengetahui atau mencari posisi elemen induknya terlebih dahulu sebelum elemen anak baru dapat disisipkan ke dalam list yang sesuai.

Aturan ketergantungan yang ketat juga berlaku pada operasi penghapusan data. Sama seperti proses insert, penghapusan elemen anak mengharuskan identifikasi terhadap elemen induknya agar pointer dapat diakses dengan tepat. Selain itu, terdapat aturan krusial pada penghapusan elemen induk; apabila sebuah elemen induk dihapus, maka seluruh elemen anak yang bernaung di bawah induk tersebut juga harus ikut dihapus. Hal ini memastikan bahwa tidak ada data anak yang tertinggal tanpa induk (dangling) yang dapat menyebabkan inkonsistensi data dalam memori.

## Guided

#### main.cpp

```cpp
#include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }
    
    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
     cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;
    
    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");
    
    printAll(list);
    cout << "\n";
    
    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");
    
    printAll(list);
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/guided.png)

Program Guided MULTI LINKED LIST ini merupakan implementasi sederhana dari struktur data Multi Linked List menggunakan bahasa C++, yang dirancang untuk merepresentasikan relasi hierarkis one-to-many antara simpul induk (ParentNode) dan simpul anak (ChildNode). Melalui penggunaan dua struktur data yang saling terhubung pointer, program ini memfasilitasi penambahan elemen induk ke dalam senarai utama serta memungkinkan penyisipan elemen anak secara spesifik di bawah induk yang sesuai berdasarkan pencarian nilai string-nya. Keseluruhan logika program diakhiri dengan fungsi traversal yang mencetak setiap induk diikuti oleh seluruh rangkaian anak yang dimilikinya secara berurutan, memvisualisasikan hubungan keterkaitan data tersebut.

### Unguided

Implementasikan ADT Multi Linked List dan ADT Linked List untuk studi kasus data mahasiswa (Nama, NIM, Jenis Kelamin, IPK) beserta seluruh operasi manipulasi data (insert, delete, find, print) menggunakan bahasa C++ sesuai spesifikasi header yang diberikan.

multilist.h
```cpp
#ifndef CIRCULARLIST_H
#define CIRCULARLIST_H

#include <iostream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    char jenis_kelamin;
    float ipk;
};

typedef Mahasiswa infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address first;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address P);
void insertFirst(List &L, address P);
void insertLast(List &L, address P);
void insertAfter(List &L, address Prec, address P);
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
address findElm(List L, string nim);
void printInfo(List L);

address createData(string nama, string nim, char jenis_kelamin, float ipk);

#endif
```

multilist.cpp
```
#include "multilist.h"

void createList(List &L) {
    L.first = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    return P;
}

void dealokasi(address P) {
    delete P;
}

address createData(string nama, string nim, char jenis_kelamin, float ipk) {
    infotype x;
    x.nama = nama;
    x.nim = nim;
    x.jenis_kelamin = jenis_kelamin;
    x.ipk = ipk;
    return alokasi(x);
}

void insertFirst(List &L, address P) {
    if (L.first == NULL) {
        L.first = P;
        P->next = L.first;
    } else {
        address last = L.first;
        while (last->next != L.first) {
            last = last->next;
        }
        P->next = L.first;
        last->next = P;
        L.first = P;
    }
}

void insertLast(List &L, address P) {
    if (L.first == NULL) {
        insertFirst(L, P);
    } else {
        address last = L.first;
        while (last->next != L.first) {
            last = last->next;
        }
        last->next = P;
        P->next = L.first;
    }
}

void insertAfter(List &L, address Prec, address P) {
    if (Prec != NULL) {
        P->next = Prec->next;
        Prec->next = P;
    }
}

void deleteFirst(List &L, address &P) {
    if (L.first == NULL) {
        P = NULL;
    } else if (L.first->next == L.first) {
        P = L.first;
        L.first = NULL;
    } else {
        address last = L.first;
        while (last->next != L.first) {
            last = last->next;
        }
        P = L.first;
        L.first = P->next;
        last->next = L.first;
        P->next = NULL;
    }
}

void deleteLast(List &L, address &P) {
    if (L.first == NULL) {
        P = NULL;
    } else if (L.first->next == L.first) {
        deleteFirst(L, P);
    } else {
        address last = L.first;
        address prevLast = NULL;
        while (last->next != L.first) {
            prevLast = last;
            last = last->next;
        }
        P = last;
        prevLast->next = L.first;
        P->next = NULL;
    }
}

void deleteAfter(List &L, address Prec, address &P) {
    if (Prec != NULL && Prec->next != L.first) {
        P = Prec->next;
        Prec->next = P->next;
        P->next = NULL;
    } else if (Prec != NULL && Prec->next == L.first) {
        deleteFirst(L, P);
    }
}

address findElm(List L, string nim) {
    if (L.first == NULL) return NULL;
    
    address P = L.first;
    do {
        if (P->info.nim == nim) {
            return P;
        }
        P = P->next;
    } while (P != L.first);
    
    return NULL;
}

void printInfo(List L) {
    if (L.first == NULL) {
        cout << "List Kosong" << endl;
        return;
    }
    
    address P = L.first;
    do {
        cout << "Nama\t: " << P->info.nama << endl;
        cout << "NIM\t: " << P->info.nim << endl;
        cout << "L/P\t: " << P->info.jenis_kelamin << endl;
        cout << "IPK\t: " << P->info.ipk << endl;
        cout << "       " << endl;
        P = P->next;
    } while (P != L.first);
}
```

main.cpp
```
#include "multilist.h"

int main() {
    List L;
    address P1 = NULL;
    address P2 = NULL;
    infotype x;

    createList(L);
    
    cout << "coba insert first, last, dan after" << endl;

    P1 = createData("Danu", "04", 'L', 4.0);
    insertFirst(L, P1);

    P1 = createData("Fahmi", "06", 'L', 3.45);
    insertLast(L, P1);

    P1 = createData("Bobi", "02", 'L', 3.71);
    insertLast(L, P1); 

    P1 = createData("Ali", "01", 'L', 3.3);
    insertFirst(L, P1);

    P1 = createData("Gita", "07", 'P', 3.75);
    insertLast(L, P1); 

    address foundNode = findElm(L, "07");
    if (foundNode != NULL) {
        P2 = createData("Cindi", "03", 'P', 3.5);
        insertAfter(L, foundNode, P2);
    }

    foundNode = findElm(L, "02");
    if (foundNode != NULL) {
        P2 = createData("Hilmi", "08", 'L', 3.3);
        insertAfter(L, foundNode, P2);
    }
    
    foundNode = findElm(L, "04");
    if (foundNode != NULL) {
        P2 = createData("Eli", "05", 'P', 3.4);
        insertAfter(L, foundNode, P2);
    }
    printInfo(L);
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/unguided.png)

Program Unguided ini merupakan implementasi penyelesaian soal latihan pada Modul 13 Multi Linked List, di mana praktikan diminta membangun struktur data Circular Single Linked List untuk studi kasus data mahasiswa. Sesuai spesifikasi latihan, program ini tidak membentuk hierarki parent-child (multi list), melainkan menyusun data mahasiswa (Nama, NIM, Jenis Kelamin, IPK) dalam satu rangkaian list melingkar (circular) di mana pointer elemen terakhir kembali menunjuk ke elemen pertama. Seluruh operasi manipulasi data seperti insert, delete, dan search dikemas dalam ADT yang membagi kode menjadi bagian deklarasi, implementasi, dan pengujian utama sesuai standar pemrograman modular.

## Referensi

Modul 13: MULTI LINKED LIST [Modul Praktikum]. Telkom University, Bandung.

GeeksforGeeks. (2024). Singly Linked List. Diakses pada 4 Desember 2025

GeeksforGeeks. (2023). Multi-level Linked List Implementation. https://www.geeksforgeeks.org/flatten-a-linked-list-with-next-and-child-pointers/ Diakses pada 4 Desember 2025























