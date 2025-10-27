# Laporan Praktikum Minggu 1 (sesuaikan minggu ke berapa?)
Topik: Inheritance [Pewaris]

## Identitas
- Nama  : [Febiana Saputri]
- NIM   : [240320569]
- Kelas : [3DSRA]

---

## Tujuan
- Mahasiswa memahami konsep inheritance dalam OOP.
- Mahasiswa mampu membuat kelas induk (parent) dan kelas anak (child)
- Mahasiswa dapat mengimplementasikan pewarisan untuk mengurangi duplikasi kode dan membuat program lebih terstruktur
  
---

## Dasar Teori
1. Inheritance adalah mekanisme pewarisan sifat dari class induk ke class anak.
2. Class anak dapat mengakses atribut dan method milik class induk.
3. Keyword extends digunakan untuk melakukan inheritance di Java.
4. Inheritance membuat kode lebih efisien, reusable, dan mudah dikembangkan.
5. Method milik induk dapat dioverride di class anak jika perlu.

---

## Langkah Praktikum
1. Buat project baru dengan nama sesuai topik, misalnya Agripos.
2. Buat class induk (superclass) dengan nama Produk yang berisi atribut umum seperti kode, nama, harga, dan stok.
3. Buat class turunan (subclass) seperti BenihKacang, PupukUrea, dan Alat yang mewarisi dari class Produk dan menambahkan atribut khusus sesuai kebutuhan.
4. Buat class utama bernama MainInheritance untuk menguji konsep pewarisan dengan membuat objek dari masing-masing subclass dan menampilkan data melalui metode getter.
5. Tambahkan class utilitas seperti CreditBy untuk menampilkan identitas mahasiswa (nama dan NIM).
6. Jalankan program dan amati hasil output di konsol untuk memastikan pewarisan berjalan dengan benar.
7. lalu commit dan push

---

## Kode Program
(Tuliskan kode utama yang dibuat, contoh:  
(Produk java)
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

    public String getKode() { return kode; }
    public String getNama() { return nama; }
    public double getHarga() { return harga; }
    public int getStok() { return stok; }

    public void tampilkanInfo() {
        System.out.println("Kode: " + kode + ", Nama: " + nama + ", Harga: " + harga + ", Stok: " + stok);
    }
}


```
(Benih Java)
```
package model;

public class Benih extends Produk {
    private String varietas;

    public Benih(String kode, String nama, double harga, int stok, String varietas) {
        super(kode, nama, harga, stok);
        this.varietas = varietas;
    }

    public String getVarietas() { return varietas; }
    public void setVarietas(String varietas) { this.varietas = varietas; }
}

```
(Pupuk Java)
```
package model;

    public class Pupuk extends Produk {
        private String jenis;
    
        public Pupuk(String kode, String nama, double harga, int stok, String jenis) {
            super(kode, nama, harga, stok);
            this.jenis = jenis;
        }
    
        public String getJenis() { return jenis; }
        public void setJenis(String jenis) { this.jenis = jenis; }
    }
```
(AlatPertanian Java)
```
package model;

public class AlatPertanian extends Produk {
    private String bahan;

    public AlatPertanian(String kode, String nama, double harga, int stok, String bahan) {
        super(kode, nama, harga, stok);
        this.bahan = bahan;
    }

    public String getBahan() { return bahan; }
    public void setBahan(String bahan) { this.bahan = bahan; }
}

```
(MainInheritance)
```
import model.*;
import util.*;

public class MainInheritance {
    public static void main(String[] args) {
        Benih b = new Benih("BNH-001", "Benih Padi IR64", 25000, 100, "IR64");
        Pupuk p = new Pupuk("PPK-101", "Pupuk Urea", 350000, 40, "Urea");
        AlatPertanian a = new AlatPertanian("ALT-501", "Cangkul Baja", 90000, 15, "Baja");

        System.out.println("Benih: " + b.getNama() + ", Varietas: " + b.getVarietas());
        System.out.println("Pupuk: " + p.getNama() + ", Jenis: " + p.getJenis());
        System.out.println("Alat Pertanian: " + a.getNama() + ", Bahan: " + a.getBahan());

        CreditBy.tampilkan("Febiana Saputri", "240320569");
    }
}

