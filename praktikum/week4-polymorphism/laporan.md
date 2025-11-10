# Laporan Praktikum Minggu 1 (sesuaikan minggu ke berapa?)
Topik: Main Polymorphism

## Identitas
- Nama  : [Febiana Saputri]
- NIM   : [240320569]
- Kelas : [3DSRA]

---

## Tujuan
-Mahasiswa mampu memahami konsep Polymorphism dalam pemrograman berorientasi objek.
-Mahasiswa mampu membedakan method overriding dan method overloading.
-Mahasiswa dapat mengimplementasikan polymorphism pada class turunan di Java.
-Mahasiswa aktif menganalisis perbedaan perilaku method yang sama pada objek berbeda.

---

## Dasar Teori
Polymorphism adalah salah satu konsep utama dalam OOP (Object-Oriented Programming) yang memungkinkan satu interface memiliki banyak implementasi.
   -Polymorphism (Banyak Bentuk): kemampuan objek berbeda untuk merespons method dengan cara yang berbeda.
   -Overriding: mendefinisikan ulang method superclass di subclass agar memiliki perilaku berbeda.
   -Overloading: membuat beberapa method dengan nama sama, tetapi parameter berbeda dalam satu class.
   -Dynamic Binding: pemanggilan method yang ditentukan saat runtime berdasarkan tipe objek sebenarnya.
   -Dengan polymorphism, program menjadi lebih fleksibel, mudah dikembangkan, dan mendukung prinsip code reusability.

---

## Langkah Praktikum
1. Overloading
   - Tambahkan method tambahStok(int jumlah) dan tambahStok(double jumlah) pada class Produk.
2. Overriding
   - Tambahkan method getInfo() pada superclass Produk.
   - Override method getInfo() pada subclass Benih, Pupuk, dan AlatPertanian.
3. Dynamic Binding
   - Buat array Produk[] daftarProduk yang berisi objek Benih, Pupuk, dan AlatPertanian.
   - Loop array tersebut dan panggil getInfo(). Perhatikan bagaimana Java memanggil method sesuai jenis objek aktual.
4. Main Class
   - Buat MainPolymorphism.java untuk mendemonstrasikan overloading, overriding, dan dynamic binding.
