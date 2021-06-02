# OOP

Paradigma OOP memudahkan memvisualisasikan kode dengan skenario kehidupan nyata. Dalam penerapan OOP kita menggabungkan kumpulan-kumpulan fungsi atau atribut yang memiliki kesamaan dalam sebuah unit yang kita sebut sebagai objek.

Pada pemrograman dengan menggunakan pendekatan OOP kita akan menemui beberapa istilah atau pembahasan seperti Class, Attribute dan Function.

Properti atau atribut yang memiliki makna yang sama meskipun tersendiri namanya berbeda. 

Biasanya programmer lebih sering menggunakan atribut untuk istilah yang berkaitan dengan hal yang mengarah ke mekanisme atau proses yang dilakukan oleh objek dan menggunakan istilah property untuk mendeskripsikan karakteristik dari sebuah objek.

Class merupakan sebuah blueprint yang dapat dikembangkan untuk membuat sebuah objek. Blueprint ini merupakan sebuah template yang di dalamnya menjelaskan seperti apa perilaku dari objek itu (berupa properti ataupun function).

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/202004081610044e0e18799a32ee7d458f1ca15b9693f6.png)

Visualisasi di atas mencontohkan gambaran umum dari konsep OOP, di mana terdapat sebuah blueprint Kucing, atribut yang dimiliki Kucing, dan kemampuan yang dapat dilakukan oleh Kucing. 

Function atau fungsi merupakan sebuah prosedur yang memiliki keterkaitan dengan pesan dan objek. Ketika kita memanggil sebuah fungsi maka sebuah mini-program akan dijalankan. 

Fungsi sendiri bisa diartikan sebagai cara sederhana untuk mengatur program buatan kita. 

Contoh, hewan memiliki beberapa behavior atau fungsi yang dapat ia lakukan seperti makan, berjalan, atau berkomunikasi dengan hewan lainnya. 

## Inheritance

Konsep inheritance membantu kita untuk meminimalisir penulisan berulang pada fungsi, properti, dan variable.

Inheritance memungkinkan kita untuk mendefinisikan sebuah class (induk) ke class baru (anak) dan memberi kita kesempatan untuk menggunakan member dari class yang diwariskan tersebut.

Inheritance dapat didefinisikan juga sebagai proses di mana suatu objek memperoleh sifat dan perilaku dari objek lainnya. 

**SuperClass**

Sebuah class yang fitur-fiturnya akan diwariskan. Kelas seperti ini biasa dikenal juga dengan istilah Induk, Base, atau Parent Class.

**SubClass**

Anak/Children class yang akan mewarisi member milik Super Class. Namun, class ini tetap dapat memiliki membernya sendiri selain yang diwarisi dari SuperClass-nya.

### Single Inheritance

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/202004082056196718098881d5b29382a142eba8fe75f8.png)

Cara terumum yang mana class yang dibuat hanya mewarisi satu class. 

### Multilevel Inheritance

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200408205751d7ef58eeaabd83393dcd9dd954143530.png)

Cara ini mengacu pada mekanisme OOP, di mana SubClass dapat mewarisi SuperClass yang di mana merupakan sebuah SubClass dari SuperClass lain. 

### Multiple Inheritance

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/2020040821041262f2422cb20e50aeff72c7b4303723df.png)

Multiple inheritance mengacu pada konsep OOP di mana sebuah class dapat mewarisi lebih dari satu SuperClass. 

Namun perlu diketahui bahwa beberapa bahasa pemrograman seperti Java tidak mendukungnya secara penuh, dengan alasan suatu SubClass harus bisa mengatur ketergantungan dari 2 (dua) SuperClass-nya.

Multiple inheritance sendiri sangat jarang digunakan dalam pengembangan perangkat lunak karena sering menyebabkan permasalahan, terutama pada hirarki class yang berpotensi menyebabkan terjadinya kompleksitas tinggi.

### Hierarchical Inheritance

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200408210220d8c169491bd88f973229ac2542453dd2.png)

Jenis ini merupakan sebuah SuperClass yang diwarisi oleh beberapa SubClass.

### Hybrid Inheritance

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/202004082102419f3803b42624a300f3ef4d56c4aea7f1.png)

Jenis inheritance yang merupakan kombinasi dari beberapa inheritance. 

Jika kita melihat bagan di atas, sudah pasti kita membutuhkan interfaces jika ingin menerapkannya pada bahasa pemrograman seperti Java, atau protocol pada Swift.

## Encapsulation

Encapsulation merupakan proses di mana sebuah penanganan data ditempatkan di dalam wadah tunggal yang disebut sebagai class.

Saat menggunakan encapsulation, data dapat diisolasi dan tidak dapat diakses langsung dari luar. Dengan begini, kita cukup menggunakan data tersebut tanpa harus tahu bagaimana proses yang terjadi sampai data tersebut bisa digunakan.

