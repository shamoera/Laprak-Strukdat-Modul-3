# <h1 align="center">Laporan Praktikum Modul 3 - Abstract Data Type</h1>
<p align="center">Shafira Shifa Azahra - 109082500125</p>

## Dasar Teori
## A. Abstract Data Type (ADT)<br/>

ADT adalah sebuah TYPE beserta sekumpulan PRIMITIF (operasi dasar) terhadap TYPE tersebut. Pada ADT yang lengkap, disertakan juga definisi invarian dari TYPE dan aksioma yang berlaku, dan ADT merupakan definisi yang bersifat statik [1]. Definisi type dari sebuah ADT dapat mengandung ADT lain, misalnya ADT waktu yang terdiri dari ADT JAM dan ADT DATE, atau garis yang terdiri dari dua buah ADT POINT [1].

1. Type

Pada bahasa C/C++, TYPE diterjemahkan menjadi tipe yang terdefinisi dalam bahasa tersebut, misalnya struct. Seluruh variabel yang bertipe tersebut dibentuk melalui konstruktor [1].

2. Primitif

Primitif adalah operasi dasar terhadap type, yang dalam konteks prosedural diterjemahkan menjadi fungsi atau prosedur [1].

3. Struktur Implementasi

ADT diimplementasikan menjadi dua modul utama dan satu modul interface program utama (driver) [1].

## B. Pengelompokan Primitif ADT<br/>

Primitif dalam ADT dikelompokkan menjadi konstruktor/kreator, selector, prosedur pengubah nilai komponen, validator komponen, destruktor/dealokator, baca/tulis, operator relasional, aritmatika, dan konversi tipe [1].

1. Konstruktor/Kreator

Membentuk nilai bertipe ADT, biasanya namanya diawali Make atau create.

2. Selector

Mengakses komponen dari tipe, biasanya namanya diawali Get.

3. Baca/Tulis

Berfungsi sebagai antarmuka dengan perangkat input dan output, misalnya prosedur untuk menampilkan isi sebuah tipe.

## C. Modul pada ADT<br/>

Penerapan ADT memisahkan program ke dalam tiga bagian [1].

1. File Header (.h)

Berisi spesifikasi type dan header dari primitif (fungsi atau prosedur).

2. File Body/Realisasi (.cpp)

Berisi kode realisasi dari primitif yang dideklarasikan pada file header.

3. File Driver (main.cpp)

Berisi program utama yang memanggil primitif dari ADT.

## D. Array 2D dan Pointer<br/>

Array 2D adalah kumpulan elemen bertipe sama yang diakses dengan dua indeks (baris dan kolom). Pointer adalah variabel yang menyimpan alamat memori dari variabel lain, dan isi variabel yang ditunjuk dapat diakses dengan operator dereferensi (*).

## Guided 

### 1. mahasiswa.cpp

```C++
#include <iostream>
#include "mahasiswa.h"

using namespace std;

void inputMhs(mahasiswa &m) {
    cout << "input nama = ";
    cin >> (m).nim;
    cout << "input nilai = ";
    cin >> (m).nilai1;
    cout << "input nilai2 = ";
    cin >> (m).nilai2;
} 

float rata2(mahasiswa m) {
    return float(m.nilai1+m.nilai2)/2;
}
```
File ini berisi kode dari dua fungsi yang dideklarasikan di mahasiswa.h. Prosedur inputMhs meminta pengguna mengetik nim, nilai1, dan nilai2. Fungsi rata2 menjumlahkan kedua nilai lalu membaginya dua. Penulisan float(...) dipakai supaya hasilnya bisa berkoma, misalnya 82.5, dan tidak dibulatkan.

### 2. mahasiswa.h

```C++
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED
struct mahasiswa{
    char nim[10];
    int nilai1, nilai2;
};

void inputMhs (mahasiswa &m) ;
float rata2 (mahasiswa m) ;
#endif // MAHASISWA_H_INCLUDED
```
File ini berisi type mahasiswa yang punya tiga data: nim, nilai1, dan nilai2. Di bawahnya ada prosedur inputMhs untuk mengisi data dan fungsi rata2 untuk menghitung rata-rata dua nilai. Tanda & pada inputMhs membuat data yang diisi di dalam prosedur ikut tersimpan di variabel aslinya. Baris #ifndef, #define, dan #endif berfungsi agar file ini tidak terbaca dua kali saat dikompilasi.

### 3. main.cpp

