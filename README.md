## KEGIATAN 1
## SuperClass Hewan
Kelas induk (superclass). Isinya satu method, bersuara(), yang mencetak teks umum. Analogi: kalau kamu cuma dibilang “ada hewan”, kamu belum tahu suaranya seperti apa, jadi jawabannya masih umum.
public class Hewan: kelas bernama Hewan yang bisa diakses dari mana saja.
public void bersuara(): method yang bisa dipanggil dari luar (public) dan tidak mengembalikan nilai (void).
System.out.println(...): mencetak teks ke layar lalu pindah baris.

## SubClass kucing dan anjing
extends Hewan artinya Kucing dan Anjing mewarisi Hewan, jadi otomatis punya method bersuara().
Tapi suara bawaan Hewan terlalu umum, jadi kedua kelas ini menulis ulang method tersebut. Disebut Method Overriding.
@Override adalah anotasi (penanda) untuk bilang ke Java, “Aku sengaja menimpa method dari induk.” Fungsinya sebagai pengaman. Kalau salah ketik nama method (misalnya bersuaraa()), Java langsung kasih tanda pentung merah (error). Makanya di modul disebut “opsional tapi direkomendasikan”.

## Class PoliTester
public static void main(String[] args) adalah pintu masuk program. Java mulai menjalankan dari sini.
Hewan[] daftarHewan = new Hewan[3]; membuat array berisi 3 slot, dan setiap slot bertipe Hewan. Slotnya masih kosong (null).
daftarHewan[0] = new Hewan(); mengisi slot 0 dengan objek Hewan biasa.
daftarHewan[1] = new Kucing(); mengisi slot 1 dengan objek Kucing. Ini boleh karena Kucing adalah Hewan. Memasukkan objek subclass ke variabel bertipe superclass disebut Upcasting.
daftarHewan[2] = new Anjing(); sama seperti di atas, tapi isinya Anjing.
for (Hewan h : daftarHewan) adalah for-each: ambil satu per satu isi array dan taruh di variabel h.
h.bersuara(); memanggil method bersuara().
output:
Hewan ini mengeluarkan suara yang tidak spesifik.
Kucing: Meow meow!
Anjing: Guk guk!

## KEGIATAN 2
## Class abstrak BangunDatar
abstract class adalah kelas yang tidak boleh dibuat objeknya. new BangunDatar("merah") akan error. Alasannya: “bangun datar” itu konsep umum, bukan benda nyata. Yang nyata itu lingkaran, persegi, segitiga, dan seterusnya.
String warna; adalah atribut yang dimiliki semua bangun datar.
Constructor BangunDatar(String warna) dipakai untuk mengisi warna. this.warna = warna; artinya “isi atribut milik objek ini (this.warna) dengan parameter yang masuk (warna)”.
public abstract double hitungLuas(); adalah abstract method. Tidak ada kurung kurawal {} dan diakhiri titik koma. Ini hanya bukti bahwa setiap bangun datar punya cara menghitung luas, tapi caranya diserahkan ke subclass. Alasannya, rumus luas tiap bangun berbeda.
cetakWarna() adalah concrete method (method biasa yang punya isi). Cara mencetak warna sama untuk semua bangun.

## Subclass Lingkaran
extends BangunDatar yang artinya Lingkaran adalah salah satu jenis bangun datar.
private double jariJari; adalah atribut khusus lingkaran. private berarti hanya bisa diakses dari dalam kelas ini.
Constructor menerima dua data, warna dan jariJari.
super(warna); memanggil constructor milik induk (BangunDatar) untuk mengisi warna. 
this.jariJari = jariJari; mengisi jari-jari milik Lingkaran sendiri.
hitungLuas() adalah method yang wajib di-override karena induknya abstrak. Isinya rumus luas lingkaran: π × r × r. Math.PI adalah nilai π (3,14159...) bawaan Java.

## TesBangunDatar
public static void main(String[] args) adalah pintu masuk program. Java mulai menjalankan dari sini.
Lingkaran lingkaran = new Lingkaran("Merah", 5); membuat objek Lingkaran dengan warna "Merah" dan jari-jari 5. Kedua nilai ini dikirim ke constructor. Yang dibuat adalah Lingkaran, bukan BangunDatar, karena kelas abstrak tidak boleh di-new.
lingkaran.cetakWarna(); memanggil method yang diwariskan dari BangunDatar. Method ini tidak ditulis di Lingkaran, tapi tetap bisa dipakai.
lingkaran.hitungLuas() memanggil method milik Lingkaran (hasil override), lalu hasilnya digabung dengan teks "Luas lingkaran: " memakai tanda + dan dicetak.
Satu objek memakai method dari dua sumber: cetakWarna() dari kelas abstrak induk, dan hitungLuas() yang ditulis sendiri oleh Lingkaran.
output:
Warna bangun ini adalah: Merah
Luas lingkaran: 78.53981633974483

## KEGIATAN 3
## Dua interface
Interface: daftar kemampuan yang wajib dimiliki. Isinya hanya nama method tanpa isi. 
AlatElektronik: apa pun yang termasuk alat elektronik harus bisa dinyalakan dan dimatikan.
Kamera: apa pun yang berfungsi sebagai kamera harus bisa mengambil foto.

## Class Smartphone
implements AlatElektronik, Kamera artinya Smartphone menyanggupi kedua kontrak sekaligus. Disebut multiple implementation, yaitu cara Java “menyimulasikan” pewarisan ganda. Java tidak mengizinkan extends dua kelas, tapi boleh implements banyak interface.
Karena sudah menyanggupi, Smartphone wajib menulis isi dari ketiga method (nyalakan, matikan, ambilFoto). Kalau ada yang terlewat, akan (error).
private String merk; menyimpan nama merek, dan constructor mengisinya.
Tanda + pada merk + " menyala..." menggabungkan teks (string concatenation)

## TesSmartphone
public static void main(String[] args) adalah titik awal program, sama seperti sebelumnya.
Smartphone hp = new Smartphone("Samsung"); membuat objek Smartphone dan menyimpannya di variabel hp. Nilai "Samsung" dikirim ke constructor dan disimpan di atribut merk.
hp.nyalakan(); menjalankan method dari interface AlatElektronik, dengan isi yang ditulis di Smartphone.
hp.ambilFoto(); menjalankan method dari interface Kamera.
hp.matikan(); menjalankan method dari interface AlatElektronik.
satu objek hp bisa memakai method dari dua interface sekaligus. ini adalah multiple implementation, cara Java menyimulasikan pewarisan ganda
output:
Samsung menyala. Booting OS...
Cekrek! Foto berhasil disimpan di galeri Samsung.
Samsung dimatikan. Goodbye:).