```
---

## Hasil Eksekusi
[(https://github.com/fabianasaputri-ops/oop-202501-240320569/tree/0faa21c0298ca41904f313e1d0a9ae568e4e17e9/praktikum/week3-inheritance/screenshots)](https://github.com/fabianasaputri-ops/oop-202501-240320569/blob/0faa21c0298ca41904f313e1d0a9ae568e4e17e9/praktikum/week3-inheritance/screenshots/MainInheritance.java.png)
---

## Analisis
(
- Program ini merupakan penerapan dari konsep Inheritance (pewarisan) pada OOP di java. Program ini terdiri dari satu superclass berupa Produk dan tiga subclass yaitu Benih, Pupuk, dan AlatPertanian. Masing-masing subclass mewarisi atribut dan method dari superclass, seperti kode, nama, harga, stok, dan lain-lain. Kemudian ditambahkan atribut khusus, misalnya varietas pada subclass Benih, atribut Jenis untuk menunjukkan tipe Pupuk, serta atribut material pada AlatPertanian, method deskripsi() juga ditambahkan untuk menampilkan informasi tambahan yang lebih spesifik mengenai produk. Ketika program dijalankan melalui class utama MainInheritance, sistem terlebih dahulu membuat tiga objek dari masing-masing subclass. Setiap objek diinisialisasi dengan pemanggilan konstruktor masing-masing subclass dan meneruskannya ke konstruktor superclass produk dengan menggunakan super() yang kemudian dilanjutkan dengan memanggil method deskripsi untuk menampilkan detail lengkap. Pada bagian akhir, method CreditBy digunakan untuk menampilkan identitas dari mahasiswa.
- Perbedaan utama antara praktikum minggu ini dan sebelumnya terletak pada penerapan konsep OOP. Pada minggu sebelumnya, praktikum menekankan pembentukan class dan object dengan prinsip enkapsulasi. Sedangkan praktikum kali ini, fokus beralih pada konsep inheritance (pewarisan) melalui pengembangan beberapa subclass yang mewarisi atribut dan metode dari superclass serta menambah atribut khusus di masing-masing subclass.
- Kendala yang dihadapi selama praktikum kali ini masih berkaitan dengan pengaturan struktur package dan proses import antar class. Hal ini mengakibatkan beberapa error muncul pada saat proses running karena perbedaan letak penyimpanan file penulisan package yang tidak sesuai. Sehingga perlu dilakukan penyesuaian ulang dari masing-masing package untuk mengatasi kendala ini. 
)
---

## Kesimpulan
Pada praktikum minggu ini, mahasiswa telah mempelajari dan menerapkan konsep inheritance (pewarisan) dalam pemrograman berorientasi objek menggunakan bahasa Java. Melalui pembuatan class induk Produk dan beberapa class turunan seperti BenihKacang, PupukUrea, dan Alat, mahasiswa memahami bagaimana subclass dapat mewarisi atribut dan metode dari superclass.
Penerapan inheritance membantu mengurangi duplikasi kode, membuat program lebih terstruktur, mudah dikembangkan, serta menunjukkan hubungan hierarki antar objek. Dengan demikian, mahasiswa mampu mengimplementasikan prinsip pewarisan secara efektif dalam pembuatan program berbasis objek.

---

## Quiz
(1. Apa keuntungan menggunakan inheritance dibanding membuat class terpisah tanpa hubungan?  
   *Jawaban:*Keuntungan menggunakan inheritance adalah dapat menghemat kode dengan mewarisi atribut dan metode dari superclass sehingga tidak perlu menulis ulang kode yang sama. Selain itu, program menjadi lebih terstruktur, mudah dipelihara, dan dapat dikembangkan karena adanya hubungan hierarki antar class.

2. Bagaimana cara subclass memanggil konstruktor superclass?   
   *Jawaban:*Subclass memanggil konstruktor superclass dengan menggunakan kata kunci super() pada baris pertama konstruktor subclass. Contohnya:
   public BenihKacang(String kode, String nama, double harga, int stok, String varietas) {
    super(kode, nama, harga, stok);
    this.varietas = varietas;
}
 
3. Berikan contoh kasus di POS pertanian selain Benih, Pupuk, dan Alat Pertanian yang bisa dijadikan subclass.  
   *Jawaban:*Contoh lainnya adalah Pestisida, Obat Tanaman, atau Peralatan Irigasi, yang semuanya bisa dijadikan subclass dari Produk karena memiliki atribut dasar yang sama seperti kode, nama, harga, dan stok, tetapi memiliki karakteristik tambahan masing-masing  )
