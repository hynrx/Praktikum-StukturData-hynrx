# <h1 align="center">LAPORAN PRAKTIKUM MODUL 14 <br> GRAPH </h1>
<p align="center">HISYAM NURDIATMOKO - 103112400049</p>

## Dasar Teori

### GRAPH

Graph didefinisikan sebagai himpunan tidak kosong yang terdiri dari node (atau disebut juga vertex) dan garis penghubung yang disebut edge. Struktur data ini digunakan untuk merepresentasikan hubungan antar objek, di mana node mewakili entitas tertentu, seperti tempat atau lokasi, sedangkan edge mewakili hubungan atau jalan yang menghubungkan entitas-entitas tersebut. Konsep dasar yang penting dalam graph adalah ketetanggaan, di mana suatu node dikatakan bertetangga dengan node lain jika keduanya dihubungkan secara langsung oleh sebuah edge. Edge dalam graph juga dapat memiliki nilai atau bobot yang merepresentasikan jarak, biaya, atau atribut lain dari hubungan tersebut.

Berdasarkan arah hubungannya, graph dibedakan menjadi dua jenis utama, yaitu Graph Berarah (Directed Graph) dan Graph Tidak Berarah (Undirected Graph). Pada Directed Graph, setiap edge memiliki arah yang spesifik, sehingga jika node A terhubung ke node B, belum tentu node B terhubung kembali ke node A. Sebaliknya, pada Undirected Graph, hubungan antar node tidak memiliki arah, yang berarti jika node A terhubung dengan node B, maka secara otomatis terbentuk hubungan timbal balik antara keduanya. Representasi graph di dalam pemrograman dapat dilakukan menggunakan Matrik Ketetanggaan (Array 2 Dimensi) atau Multi Linked List. Dalam praktikum ini, representasi yang digunakan adalah Multi Linked List karena sifatnya yang dinamis dalam menangani penambahan data. Struktur ini melibatkan penggunaan pointer di mana node induk berisi informasi node dan pointer ke node anak atau edge, sementara node anak merepresentasikan hubungan ke node tujuan.

Untuk menelusuri atau mengunjungi node-node di dalam graph, terdapat dua metode pencarian utama, yaitu Breadth First Search (BFS) dan Depth First Search (DFS). BFS bekerja dengan mengunjungi node mulai dari root (kedalaman 0), kemudian menyusur ke seluruh node pada kedalaman 1, kedalaman 2, dan seterusnya secara melebar, yang biasanya diimplementasikan menggunakan struktur data Queue. Sementara itu, DFS bekerja dengan mengunjungi root dan kemudian menelusuri sedalam mungkin ke subtree node tersebut secara rekursif sebelum kembali (backtracking), yang umumnya diimplementasikan menggunakan struktur data Stack. Selain metode penelusuran, terdapat juga konsep Topological Sort, yaitu proses pengurutan linear dari elemen-elemen yang memiliki keterurutan parsial, seperti prasyarat mata kuliah atau urutan pengerjaan tugas dalam sebuah proyek, di mana elemen yang tidak memiliki predecessor akan diproses terlebih dahulu.

## Guided

graf.h
```cpp
#ifndef GRAF_H_INCLUDED
#define GRAF_H_INCLUDED

#include <iostream>
using namespace std;

typedef char infoGraph;

struct ElmNode;
struct ElmEdge;

typedef ElmNode *adrNode;
typedef ElmEdge *adrEdge;

struct ElmNode
{
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode next;
};

struct ElmEdge
{
    adrNode node;
    adrEdge next;
};

struct Graph
{
    adrNode first;
};

// PRIMITIF GRAPH
void CreateGraph(Graph &G);
adrNode AllocateNode(infoGraph X);
adrEdge AllocateEdge(adrNode N);

void InsertNode(Graph &G, infoGraph X);
adrNode FindNode(Graph G, infoGraph X);

void ConnectNode(Graph &G, infoGraph A, infoGraph B);

void PrintInfoGraph(Graph G);

// Traversal
void ResetVisited(Graph &G);
void PrintDFS(Graph &G, adrNode N);
void PrintBFS(Graph &G, adrNode N);

#endif
```

