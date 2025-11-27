# Laporan Praktikum Minggu 5
Topik: [Abstraction (Abstract Class & Interface)]

## Identitas
- Nama  : [Febiana Saputri]
- NIM   : [240320569]
- Kelas : [3DSRA]

---

## Tujuan
- Mahasiswa mampu menjelaskan perbedaan abstract class dan interface.
- Mahasiswa mampu mendesain abstract class dengan method abstrak sesuai kebutuhan kasus.
- Mahasiswa mampu membuat interface dan mengimplementasikannya pada class.
- Mahasiswa mampu menerapkan multiple inheritance melalui interface pada rancangan kelas.
- Mahasiswa mampu mendokumentasikan kode (komentar kelas/method, README singkat pada folder minggu).

---

## Dasar Teori
Abstraksi adalah proses menyederhanakan kompleksitas dengan menampilkan elemen penting dan menyembunyikan detail implementasi.
   - Abstract class: tidak dapat diinstansiasi, dapat memiliki method abstrak (tanpa badan) dan non-abstrak. Dapat menyimpan state (field).
   - Interface: kumpulan kontrak (method tanpa implementasi konkret). Sejak Java 8 mendukung default method. Mendukung multiple inheritance (class dapat mengimplementasikan banyak interface).
   - Gunakan abstract class bila ada shared state dan perilaku dasar; gunakan interface untuk mendefinisikan kemampuan/kontrak lintas hierarki.
Dalam konteks Agri-POS, Pembayaran dapat dimodelkan sebagai abstract class dengan method abstrak prosesPembayaran() dan biaya(). Implementasi konkritnya: Cash dan EWallet. Kemudian, interface seperti Validatable (mis. verifikasi OTP) dan Receiptable (mencetak bukti) dapat diimplementasikan oleh jenis pembayaran yang relevan.

---

## Langkah Praktikum
1. Abstract Class – Pembayaran
   Buat Pembayaran (abstract) dengan field invoiceNo, total dan method:
   - double biaya() (abstrak) → biaya tambahan (fee).
   - boolean prosesPembayaran() (abstrak) → mengembalikan status berhasil/gagal.
   - double totalBayar() (konkrit) → return total + biaya();.

2. Subclass Konkret
   - Cash → biaya = 0, proses = selalu berhasil jika tunai >= totalBayar().
   - EWallet → biaya = 1.5% dari total; proses = membutuhkan validasi.

3. Interface
   - Validatable → boolean validasi(); (contoh: OTP).
   - Receiptable → String cetakStruk();

4. Multiple Inheritance via Interface
   - EWallet mengimplementasikan dua interface: Validatable, Receiptable.
   - Cash setidaknya mengimplementasikan Receiptable.

5. Main Class
   - Buat MainAbstraction.java untuk mendemonstrasikan pemakaian Pembayaran (polimorfik).
   - Tampilkan hasil proses dan struk. Di akhir, panggil CreditBy.print("[NIM]", "[Nama]").

6. Commit dan Push
   Commit dengan pesan: week5-abstraction-interface.
---

## Kode Program

java
import model.kontrak.Receiptable;
import model.pembayaran.Cash;
import model.pembayaran.EWallet;
import model.pembayaran.Pembayaran;
import model.pembayaran.TransferBank;
import util.CreditBy;

public class MainAbstraction {
    public static void main(String[] args) {
        Pembayaran cash = new Cash("INV-001", 87000, 100000);
        Pembayaran ew = new EWallet("INV-002", 175000, "febianasaputri@ewallet", "123456");
        Pembayaran transfer = new TransferBank("INV-003", 150000, "BCA", true);


        System.out.println(((Receiptable) cash).cetakStruk());
        System.out.println(((Receiptable) ew).cetakStruk());
        System.out.println(((Receiptable) transfer).cetakStruk());
    
        CreditBy.print("Febiana Saputri", "240320569");
    }
}

---

## Hasil Eksekusi
(Sertakan screenshot hasil eksekusi program.  
![Screenshot hasil](screenshots/SS-WEEK5.png)
)
---

## Analisis

- Jelaskan bagaimana kode berjalan.  
   Kode berjalan dengan membuat tiga objek pembayaran (Cash, EWallet, dan TransferBank) yang semuanya merupakan subclass dari Pembayaran sekaligus mengimplementasikan interface Receiptable, sehingga masing-masing memiliki versi sendiri dari method cetakStruk(). Di dalam main, objek-objek tersebut dipanggil melalui casting ke Receiptable, sehingga program dapat memanggil cetakStruk() tanpa peduli jenis pembayarannya; inilah polimorfisme berbasis interface. Setiap objek menghasilkan struk sesuai logika kelasnya—Cash menghitung kembalian, EWallet menghitung total + fee, dan TransferBank menambah biaya admin—lalu hasilnya dicetak ke layar. Setelah itu, method CreditBy.print() dijalankan untuk menampilkan identitas praktikan sebagai bagian dari output akhir.