Encapsulation bukan menyembunyikan sebuah data tetapi, encapsulation yang menyebabkan data tersebut tersembunyi.

## Abstraction

Abstraction adalah mekanisme saat proses dalam sebuah objek disembunyikan. Object tersebut hanya akan menyediakan apa yang benar-benar perlu digunakan.

Perbedaan Abstraction dengan Encapsulation:

* Saat menerapkan abstraction, kita cukup fokus pada apa yang dilakukan suatu objek tanpa harus tahu bagaimana itu dilakukan. Sedangkan encapsulation adalah bagaimana ia menyembunyikan mekanisme suatu objek ketika melakukan sesuatu.
* Jika Encapsulation menyembunyikan data dengan menyediakan getter setter untuk mengaksesnya, maka abstraction menyembunyikan sebuah implementasi dengan memanfaatkan abstract class, interface, dan lain sebagainya.

### Abstraction Layer

Abstraction layer atau abstraction level merupakan mekanisme yang memisahkan 2 (dua) kompleksitas sebuah sistem.

Dalam proses komputasi, abstraction layer atau level merupakan cara menyembunyikan detail implementasi yang kompleks dari serangkaian fungsionalitas tertentu dengan tujuan agar dapat memisahkan masalah seperti interoperabilitas.

## Polymorphism

Polymorphism merupakan kemampuan objek, variabel, atau fungsi yang dapat memiliki berbagai bentuk.

Secara umum polymorphism dalam OOP terjadi ketika suatu SuperClass direferensikan ke dalam SubClass

## Compile-time Polymorphism

Compile time polymorphism adalah sebuah proses di mana sebuah method atau fungsi dipanggil saat kompilasi.

Ini dapat terjadi karena sebuah konsep bernama method overloading. Method overloading merupakan kondisi di mana kita bisa membuat 2 (dua) atau lebih fungsi yang memiliki jumlah, tipe, dan urutan parameter yang berbeda di dalam sebuah class. 

Contoh penerapannya terbagi atas 2 (dua) yang didasari atas pengertian method overloading itu sendiri. 

**Parameter type**

~~~
class Arithmetic {
    func add(_ valueA: Int, _ valueB: Int) -> Int {
        return valueA + valueB
    }
    
    func add(_ valueA: UInt64, _ valueB: UInt64) -> UInt64 {
        return valueA + valueB
    }
    
    func add(_ valueA: Int, _ valueB: UInt64) -> UInt64 {
        return UInt64(valueA) + valueB
    }
    
    func add(_ valueA: UInt64, _ valueB: Int) -> UInt64 {
        return valueA + UInt64(valueB)
    }
}
~~~

Method overloading di atas dibedakan atas tipe argumen yang menjadi parameter dari fungsi tersebut.

Argumen yang disematkan ketika fungsi tersebut digunakan, mendasari berjalannya proses kompilasi.

**Parameter count**

Sebuah fungsi yang dapat memiliki nama yang sama namun jumlah parameter yang berbeda.

~~~
class Arithmetic {
    func add(_ valueA: Int, _ valueB: Int) -> Int {
        return valueA + valueB
    }
    
    func add(_ valueA: UInt64, _ valueB: UInt64) -> UInt64 {
        return valueA + valueB
    }
    
    func add(_ valueA: Int, _ valueB: UInt64) -> UInt64 {
        return UInt64(valueA) + valueB
    }
    
    func add(_ valueA: UInt64, _ valueB: Int) -> UInt64 {
        return valueA + UInt64(valueB)
    }
}
 
class Add : Arithmetic {
    override func add(_ valueA: Int, _ valueB: Int) -> Int {
        print("Calculate!")
        return super.add(valueA, valueB)
    }
}
~~~

### Runtime Polymorphism

Proses di mana sebuah fungsi dipanggil pada saat runtime.

Contoh dari runtime polymorphism adalah method overriding, yaitu sebuah kelas yang memiliki fungsi dengan nama sama dengan fungsi yang di dalam kelas induknya.

Method overriding adalah sebuah fitur pada sebuah bahasa pemrograman yang memungkinan sub class mewarisi sebuah implementasi yang spesifik dari sebuah fungsi yang ada pada kelas induknya (parent class). 

Implementasi pada sub class akan menimpa atau mengganti implementasi pada parent class.

~~~
func main() {
    let cat = Cat()
    cat.walk()
}
 
class Animal {
    func walk() {
        print("\(String(describing: type(of: self))) walk!")
    }
}
 
class Cat : Animal {
    override func walk() {
        print("Yeay! \(String(describing: type(of: self))) walked!")
    }
}
~~~