graf.cpp
```cpp
#include "graf.h"
#include <queue>
#include <stack>

void CreateGraph(Graph &G)
{
    G.first = NULL;
}

adrNode AllocateNode(infoGraph X)
{
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->next = NULL;
    return P;
}

adrEdge AllocateEdge(adrNode N)
{
    adrEdge P = new ElmEdge;
    P->node = N;
    P->next = NULL;
    return P;
}

void InsertNode(Graph &G, infoGraph X)
{
    adrNode P = AllocateNode(X);
    P->next = G.first;
    G.first = P;
}

adrNode FindNode(Graph G, infoGraph X)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        if (P->info == X)
            return P;
        P = P->next;
    }
    return NULL;
}

void ConnectNode(Graph &G, infoGraph A, infoGraph B)
{
    adrNode N1 = FindNode(G, A);
    adrNode N2 = FindNode(G, B);

    if (N1 == NULL || N2 == NULL)
    {
        cout << "Node tidak ditemukan!\n";
        return;
    }

    // Buat edge dari N1 ke N2
    adrEdge E1 = AllocateEdge(N2);
    E1->next = N1->firstEdge;
    N1->firstEdge = E1;

    // Karena undirected → buat edge balik
    adrEdge E2 = AllocateEdge(N1);
    E2->next = N2->firstEdge;
    N2->firstEdge = E2;
}

void PrintInfoGraph(Graph G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        cout << P->info << " -> ";
        adrEdge E = P->firstEdge;
        while (E != NULL)
        {
            cout << E->node->info << " ";
            E = E->next;
        }
        cout << endl;
        P = P->next;
    }
}

void ResetVisited(Graph &G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        P->visited = 0;
        P = P->next;
    }
}

void PrintDFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    N->visited = 1;
    cout << N->info << " ";

    adrEdge E = N->firstEdge;
    while (E != NULL)
    {
        if (E->node->visited == 0)
        {
            PrintDFS(G, E->node);
        }
        E = E->next;
    }
}

void PrintBFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    queue<adrNode> Q;
    Q.push(N);

    while (!Q.empty())
    {
        adrNode curr = Q.front();
        Q.pop();

        if (curr->visited == 0)
        {
            curr->visited = 1;
            cout << curr->info << " ";

            adrEdge E = curr->firstEdge;
            while (E != NULL)
            {
                if (E->node->visited == 0)
                {
                    Q.push(E->node);
                }
                E = E->next;
            }
        }
    }
}
```

main.cpp
```cpp
#include "graf.h"
#include <iostream>
using namespace std;

int main()
{
    Graph G;
    CreateGraph(G);

    // Tambah node
    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');

    // Hubungkan node (graph tidak berarah)
    ConnectNode(G, 'A', 'B');
    ConnectNode(G, 'A', 'C');
    ConnectNode(G, 'B', 'D');
    ConnectNode(G, 'C', 'E');

    cout << "=== Struktur Graph ===\n";
    PrintInfoGraph(G);

    cout << "\n=== DFS dari Node A ===\n";
    ResetVisited(G);
    PrintDFS(G, FindNode(G, 'A'));

    cout << "\n\n=== BFS dari Node A ===\n";
    ResetVisited(G);
    PrintBFS(G, FindNode(G, 'A'));

    cout << endl;
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/guided.png)

Program guided ini merupakan implementasi struktur data graf tak berarah (undirected graph) menggunakan representasi adjacency list dalam bahasa C++. Kode ini menyediakan fungsi dasar untuk memanipulasi graf, seperti menambahkan simpul, menghubungkan dua simpul, dan mencari data tertentu. Selain itu, program ini mendemonstrasikan simulasi penelusuran graf menggunakan dua metode traversal utama, yaitu Depth-First Search (DFS) yang bekerja secara rekursif dan Breadth-First Search (BFS) yang memanfaatkan antrean (queue) untuk mengunjungi setiap simpul.

### Unguided

1. Buatlah ADT Binary Search Tree menggunakan Linked list sebagai berikut di dalam file “graph.h”:
```
Type infoGraph: char
Type adrNode : pointer to ElmNode
Type adrEdge : pointer to ElmNode
Type ElmNode <
info : infoGraph
visited : integer
firstEdge : adrEdge
Next : adrNode
>
Type ElmEdge <
Node : adrNode
Next : adrEdge
>
Type Graph <
first : adrNode
>
procedure CreateGraph (input/output G : Graph)
procedure InsertNode (input/output G : Graph,
 input X : infotype)