```C++
#include <iostream>
#include "mahasiswa.h"

using namespace std;

int main()
{
    mahasiswa mhs;
    inputMhs (mhs) ;
    cout << "rata-rata = " << rata2 (mhs) ;
    return 0;
}
```
Ini adalah program utamanya. Di sini dibuat variabel mhs bertipe mahasiswa, diisi lewat inputMhs, lalu rata-ratanya ditampilkan dengan rata2. Agar ketiga file bisa jalan bersama, kompilasinya memakai perintah g++ main.cpp mahasiswa.cpp -o main.

## Unguided 

### 1. Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI dengan rumus 0.3uts+0.4uas+0.3*tugas.

```C++
#include <iostream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts, uas, tugas;
    float nilaiAkhir;
};

// FUNGSI penghitung nilai akhir
float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return 0.3f * uts + 0.4f * uas + 0.3f * tugas;
}

int main() {
    Mahasiswa mhs[10];
    int n;

    do {
        cout << "Jumlah mahasiswa (1-10): ";
        cin >> n;
    } while (n < 1 || n > 10);
    cin.ignore();                      // buang sisa newline sebelum getline

    for (int i = 0; i < n; i++) {
        cout << "\nMahasiswa ke-" << i + 1 << endl;
        cout << "Nama  : "; getline(cin, mhs[i].nama);
        cout << "NIM   : "; cin >> mhs[i].nim;
        cout << "UTS   : "; cin >> mhs[i].uts;
        cout << "UAS   : "; cin >> mhs[i].uas;
        cout << "Tugas : "; cin >> mhs[i].tugas;
        cin.ignore();                  // buang newline untuk getline berikutnya

        mhs[i].nilaiAkhir = hitungNilaiAkhir(mhs[i].uts, mhs[i].uas, mhs[i].tugas);
    }

    cout << "\n=== Data Mahasiswa ===\n";
    for (int i = 0; i < n; i++) {
        cout << i + 1 << ". " << mhs[i].nama << " | " << mhs[i].nim
             << " | UTS: " << mhs[i].uts
             << " | UAS: " << mhs[i].uas
             << " | Tugas: " << mhs[i].tugas
             << " | Nilai Akhir: " << mhs[i].nilaiAkhir << endl;
    }
    return 0;
}
```
### Output Unguided 1 :