- Apa perbedaan pendekatan minggu ini dibanding minggu sebelumnya.  
   Perbedaan utama minggu ini dibanding minggu sebelumnya adalah jika minggu lalu kamu menggunakan *polymorphism berbasis inheritance* (class induk dan class turunan), maka minggu ini kamu menggunakan *polymorphism berbasis interface*. Pada minggu sebelumnya, semua subclass harus berada dalam satu hirarki dan mewarisi perilaku dari satu class induk, sedangkan minggu ini setiap class bebas mengimplementasikan interface Receiptable tanpa harus berada dalam satu garis keturunan yang sama, sehingga lebih fleksibel dan memungkinkan objek berbeda memiliki perilaku yang konsisten (seperti cetakStruk()) meskipun tidak saling mewarisi. Dengan kata lain, minggu lalu fokus pada pewarisan, sedangkan minggu ini fokus pada *kontrak perilaku* melalui interface.

- Kendala yang dihadapi dan cara mengatasinya.  
   Kendala yang dihadapi meliputi error package yang tidak sesuai karena struktur folder berbeda dengan deklarasi package, error saat mencoba menjalankan interface karena interface tidak memiliki main(), serta error kompilasi seperti pada CreditBy akibat method atau package yang tidak cocok. Cara mengatasinya adalah menyesuaikan folder dengan package yang ditulis, menjalankan hanya class yang memiliki method main(), serta memperbaiki method, return type, atau package pada file yang error hingga sesuai dengan struktur project.


---

## Kesimpulan
(Kesimpulan dari praktikum minggu ini adalah bahwa penggunaan interface memberikan fleksibilitas lebih besar dalam menerapkan polimorfisme karena sebuah class dapat mengimplementasikan banyak interface tanpa harus terikat pada satu hirarki pewarisan. Dengan interface seperti Receiptable, berbagai jenis pembayaran dapat memiliki metode cetakStruk() masing-masing namun tetap diperlakukan secara seragam saat digunakan. Praktikum ini menunjukkan bahwa interface sangat efektif untuk mendefinisikan perilaku yang harus dimiliki oleh banyak class berbeda, membuat desain program lebih modular, mudah diperluas, dan lebih rapi dibanding hanya mengandalkan inheritance seperti minggu sebelumnya.
)

---

## Quiz
(1. [Jelaskan perbedaan konsep dan penggunaan abstract class dan interface.]  
   *Jawaban:* Abstract class digunakan sebagai kerangka dasar bagi class-class yang masih satu keluarga dan dapat berisi atribut, constructor, method biasa, maupun method abstract, sehingga cocok ketika beberapa class berbagi perilaku atau data yang sama. Sementara itu, interface berfungsi sebagai kontrak perilaku yang hanya mendefinisikan method apa yang harus dimiliki tanpa menyediakan implementasi, sehingga cocok ketika banyak class yang tidak saling berhubungan tetap harus memiliki perilaku yang sama. Abstract class hanya mendukung single inheritance, sedangkan interface dapat diimplementasikan oleh banyak class sekaligus, sehingga lebih fleksibel untuk mendistribusikan perilaku tertentu tanpa memaksa class tersebut berada dalam satu hirarki pewarisan.

2. [Mengapa multiple inheritance lebih aman dilakukan dengan interface pada Java?]  
   *Jawaban:* Multiple inheritance lebih aman dilakukan dengan interface di Java karena interface hanya berisi *kontrak perilaku* tanpa menyimpan state atau implementasi detail, sehingga tidak menimbulkan konflik pewarisan seperti pada multiple inheritance berbasis class. Jika Java mengizinkan class mewarisi banyak class sekaligus, maka bisa muncul masalah seperti *diamond problem*—dua parent memiliki atribut atau method yang sama sehingga compiler tidak tahu versi mana yang harus dipakai. Dengan interface, class hanya mengimplementasikan deklarasi method, bukan mewarisi data atau logika internal, sehingga tidak ada benturan state maupun implementasi. Karena itu Java memilih hanya mengizinkan multiple inheritance melalui interface agar tetap fleksibel namun aman dari konflik pewarisan. 

3. [Pada contoh Agri-POS, bagian mana yang paling tepat menjadi abstract class dan mana yang menjadi interface? Jelaskan alasannya]  
   *Jawaban:* Pada contoh Agri-POS, **Pembayaran** adalah bagian yang paling tepat dijadikan *abstract class*, sedangkan **Receiptable** adalah bagian yang tepat dijadikan *interface*. Pembayaran cocok sebagai abstract class karena semua jenis pembayaran (Cash, EWallet, TransferBank) memiliki struktur dan data dasar yang sama seperti nomor invoice, total, dan cara menghitung biaya, sehingga class ini dapat menyimpan atribut umum dan sebagian logika dasar yang diwariskan ke subclass. Sebaliknya, Receiptable tepat sebagai interface karena hanya mendefinisikan perilaku wajib berupa cetakStruk() tanpa memaksa semua jenis pembayaran berbagi struktur data atau logika yang sama; setiap metode pembayaran memiliki cara berbeda untuk menampilkan struk, tetapi semuanya tetap harus menyediakan implementasinya. Dengan desain ini, abstract class mengatur fondasi dan kesamaan, sementara interface memaksakan perilaku yang seragam tanpa memengaruhi hierarki pewarisan.
 )