procedure ConnectNode (input/output N1, N2 : adrNode)
procedure PrintInfoGraph (input G : Graph)
```
Buatlah implementasi ADT Graph pada file “graph.cpp” dan cobalah hasil implementasi ADT
pada file “main.cpp”.

2. Buatlah prosedur untuk menampilkanhasil penelusuran DFS. prosedur PrintDFS (Graph G, adrNode N);

3. Buatlah prosedur untuk menampilkanhasil penelusuran DFS. prosedur PrintBFS (Graph G, adrNode N);

graph.h
```cpp
#ifndef GRAPH_H
#define GRAPH_H
#include <iostream>

using namespace std;

typedef char infoGraph;
typedef struct ElmNode *adrNode;
typedef struct ElmEdge *adrEdge;

struct ElmNode {
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode Next;
};

struct ElmEdge {
    adrNode Node;
    adrEdge Next;
};

struct Graph {
    adrNode first;
};

void CreateGraph(Graph &G);
adrNode AllocateNode(infoGraph X);
adrEdge AllocateEdge(adrNode N);
void InsertNode(Graph &G, infoGraph X);
void ConnectNode(adrNode N1, adrNode N2);
void PrintInfoGraph(Graph G);
adrNode FindNode(Graph G, infoGraph X);
void ResetVisited(Graph &G);
void PrintDFS(Graph G, adrNode N);
void PrintBFS(Graph G, adrNode N);

#endif
```

graph.cpp
```
#include "graph.h"

struct QNode {
    adrNode data;
    QNode *next;
};

struct Queue {
    QNode *head;
    QNode *tail;
};

void createQueue(Queue &Q) {
    Q.head = NULL;
    Q.tail = NULL;
}

bool isEmptyQ(Queue Q) {
    return Q.head == NULL;
}

void enqueue(Queue &Q, adrNode N) {
    QNode *newQ = new QNode;
    newQ->data = N;
    newQ->next = NULL;
    if (isEmptyQ(Q)) {
        Q.head = newQ;
        Q.tail = newQ;
    } else {
        Q.tail->next = newQ;
        Q.tail = newQ;
    }
}

adrNode dequeue(Queue &Q) {
    if (isEmptyQ(Q)) return NULL;
    QNode *temp = Q.head;
    adrNode N = temp->data;
    Q.head = Q.head->next;
    if (Q.head == NULL) {
        Q.tail = NULL;
    }
    delete temp;
    return N;
}

void CreateGraph(Graph &G) {
    G.first = NULL;
}

adrNode AllocateNode(infoGraph X) {
    adrNode N = new ElmNode;
    N->info = X;
    N->visited = 0;
    N->firstEdge = NULL;
    N->Next = NULL;
    return N;
}

adrEdge AllocateEdge(adrNode N) {
    adrEdge E = new ElmEdge;
    E->Node = N;
    E->Next = NULL;
    return E;
}

void InsertNode(Graph &G, infoGraph X) {
    adrNode N = AllocateNode(X);
    if (G.first == NULL) {
        G.first = N;
    } else {
        adrNode P = G.first;
        while (P->Next != NULL) {
            P = P->Next;
        }
        P->Next = N;
    }
}

void ConnectNode(adrNode N1, adrNode N2) {
    if (N1 != NULL && N2 != NULL) {
        adrEdge E1 = AllocateEdge(N2);
        E1->Next = N1->firstEdge;
        N1->firstEdge = E1;

        adrEdge E2 = AllocateEdge(N1);
        E2->Next = N2->firstEdge;
        N2->firstEdge = E2;
    }
}