##### Output 
![Screenshot Output Unguided 1_1](https://github.com/shamoera/Laprak-Strukdat-Modul-3/blob/main/soal1.png)


Program ini menyimpan data mahasiswa dalam array mhs yang muat 10 data. Setiap data berupa struct Mahasiswa yang berisi nama, nim, uts, uas, tugas, dan nilai akhir. Jumlah mahasiswa yang diinput dibatasi 1 sampai 10 memakai do-while. Nilai akhir dihitung oleh fungsi hitungNilaiAkhir dengan rumus 0.3uts + 0.4uas + 0.3*tugas, jadi bukan dihitung langsung di main. Perintah cin.ignore() dipakai supaya getline untuk nama tidak terlewat karena ada sisa tombol Enter di input sebelumnya. Contohnya, UTS 80, UAS 90, dan tugas 100 menghasilkan nilai akhir 24 + 36 + 30 = 90. 

### 2. Buatlah ADT pelajaran sebagai berikut di dalam file "pelajaran.h", buat implementasinya pada file "pelajaran.cpp", dan cobalah pada file "main.cpp".

## pelajaran.cpp
```C++
#include "pelajaran.h"

pelajaran create_pelajaran(string namapel, string kodepel) {
    pelajaran p;
    p.namaMapel = namapel;
    p.kodeMapel = kodepel;
    return p;
}

void tampil_pelajaran(pelajaran pel) {
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}
```
## pelajaran.h
```C++
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED

#include <iostream>
#include <string>
using namespace std;

struct pelajaran {
    string namaMapel;
    string kodeMapel;
};

pelajaran create_pelajaran(string namapel, string kodepel);

void tampil_pelajaran(pelajaran pel);

#endif 
```
## main.cpp
```C++
#include "pelajaran.h"
using namespace std;

int main() {
    string namapel = "Struktur Data";
    string kodepel = "STD";
    pelajaran pel = create_pelajaran(namapel, kodepel);
    tampil_pelajaran(pel);

    return 0;
}
```
### Output Unguided 2 :

##### Output 
![Screenshot Output Unguided 2_1](https://github.com/shamoera/Laprak-Strukdat-Modul-3/blob/main/soal2.png)


Soal ini memakai konsep ADT, jadi programnya dipecah jadi tiga file. File pelajaran.h berisi type pelajaran (punya namaMapel dan kodeMapel) serta deklarasi fungsi create_pelajaran dan prosedur tampil_pelajaran. File pelajaran.cpp berisi kode lengkapnya: create_pelajaran membuat data pelajaran dari nama dan kode yang diberikan, sedangkan tampil_pelajaran menampilkannya ke layar. File main.cpp membuat data pelajaran "Struktur Data" dengan kode "STD"

### 3. Buatlah program dengan 2 buah array 2D integer berukuran 3x3 dan 2 buah pointer integer, fungsi/prosedur yang menampilkan isi sebuah array 2D, fungsi/prosedur yang menukarkan isi dari 2 array 2D pada posisi tertentu, dan fungsi/prosedur yang menukarkan isi variabel yang ditunjuk oleh 2 buah pointer.

```C++
#include <iostream>
using namespace std;

// Menampilkan isi sebuah array 2D 3x3
void tampilArray(int arr[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << arr[i][j] << "\t";
        }
        cout << endl;
    }
}

// Menukar isi array A dan B pada posisi (baris, kolom)
void tukarArray(int A[3][3], int B[3][3], int baris, int kolom) {
    int temp = A[baris][kolom];
    A[baris][kolom] = B[baris][kolom];
    B[baris][kolom] = temp;
}

// Menukar isi variabel yang ditunjuk oleh 2 pointer
void tukarPointer(int *p1, int *p2) {
    int temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}

int main() {
    int A[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    int B[3][3] = {{10, 20, 30}, {40, 50, 60}, {70, 80, 90}};
    int *p1, *p2;

    cout << "=== Kondisi Awal ===" << endl;
    cout << "Array A:" << endl; tampilArray(A);
    cout << "Array B:" << endl; tampilArray(B);

    // --- Menukar isi A dan B pada posisi tertentu ---
    int baris, kolom;
    do {
        cout << "\nMasukkan posisi yang ditukar (baris kolom, 0-2): ";
        cin >> baris >> kolom;
    } while (baris < 0 || baris > 2 || kolom < 0 || kolom > 2);

    tukarArray(A, B, baris, kolom);

    cout << "\n=== Setelah tukarArray pada posisi ["
         << baris << "][" << kolom << "] ===" << endl;
    cout << "Array A:" << endl; tampilArray(A);
    cout << "Array B:" << endl; tampilArray(B);

    // --- Menukar isi variabel yang ditunjuk 2 pointer ---
    p1 = &A[0][0];
    p2 = &B[2][2];

    cout << "\nSebelum tukarPointer: *p1 = " << *p1 << ", *p2 = " << *p2 << endl;
    tukarPointer(p1, p2);
    cout << "Sesudah tukarPointer: *p1 = " << *p1 << ", *p2 = " << *p2 << endl;

    cout << "\n=== Kondisi Akhir ===" << endl;
    cout << "Array A:" << endl; tampilArray(A);
    cout << "Array B:" << endl; tampilArray(B);

    return 0;
}
```
### Output Unguided 3 :

##### Output 
![Screenshot Output Unguided 3_1](https://github.com/shamoera/Laprak-Strukdat-Modul-3/blob/main/soal3.png)

Program ini punya dua array 2D berukuran 3x3 (A dan B) dan dua pointer integer (p1 dan p2). Fungsi tampilArray menampilkan isi array baris demi baris. Fungsi tukarArray menukar isi A dan B pada posisi (baris, kolom) yang diketik pengguna, dengan variabel temp sebagai tempat menyimpan sementara. Fungsi tukarPointer menukar isi dari variabel yang ditunjuk dua pointer, yaitu *p1 dan *p2. Di program ini p1 menunjuk A[0][0] dan p2 menunjuk B[2][2], jadi setelah ditukar, isi kedua elemen itu di array A dan B ikut berubah. Contohnya, kalau posisi yang diketik 1 1, maka A[1][1] (5) bertukar dengan B[1][1] (50). Setelah itu A[0][0] (1) bertukar dengan B[2][2] (90).

## Kesimpulan
Dari praktikum ini dapat disimpulkan bahwa ADT membuat program lebih rapi karena dipisah menjadi tiga bagian, yaitu file header (.h) untuk definisi type dan daftar fungsi, file .cpp untuk isi fungsi, dan main.cpp untuk program utama. Dengan begitu kode lebih mudah dibaca dan fungsinya bisa dipakai lagi di program lain. ADT sudah dicoba pada data mahasiswa dan pelajaran. Selain itu, praktikum ini juga melatih penggunaan array 2D, fungsi, dan pointer untuk menukar isi variabel.

## Referensi
[1] Informatics Lab, Fakultas Informatika, Telkom University. (n.d.). "Modul 3 Abstract Data Type (ADT)", Modul Praktikum Struktur Data. Purwokerto: Telkom University. 
<br>