5. CreditBy
   - Tetap panggil CreditBy.print("<NIM>', "<Nama>").
6. Commit dan Push
   - Commit dengan Pesan: week4-polymorhism.

---

## Kode Program
1. Produk.java
```
package model;

public class Produk {
    private String kode;
    private String nama;
    private double harga;
    private int stok;

    public Produk(String kode, String nama, double harga, int stok) {
        this.kode = kode;
        this.nama = nama;
        this.harga = harga;
        this.stok = stok;
    }

    // Overloading
    public void tambahStok(int jumlah) {
        this.stok += jumlah;
    }

    public void tambahStok(double jumlah) {
        this.stok += (int) jumlah;
    }

    // Getter
    public String getKode() { return kode; }
    public String getNama() { return nama; }
    public double getHarga() { return harga; }
    public int getStok() { return stok; }

    // Method yang akan dioverride
    public String getInfo() {
        return "Produk: " + nama + " (Kode: " + kode + ", Harga: " + harga + ", Stok: " + stok + ")";
    }
}
```
2. Benih.java
```
package model;

public class Benih extends Produk {
    private String varietas;

    public Benih(String kode, String nama, double harga, int stok, String varietas) {
        super(kode, nama, harga, stok);
        this.varietas = varietas;
    }

    @Override
    public String getInfo() {
        return "Benih - " + super.getInfo() + ", Varietas: " + varietas;
    }
}
```
3. Pupuk.java
```
package model;

public class Pupuk extends Produk {
    private String jenis;

    public Pupuk(String kode, String nama, double harga, int stok, String jenis) {
        super(kode, nama, harga, stok);
        this.jenis = jenis;
    }

    @Override
    public String getInfo() {
        return "Pupuk - " + super.getInfo() + ", Jenis: " + jenis;
    }
}
```
4. AlatPertanian.java
```
//overriding alat pertanian

package com.upb.agripos.model;

public class AlatPertanian extends Produk {
    private String material;

    public AlatPertanian(String kode, String nama, double harga, int stok, String material) {
        super(kode, nama, harga, stok);
        this.material = material;
    }

    @Override
    public String getInfo() {
        return "Alat Pertanian: " + super.getInfo() + ", Material: " + material;
    }
}
```
5. MainPolymorphism.java
```
//main program polymorphism

package com.upb.agripos;

import com.upb.agripos.model.*;
import com.upb.agripos.util.CreditBy;

public class MainPolymorphism {
    public static void main(String[] args) {
        
        System.out.println("=== Program Agri-POS ===");
        System.out.println("------------------------");
        System.out.println("Daftar Produk: ");
        
        Produk[] daftarProduk = {
            new Benih("BNH-001", "Benih Padi IR64", 25000, 100, "IR64"),
            new Pupuk("PPK-101", "Pupuk Urea", 350000, 40, "Urea"),
            new AlatPertanian("ALT-501", "Cangkul Baja", 90000, 15, "Baja")
        };

        for (Produk p : daftarProduk) {
            System.out.println(p.getInfo()); // Dynamic Binding
        }

        CreditBy.print("Difa Rizkiana Fauziyah", "240320564");
    }
}
```

---

## Hasil Eksekusi
(Sertakan screenshot hasil eksekusi program.  
![Screenshot hasil](screenshots/hasil.png)
)
---

## Analisis
1. Cara Kerja Kode

    Program ini merupakan penerapan dari konsep polymorphism dengan Produk sebagai class induk bagi semua jenis produk dalam Agri-POS. Superclass ini memiliki atribut seperti kode, nama, harga, dan stok yang memuat identitas setiap produk. Selain itu, class Produk juga memiliki method tambahStok() yang di-overload agar dapat menerima parameter dengan tipe data berbeda, baik int maupun double. Method ini digunakan untuk menambah jumlah stok produk sesuai kebutuhan. Kemudian terdapat method getInfo() yang mengembalikan informasi umum produk berupa nama dan kode. Method ini yang nantinya akan di-override oleh subclass untuk menampilkan informasi lebih spesifik.
    
    Dari kelas Produk ini diturunkan beberapa subclass lain yang mewakili jenis produk berbeda, yaitu Benih, Pupuk, dan AlatPertanian, di mana masing-masing subclass menambahkan atribut khusus. Seperti misalnya, subclass Benih menambahkan atribut varietas, subclass Pupuk menambahkan atribut jenis, dan atribut material ditambahkan pada subclass AlatPertanian. Subclass tersebut melakukan overriding terhadap method getInfo() dari class Produk untuk menampilkan informasi tambahan mengenai atribut khusus yang telah dibuat. Pemanggilan super.getInfo() tetap dilakukan agar informasi umum produk tetap muncul bersamaan dengan data spesifik subclass tersebut.
    
    Bagian utama dari penerapan polymorphism terdapat pada class MainPolymorphism, yang berperan sebagai pusat eksekusi program. Di dalam class ini, dibuat arrat Produk[] yang berisi objek-objek dari beberapa subclass. Meskipun seluruh elemen array menggunakan tipe Produk, setiap objek di dalamnya tetap mempertahankan perilaku spesifik masing-masing. Proses ini menjadi inti dari mekanisme dynamic binding. Ketika dilakukan pemanggilan method getInfo() melalui looping for-each, Java akan akan memanggil versi method yang sesuai dengan tipe objek sebenarnya pada saat program dijalankan. Bagian akhir dari program memanggil CreditBy.print() untuk menampilkan identitas dari mahasiswa.
2. Perbedaan dengan Praktikum Sebelumnya

    Terdapat perbedaan dengan praktikum minggu sebelumnya, di mana pembahasan sebelumnya berfokus pada konsep inheritance, yaitu bagaimana suatu class dapat menurunkan atribut dan method pada subclass. Sementara itu, praktikum minggu ini fokus pada penerapan polymorphism dan method overriding, yang mana subclass dapat memodifikasi perilaku method dari superclass. Melalui polymorphism, objek-objek yang berbeda dapat diakses menggunakan satu referensi umum dan program akan menyesuaikan method yang dijalankan secara dinamis.

3. Kendala yang Dihadapi

    Kendala yang dihadapi pada praktikum kali ini muncul pada saat proses kompilasi dan eksekusi program berupa error "invalid filename" dan "Class not found exception". Kendala ini terjadi karena struktur direktori dan perintah kompilasi Java belum diarahkan sesuai dengan lokasi file program. Perlu dilakukan kompilasi ulang dengan menyesuaikan lokasi file agar hasil kompilasi tersimpan di dalam folder bin, sehingga program sepenuhnya bisa dijalankan serta menampilkan hasil output yang diinginkan.


---

## Kesimpulan
Secara keseluruhan, program ini berhasil memperlihatkan penerapan konsep polymorphism dengan baik. Penerapan ini menunjukkan bagaimana polymorphism memungkinkan satu tipe referensi tunggal di superclass untuk merepresentasikan berbagai bentuk method pada subclass tanpa memerlukan pengondisian yang kompleks seperti if-else atau switch. Jika di masa mendatang dilakukan penambahan subclass dari superclass, maka sistem dapat secara otomatis menanganinya tanpa mengubah logika utama pada class polymorphism. Selain itu, hasil output program menunjukkan bahwa setiap objek menampilkan detail informasi yang berbeda sesuai dengan jenis produknya. Hal ini mempertegas bahwa overriding berhasil diterapkan dengan benar dan sistem mampu mengenali serta mengeksekusi method yang sesuai dengan class masing-masing. Konsep ini membuat program menjadi lebih efisien, terstruktur, dan fleksibel untuk dikembangkan sesuai kebutuhan Agri-POS.


---

## Quiz
1. Apa perbedaan overloading dan overriding?  
   *Jawaban:* Overloading terjadi ketika terdapat penggunaan beberapa method dengan nama yang sama namun memiliki parameter yang berbeda dalam satu class, baik jumlah, tipe data, maupun urutan. Tujuannya adalah memberikan kemudahan bagi pengguna untuk memanggil method yang sama dengan variasi input yang berbeda tanpa harus membuat nama method baru. Sedangkan overriding terjadi ketika sebuah subclass mengganti implementasi method dari superclass dengan nama dan parameter yang sama namun dengan isi berbeda. Tujuannya adakah agar setiap subclass dapat menyesuaikan perilaku method sesuai kebutuhan spesifiknya.

2. Bagaimana Java menentukan method mana yang dipanggil dalam dynamic binding?  
   *Jawaban:* Dalam java, dynamic binding menentukan method yang dijalankan berdasarkan objek sebenarnya saat program dieksekusi, bukan berdasarkan tipe referensinya. Proses ini terjadi pada tahap runtime, ketika referensi superclass menunjuk pada objek subclass, maka method yang dipanggil adalah milik subclass tersebut. 

3. Berikan contoh kasus polymorphism dalam sistem POS selain produk pertanian!  
   *Jawaban:* Dalam konteks POS, penerapan polymorphism dapat diimplementasikan juga pada POS Fashion Store. sebagai contoh, superclass Produk dapat diturunkan menjadi subclass seperti Baju, Celana, dan Aksesoris, yang masing-masing memiliki atribut dan perilaku khusus, misalnya atribut tambahan berupa Ukuran, Jenis kain, Warna, dan lain sebagainya. Ketika program memanggil method getInfo() melalui Produk, maka hasil output akan menampilkan informasi spesifik sesuai objek sebenarnya.