void PrintInfoGraph(Graph G) {
    adrNode P = G.first;
    while (P != NULL) {
        cout << "Node " << P->info << " terhubung dengan : ";
        adrEdge E = P->firstEdge;
        while (E != NULL) {
            cout << E->Node->info << " ";
            E = E->Next;
        }
        cout << endl;
        P = P->Next;
    }
}

adrNode FindNode(Graph G, infoGraph X) {
    adrNode P = G.first;
    while (P != NULL) {
        if (P->info == X) {
            return P;
        }
        P = P->Next;
    }
    return NULL;
}

void ResetVisited(Graph &G) {
    adrNode P = G.first;
    while (P != NULL) {
        P->visited = 0;
        P = P->Next;
    }
}

void DFS_Helper(adrNode N) {
    if (N == NULL || N->visited == 1) return;
    
    N->visited = 1;
    cout << N->info << " ";
    
    adrEdge E = N->firstEdge;
    while (E != NULL) {
        if (E->Node->visited == 0) {
            DFS_Helper(E->Node);
        }
        E = E->Next;
    }
}

void PrintDFS(Graph G, adrNode N) {
    ResetVisited(G);
    DFS_Helper(N);
    cout << endl;
}

void PrintBFS(Graph G, adrNode N) {
    ResetVisited(G);
    if (N == NULL) return;

    Queue Q;
    createQueue(Q);
    
    enqueue(Q, N);
    N->visited = 1;

    while (!isEmptyQ(Q)) {
        adrNode current = dequeue(Q);
        cout << current->info << " ";

        adrEdge E = current->firstEdge;
        while (E != NULL) {
            if (E->Node->visited == 0) {
                E->Node->visited = 1;
                enqueue(Q, E->Node);
            }
            E = E->Next;
        }
    }
    cout << endl;
}
```

main.cpp
```
#include "graph.h"

int main() {
    Graph G;
    CreateGraph(G);

    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');
    InsertNode(G, 'F');
    InsertNode(G, 'G');
    InsertNode(G, 'H');

    adrNode A = FindNode(G, 'A');
    adrNode B = FindNode(G, 'B');
    adrNode C = FindNode(G, 'C');
    adrNode D = FindNode(G, 'D');
    adrNode E = FindNode(G, 'E');
    adrNode F = FindNode(G, 'F');
    adrNode G_Node = FindNode(G, 'G');
    adrNode H = FindNode(G, 'H');

    ConnectNode(A, B);
    ConnectNode(A, C);
    ConnectNode(B, D);
    ConnectNode(B, E);
    ConnectNode(C, F);
    ConnectNode(C, G_Node);
    ConnectNode(D, H);
    ConnectNode(E, H);
    ConnectNode(F, H);
    ConnectNode(G_Node, H);

    PrintInfoGraph(G);
    cout << endl;

    cout << "DFS TRAVERSAL: ";
    PrintDFS(G, A);

    cout << "BFS TRAVERSAL: ";
    PrintBFS(G, A);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/unguided.png)

Program unguided ini adalah implementasi struktur data Graf tak berarah menggunakan representasi adjacency list dalam bahasa C++. Soal unguided ini mencakup definisi tipe data abstrak untuk node dan edge, serta menyediakan operasi dasar seperti penambahan node, penghubungan antar node, dan penayangan informasi koneksi graf. Selain itu, program ini mengimplementasikan dua algoritma penelusuran utama, yaitu Depth First Search (DFS) secara rekursif dan Breadth First Search (BFS) menggunakan bantuan struktur data queue buatan sendiri, yang didemonstrasikan melalui simulasi koneksi node A hingga H di fungsi utama.

## Referensi

Modul 14: GRAPH [Modul Praktikum]. Telkom University, Bandung.

GeeksforGeeks. (2023). Multi-level Linked List Implementation. https://www.geeksforgeeks.org/flatten-a-linked-list-with-next-and-child-pointers/ Diakses pada 13 Desember 2025



























