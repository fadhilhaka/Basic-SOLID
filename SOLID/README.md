# SOLID

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200423171403c7df7b777d495b81fe9cabaf74e759e2.png)

OOP dan SOLID merupakan 2 (dua) hal yang berbeda. 

OOP adalah sebuah paradigma untuk menuliskan program yang sudah diadaptasi oleh beberapa bahasa pemrograman, sedangkan SOLID merupakan kumpulan principle untuk membantu kita  mengembangkan sebuah perangkat lunak dengan tingkat kekukuhan yang tinggi.

## Tujuan SOLID

Menulis kode yang dapat dengan mudah diekstensi (extended) dan dipertahankan (maintained).

Prinsip SOLID bukanlah suatu hukum atau aturan tertentu yang wajib kita patuhi, melainkan sebuah prinsip yang dimaksudkan untuk membantu kita dalam menuliskan kode yang rapi.

Berikut adalah tujuan dari prinsip SOLID dalam pembuatan struktur mid-level perangkat lunak:

* Toleran terhadap perubahan [2](https://learning.oreilly.com/library/view/clean-architecture-a/9780134494272/).
* Mudah dipahami [2](https://learning.oreilly.com/library/view/clean-architecture-a/9780134494272/).
* Komponen dasar dapat digunakan kembali dalam bentuk software system lainnya [2](https://learning.oreilly.com/library/view/clean-architecture-a/9780134494272/).

Istilah mid-level yang merujuk pada prinsip SOLID ini diterapkan oleh engineer yang bekerja pada level module [2](https://learning.oreilly.com/library/view/clean-architecture-a/9780134494272/).

Prinsip ini diterapkan tepat di atas level kode. Manfaatnya, ia dapat membantu menentukan jenis struktur perangkat lunak yang digunakan dalam modul dan komponen. 

Setelah komponen tersebut dapat kita desain dengan baik menggunakan prinsip SOLID, maka selanjutnya kita dapat melanjutkan ke dalam prinsip-prinsip arsitektur tingkat tinggi (high-level architecture) [2](https://learning.oreilly.com/library/view/clean-architecture-a/9780134494272/). 

## Single Responsibility Principle (SRP)

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200430161018b26cbb7406f733e49c4e99847ad1c0d8.png)

>"A module should be responsible to one, and only one, actor."  
[(Robert Cecil Martin, 2017)](https://learning.oreilly.com/library/view/clean-architecture-a/9780134494272/)

SRP digunakan untuk mengatur tanggung jawab dari sebuah entitas yang berada di dalam sebuah proyek dalam hal ini adalah sebuah module/class untuk memenuhi kebutuhan dari actor. Actor merupakan kumpulan "user" atau "stakeholder" yang menginginkan perubahan pada perangkat lunak kita [2](https://learning.oreilly.com/library/view/clean-architecture-a/9780134494272/).

Tanggung jawab (responsibility) berarti bahwa jika suatu class punya 2 (dua) fungsionalitas yang tak miliki keterkaitan untuk melakukan suatu perubahan, maka kita harus membagi fungsionalitas yang berbeda tersebut dengan cara memisahkannya menjadi dua class yang berbeda. 

Setiap class yang sudah dipisahkan berdasarkan fungsionalitasnya hanya akan menangani satu tanggung jawab. Sehinga, jika kita melakukan perubahan tanggung jawab, kita cukup fokus pada masing-masing class yang sudah dipisahkan tersebut.

Untuk mengetahui seperti apa penerapan Single Responsibility Principle (SRP), kita akan membuat sebuah contoh kasus tentang layanan product makanan dengan skenario berikut:

Pada sebuah proyek kita mempunyai sebuah class yang bertanggung jawab untuk menangani pelayan dengan nama FoodService. Nah, Di dalamnya terdapat properti id, name, dan date. 

~~~
import Foundation
 
class FoodService{
    private var _id: Int
    private var _name: String
    private var _date: String
    
    init(id: Int, name: String, date: String) {
        _id = id
        _name = name
        _date = date
    }
    
    func addToStore() {
        if (!isExpired()) {
            //Add to store
        }
    }
    
    private func isExpired() -> Bool {
        var foodDate = NSDate()
        let now = NSDate()
        let dateFormater = DateFormatter()
        dateFormater.dateFormat = "yyyy-mm-dd"
        
        foodDate = dateFormater.date(from: _date)! as NSDate
        
        return foodDate.compare(now as Date) == ComparisonResult.orderedDescending
    }
}
~~~

Dari contoh kode di atas, kita bisa melihat beberapa fungsionalitas yaitu fungsi untuk memasukkan objek ke dalam store dengan nama addToStore() dan fungsi untuk mengecek kadaluarsa dari produk makanan dengan nama isExpired().

Pada fungsi isExpired(), di dalamnya terdapat beberapa baris kode untuk membandingkan tanggal guna mengetahui masa kadaluarsa. Kita juga bisa melihat jika di dalam fungsi tersebut terdapat baris kode untuk melakukan format tanggal berdasarkan pattern yang sudah ada dan tentunya kode untuk melakukan parse tanggal guna mendapatkan waktu kadaluarsa yang valid.

Di sini kita sudah bisa melihat terdapat 2 (dua) tanggung jawab yang berbeda tetapi tidak masalah karena ketika digunakan. Class FoodService akan berfungsi dengan semestinya. 

Tapi, bagaimana jika terjadi perubahan pada fungsi isExpired() seperti perubahan pattern atau locale (bahasa) pada platform? Tentunya kita bisa mengubahnya langsung di dalam kelas tersebut. Namun seperti yang kita ketahui, FoodService sendiri bertanggung jawab untuk menangani pelayanan makanan. Bukan untuk menangani waktu kadaluarsa produk.

Untuk itu, kita harus memisahkan fungsi isExpired() ke dalam class tersendiri.

~~~
import Foundation
 
class FoodService{
    private var _id: Int
    private var _name: String
    private var _date: String
    
    init(id: Int, name: String, date: String) {
        _id = id
        _name = name
        _date = date
    }
    
    func addToStore() {
        if (!FoodExpiry.isExpired(date: _date)) {
            //Add to store
        }
    }
}
 
class FoodExpiry {
    static func isExpired(date: String) -> Bool {
        var foodDate = NSDate()
        let now = NSDate()
        let dateFormater = DateFormatter()
        dateFormater.dateFormat = "yyyy-mm-dd"
        
        foodDate = dateFormater.date(from: date)! as NSDate
        
        return foodDate.compare(now as Date) == ComparisonResult.orderedDescending
    }
}
~~~

Dengan memisahkannya ke dalam class tersendiri, kita tinggal fokus pada kelas yang memiliki tanggung jawabnya. Dengan memisahkannya seperti kode di atas, FoodExpiry dapat digunakan pada kelas lainnya yang membutuhkan tanpa harus bergantung pada kelas FoodService seperti pada contoh kode sebelumnya.

Single Responsibility Principle (SRP) merupakan cara yang baik untuk mengidentifikasi class selama fase desain aplikasi, dan mengingatkan Anda untuk memikirkan semua cara agar class dapat dikembangkan tanpa adanya masalah berarti. 

Pemisahan tanggung jawab yang baik dilakukan hanya ketika sebuah gambaran lengkap aplikasi secara keseluruhan tentang bagaimana aplikasi itu dapat bekerja, telah dibuat dan dipahami dengan baik. Sehingga kita dapat memisahkannya dengan rinci.

## Open/Close Principle (OCP)

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200430150245c1ab94f145a97f67feb1a96d0f400bc3.png)

>"A software artifact should be open for extension but closed for modification."
[(Bertrand Meyer, 1988)](https://learning.oreilly.com/library/view/clean-architecture-a/9780134494272/)

Pada Tahun 1988, seorang profesor asal Perancis, Bertrand Meyer menulis sebuah buku yang berjudul Object Oriented Software Construction. Di dalamnya terdapat sebuah aturan yang mengatur di mana sebuah artefak perangkat lunak harus terbuka untuk ditambahkan tetapi tertutup untuk dimodifikasi. 

Aturan tersebut kemudian ditulis lagi pada sebuah artikel yang berjudul The Open-Closed Principle oleh Robert C. Martin pada tahun 1996.

Terbuka untuk ditambahkan adalah keadaan ketika sebuah sistem dapat ditambahkan dengan spesifikasi baru yang dibutuhkan. 

Sedangkan tertutup untuk dimodifikasi adalah agar ketika ingin menambahkan spesifikasi baru, kita tidak perlu mengubah atau memodifikasi sistem yang telah ada.

Secara umum, penggunaan aturan open/close diterapkan dengan memanfaatkan interface dan abstraksi kelas daripada menggunakan sebuah kelas konkret. Penggunaan interface dan abstraksi kelas bertujuan agar dapat mudah diperbaiki setelah pengembangan tanpa harus mengganggu kelas yang mewarisi dan ketika ingin membuat fungsionalitas baru, cukup dengan membuat kelas baru dan mewarisi interface atau abstraksi tersebut.

Untuk mengetahui seperti apa penerapan Open/Close Principle, kita akan menggunakan sebuah skenario sederhana di mana kita mempunyai sebuah fitur untuk melakukan checkout product. 

~~~
class Product{
    /** Product entities */
}
 
class ShippingOrderService {
    
    func checkout(product: Product, type: ShippingType){
        switch type {
        case ShippingType.JNE:
            /** do checkout product with this shipping type */
            break
        case ShippingType.TIKI:
            /** do checkout product with this shipping type */
            break
        default:
            print("Unsupported shipping type")
        }
    }
}
~~~

Di dalam class ShippingOrderService di atas terdapat sebuah fungsi dengan parameter berupa enum:

~~~
enum ShippingType {
   case JNE, TIKI
}
~~~

Fungsi checkout yang berada pada class ShippingOrderService di atas memiliki beberapa statement untuk menentukan nilai biaya kirim product berdasar jenis pengiriman. Untuk saat ini, kode di atas dapat menjalankan tugasnya dengan baik. Tetapi, suatu saat dengan kode di atas, jika kita diminta untuk menambahkan jenis pengiriman baru, tentunya kita akan membuat konstanta baru dan menjadikannya kondisi pada statement untuk menentukan tugas yang akan dijalankan. 

~~~
class Product{
    /** Product entities */
}
 
class ShippingOrderService {
    
    func checkout(product: Product, type: ShippingType){
        switch type {
        case ShippingType.JNE:
            /** do checkout product with this shipping type */
            break
        case ShippingType.TIKI:
            /** do checkout product with this shipping type */
            break
        case ShippingType.POSINDO:
            /** do checkout product with this shipping type */
            break
        default:
            print("Unsupported shipping type")
        }
    }
}

enum ShippingType {
    case JNE, TIKI, POSINDO
}
~~~

Cara tersebut melanggar prinsip dasar open/close principle karena kita melakukan perubahan pada kode yang telah ada. Lantas bagaimana cara untuk mencapai penerapan aturan open/close principle? 

Pertama, hapus class enum yang berisi beberapa jenis pengiriman dan gantilah dengan beberapa class tersendiri yang di dalamnya terdapat fungsi yang sesuai dengan yang dibutuhkan. 

~~~
protocol Shipping {
    func calculate(product: Product) -> Int
}
 
class JNEShipping: Shipping {
    func calculate(product: Product) -> Int {
        return /** calculate amount of this type with product*/
    }
}
 
class TIKIShipping: Shipping {
    func calculate(product: Product) -> Int {
        return /** calculate amount of this type with product*/
    }
}
~~~

Kemudian untuk class ShippingOrderService, dapat disederhanakan seperti berikut ini:

~~~
class ShippingOrderService {
    func checkout(product: Product, shipping: Shipping){
        let costShipping = shipping.calculate(product: product)
        /** Code to do check */
    }
}
~~~

Sampai saat ini, kode yang sudah kita ubah di atas dapat berjalan dengan baik dan tentunya sudah mengikuti aturan dari open/close principle. Ini bisa dibuktikan ketika ingin menambahkan jenis pengiriman baru, kita cukup membuat class baru tanpa harus mengubah kode yang berada di dalam class ShippingOrderService.

~~~
class ShippingOrderService {
    func checkout(product: Product, shipping: Shipping){
        let costShipping = shipping.calculate(product: product)
        /** Code to do check */
    }
}
 
protocol Shipping {
    func calculate(product: Product) -> Int
}
 
class JNEShipping: Shipping {
    func calculate(product: Product) -> Int {
        return /** calculate amount of this type with product*/
    }
}
 
class TIKIShipping: Shipping {
    func calculate(product: Product) -> Int {
        return /** calculate amount of this type with product*/
    }
}
 
class POSINDOShipping: Shipping{
    func calculate(product: Product) -> Int {
        return /** calculate amount of this type with product*/
    }
}
 
class SiCepatShipping: Shipping{
    func calculate(product: Product) -> Int {
        return /** calculate amount of this type with product*/
    }
}
~~~

Saat menerapkan open/close principle ke dalam project, kita bisa membatasi kebutuhan untuk mengubah kode yang telah ditulis, diuji dan di-debug. Tujuannya untuk menghindari resiko atau kelemahan sistem yang bisa saja terjadi. 

Selain itu, kita bisa menghindari ketergantungan dan meningkatkan fleksibilitas sistem. Tentunya ini akan meringankan proses skalabilitas dari sisi pengembangan perangkat lunak.

## Liskov Substitution Principle (LSP)

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200430161059889ba363fb6ec5aeaa1f92b144c57083.png)

>“If for each object o1 of type S there is an object o2 of type T such that for all programs P defined in terms of T, the behaviour of P is unchanged when o1 is substituted for o2 then S is a subtype of T.”
[Barbara Liskov](https://learning.oreilly.com/library/view/clean-architecture-a/9780134494272/)

Sederhananya, Liskov’s substitution adalah aturan yang berlaku untuk hirarki pewarisan. Hal ini mengharuskan kita untuk mendesain kelas-kelas yang kita miliki sehingga ketergantungan antar klien dapat disubstitusikan tanpa klien mengetahui tentang perubahan yang ada.

Oleh karena itu, seluruh SubClass setidaknya dapat berjalan dengan cara yang sama seperti SuperClass-nya.

Untuk menjadikan sebuah kelas benar-benar menjadi SubClass, kelas tersebut tidak hanya wajib untuk menerapkan fungsi dan properti dari SuperClass, melainkan juga harus memiliki perilaku yang sama dengan SuperClass-nya. Untuk mencapainya, terdapat beberapa aturan yang harus dipatuhi. 

### Contravariant and Covariant

Contravariant adalah kondisi di mana parameter dari sebuah fungsi yang berada pada SubClass harus memiliki tipe dan jumlah yang sama dengan fungsi yang berada pada SuperClass-nya. 

Covariant adalah kondisi pengembalian nilai dari fungsi yang berada pada SubClass dan SuperClass.

### Preconditions and Postconditions

Selanjutnya adalah aturan preconditions dan postconditions. Ini merupakan tindakan yang harus ada sebelum atau sesudah sebuah proses dijalankan. 

Contohnya, ketika kita ingin memanggil sebuah fungsi yang digunakan untuk membaca data dari database, terlebih dahulu kita harus memastikan database tersebut dalam keadaan terbuka agar proses dapat dijalankan. Ini disebut sebagai precondition. 

Sedangkan postcondition, contohnya saat proses baca tulis di dalam database telah selesai, kita harus memastikan database tersebut sudah tertutup.

### Invariant

Dalam pembuatan sebuah SubClass, SubClass tersebut harus memiliki invariant yang sama dengan SuperClass-nya. 

Invariant sendiri adalah penjelasan dari kondisi suatu proses yang benar sebelum proses tersebut dimulai dan tetap benar setelahnya.

### Constraint

Secara default, SubClass dapat memiliki fungsi dan properti dari SuperClass-nya. Selain itu, kita juga dapat menambahkan member baru di dalamnya. 

Constraint di sini adalah pembatasan yang ditentukan oleh SuperClass terhadap perubahan keadaan sebuah obyek. 

Sebagai contoh misal SuperClass memiliki obyek yang memiliki nilai tetap, maka SubClass tidak diijinkan untuk mengubah keadaan dari nilai obyek tersebut.

~~~
protocol Product {
    var name: String { get }
    var expiredDate: Date { get }
    
    /**
     * Function to get all of information about product
     */
    func getProductInfo()
}
 
class Vegetable: Product{
    var name: String {
        return "Broccoli"
    }
    
    var expiredDate: Date {
        return Date()
    }
 
    func getProductInfo() {
        // some magic code
    } 
}
~~~

Pada contoh kode di atas kita memiliki sebuah kelas abstract bernama Product yang di dalamnya terdapat pula beberapa member abstract . Kelas tersebut diwariskan oleh kelas lain yaitu kelas Vegetable. Untuk saat ini, kelas tersebut dapat berjalan dengan baik sesuai dengan fungsinya.

Selanjutnya kita membutuhkan sebuah kelas produk baru. Katakanlah produk smartphone. Untuk itu, kita tinggal membuat kelas baru yang mewarisi kelas Product karena kelas tersebut merupakan abstraksi dari sebuah kelas produk.

~~~
protocol Product {
    var name: String { get }
    var expiredDate: Date { get }
    
    /**
     * Function to get all of information about product
     */
    func getProductInfo()
}
 
class Vegetable: Product{
    var name: String {
        return "Broccoli"
    }
    
    var expiredDate: Date {
        return Date()
    }
 
    func getProductInfo() {
        // some magic code
    }
}
 
class Smartphone: Product{
    var name: String {
        return "Samsung S10+ Limited Edition"
    }
    
    var expiredDate: Date {
        return Date() // ?????
    }
    
    func getProductInfo() {
        // some magic code
    }
}
~~~

Pada kode di atas hubungan antara kelas Product dan kelas Vegetable sudah benar dan dapat berjalan dengan baik. Tapi jika kita perhatikan pada kelas Smartphone, di dalamnya terdapat member yang nilainya adalah masa kedaluwarsa produk yang harus kita tentukan. Namun seperti yang kita ketahui, sebuah smartphone tidaklah mempunyai masa kedaluwarsa. Dalam kasus ini kelas Product menjadi tidak relevan untuk diwariskan ke kelas Smartphone dan ini tentunya melanggar aturan SubClass yang sudah kita pelajari di modul sebelumnya.

Untuk mengatasi kasus di atas, kita perlu melakukan substitusi fungsi yang tidak relevan tersebut ke dalam kelas abstraksi sendiri dan diwariskan pada kelas yang relevan. Namun, Perubahan ini tetap menjadikan kelas Product sebagai SuperClass dari hirarki yang ada saat ini.

~~~
protocol Product {
    var name: String { get }
    
    /**
     * Function to get all of information about product
     */
    func getProductInfo()
}
 
protocol FoodProduct: Product {
    var expiredDate: Date { get }
}
 
class Vegetable: FoodProduct{
    var name: String {
        return "Broccoli"
    }
    
    var expiredDate: Date {
        return Date()
    }
    
    func getProductInfo() {
        // some magic code
    }
}
 
class Smartphone: Product {
    var name: String {
        return "Samsung S10+ Limited Edition"
    }
    
    func getProductInfo() {
        // some magic code
    }
}
~~~

Dengan perubahan kode seperti di atas, kita sudah memenuhi aturan yang ada. Mudah bukan? Liskov’s Substitution principle merupakan prinsip yang dapat meningkatkan design dari sistem yang kita kembangkan. Sehingga ketergantungan antar klien dapat disubstitusikan tanpa klien tahu perubahan yang ada.

## Interface Segregation Principle (ISP)

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/2020043016113815e57b528ff843b8ce30912be4980376.png)

>"Clients should not be forced to depend upon interfaces that they do not use." 
(Robert Cecil Martin)

Prinsip ini sendiri bertujuan untuk mengurangi jumlah ketergantungan sebuah class terhadap interface class yang tidak dibutuhkan.

Pada saat kita membuat sebuah sistem, pasti kita pernah membuat sebuah class yang memiliki atau mengimplementasikan beberapa public interface dan interface-interface tersebut juga digunakan dan di implementasi oleh class lainnya dalam sistem kita. Class-class yang kita buat ini terkadang hanya membutuhkan beberapa fungsi yang ada pada interface tersebut sehingga menurut aturan prinsip interface segregation hal ini kurang baik. 

Tapi tenang, ketika prinsip interface segregation diterapkan, setiap class-class akan mengimplementasi beberapa interface class yang lebih kecil sesuai dengan fungsi-fungsi yang dibutuhkan class-class tersebut. 

Hal ini berarti bahwa class-class yang saling bergantung dapat berkomunikasi dengan menggunakan interface yang lebih kecil, mengurangi ketergantungan pada fungsi-fungsi yang tidak digunakan dan mengurangi coupling. 

Dengan menggunakan interface yang lebih kecil akan memudahkan dalam implementasi, meningkatkan fleksibilitas dan juga kemungkinan untuk digunakan kembali (reuse).

~~~
protocol IPayment {
    func setPaymentName()
    func setAmount()
    func bankID()
    func virtualBankID()
    func accountID()
}
 
class Gopay : IPayment {
    
    func setPaymentName() {
        // Implementation code
    }
    
    func setAmount(){
        // Implementation code
    }
    
    func bankID(){
        // Implementation code
    }
    
    func virtualBankID(){
        // Implementation code
    }
    
    func accountID(){
        // Implementation code
    }
}
 
class Mandiri : IPayment {
    
    func setPaymentName() {
        // Implementation code
    }
    
    func setAmount(){
        // Implementation code
    }
    
    func bankID(){
        // Implementation code
    }
    
    func virtualBankID(){
        // Implementation code
    }
    
    func accountID(){
        // Implementation code
    }
}
 
class BNI : IPayment {
    
    func setPaymentName() {
        // Implementation code
    }
    
    func setAmount(){
        // Implementation code
    }
    
    func bankID(){
        // Implementation code
    }
    
    func virtualBankID(){
        // Implementation code
    }
    
    func accountID(){
        // Implementation code
    }
}
~~~

Jika kita perhatikan kode di atas, terdapat sebuah class interface dengan nama IPayment yang diimplementasi oleh class Gopay, Mandiri, dan BNI. Di mana class-class tersebut memiliki semua fungsi yang ada pada class interface IPayment. 

Semua class tersebut membutuhkan interface IPayment untuk mengurangi pembuatan fungsi yang berulang di setiap kelas tersebut dan mempermudah kita untuk mengatur dependensi. Namun seperti yang kita ketahui, class Mandiri dan BNI bukanlah sebuah metode pembayaran EWallet seperti halnya class Gopay.

Nah dalam kasus ini, kita akan mendapati beberapa kontrak yang tidak digunakan di masing-masing class yang mana ini merupakan sebuah kondisi yang melanggar aturan dari prinsip Interface Segregation.

Untuk menyelesaikan kasus di atas, kita akan sedikit mengubah beberapa potongan kode sebelumnya dengan memecah beberapa kontrak yang tidak digunakan pada interface IPayment menjadi sebuah interface tersendiri yang tentunya sesuai dengan kebutuhan masing-masing class.

~~~
protocol EWalletProvider {
   func accountID()
   func walletProviderID()
}
 
protocol PaymentProvider {
   func paymentName()
   func amount()
}
 
protocol BankProvider {
   func bankID()
   func virtualAccount()
}
~~~

Bisa kita perhatikan, interface IPayment yang sebelumnya memiliki beberapa kontrak, sekarang sudah menjadi beberapa interface tersendiri sesuai dengan apa yang dibutuhkan.

Langkah selanjutnya adalah mengubah implementasi dari beberapa kelas yang sebelumnya mengimplementasi interface IPayment. Untuk class Gopay diubah menjadi class yang mengimplementasi interface EWalletProvider dan PaymentProvider. 

Sedangkan class Mandiri dan BNI diubah menjadi class yang mengimplementasi interface BankProvider dan PaymentProvider.

~~~
class Gopay : EWalletProvider, PaymentProvider {
    func paymentName() {
        // Implementation code
    }
    func amount() {
        // Implementation code
    }
    func accountID() {
        // Implementation code
    }
    func walletProviderID() {
        // Implementation code
    }
}
 
class Mandiri : BankProvider, PaymentProvider {
    func paymentName() {
        // Implementation code
    }
    func amount() {
        // Implementation code
    }
    func bankID() {
        // Implementation code
    }
    func virtualAccount() {
        // Implementation code
    }
}
 
class BNI : BankProvider, PaymentProvider {
    func paymentName() {
        // Implementation code
    }
    func amount() {
        // Implementation code
    }
    func bankID() {
        // Implementation code
    }
    func virtualAccount() {
        // Implementation code
    }
}
~~~

Dengan memecah interface menjadi beberapa interface kecil, kita dapat dengan mudah menyesuaikan kebutuhan masing-masing class. Kita juga dapat dengan mudah menambahkan class-class baru yang mengimplementasi interface yang sesuai. 

Semisal kita ingin menambahkan class EWallet baru yaitu OVO. Maka kita hanya perlu membuat class OVO mengimplementasikan interface EWalletProvider dan PaymentProvider.

Interface Segregation Principle dapat membantu kita untuk mengembangkan sistem yang kukuh dan mudah dipelihara. Kita dapat mencegah pembuatan interface yang memiliki banyak fungsi untuk kepentingan yang berbeda-beda.

## Dependency Inversion Principle (DIP)

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/202004301612143eac1ab309e856710e6d8b10caa662f6.png)

Pada prinsip Dependency Inversion terdapat dua pernyataan atau aturan yang perlu kita ketahui, yang pertama adalah high-level module tidak diperbolehkan untuk bergantung pada low-level module. Keduanya harus bergantung pada abstraction. 

Pernyataan yang kedua, abstraksi tidak diperbolehkan untuk bergantung pada detail. Detail harus bergantung pada abstraksi.

>"High-level modules should not depend on low-level modules. Both should depend on abstractions." 
(Robert Cecil Martin)

Prinsip Dependency Inversion hampir sama dengan konsep layering dalam aplikasi, di mana low-level modules bertanggung jawab dengan fungsi yang sangat detail dan high-level modules menggunakan low-level classes untuk mencapai tugas yang lebih besar. 

Hal ini bisa dicapai dengan bergantung pada sebuah abstraksi, ketika ada ketergantungan antar kelas seperti interface, daripada referensi langsung ke kelas lainnya.

High-level modules adalah kelas-kelas yang berurusan dengan kumpulan-kumpulan fungsionalitas. Pada hirarki tertinggi terdapat kelas-kelas yang mengimplementasikan aturan bisnis sesuai dengan desain yang telah ditentukan. 

Low-level modules bertanggung jawab pada operasi yang lebih detail. Pada level terendah memungkinkan modul ini untuk bertanggung jawab dalam menulis informasi ke database atau menyampaikan pesan ke sistem operasi. 

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/202004061045114485e0544f3d45306d40612a72780852.jpeg)

Hirarki di atas adalah gambaran fitur sebuah transaksi yang digunakan untuk berinteraksi dengan database. Terdapat class PaymentService yang digunakan untuk melakukan pembayaran dan class MySQLDatabase yang bertanggung jawab menyimpan data tersebut ke dalam database.

Pada sistem ini juga akan terdapat fungsi-fungsi untuk menambah atau menghapus data pembayaran. Untuk melakukan pembayaran kita akan membutuhkan class yang merupakan high-level yaitu class PaymentService. 

Jika kita melihat penerapan pada class tersebut, permasalahan yang ada adalah class tersebut bergantung pada class database dan memiliki referensi langsung pada class tersebut sebagai propertinya. 

Akibatnya, mustahil kita mengganti tipe data dari class tersebut atau ketika kita ingin menambahkan database baru. Kecuali, class-class yang akan kita tambahkan merupakan SubClass dari class MySQLDatabase. 

Namun, dengan menambahkan class baru tersebut, kita dapat menyalahi prinsip Liskov Substitution. Kenapa? Sebabnya, kita membutuhkan perubahan lagi pada class PaymentService yang berarti kita menyalahi aturan lainnya yaitu Open/Close Principle.

Masalah lainnya yang akan timbul adalah ketika kita membutuhkan perubahan pada class MySQLDatabase, di mana perubahan yang ada pada class tersebut dapat mempengaruhi class di atasnya yaitu PaymentService.

Hal ini juga memungkinkan kita untuk mengubah class-class lainnya yang berada pada hierarki di atasnya, ketika sistem kita terus berkembang, permasalahan ini akan tetap terus ada dan semakin membuat kita kesusahan dalam mengembangkan sistem yang kukuh.

Dengan menerapkan prinsip Dependency Inversion, kita dapat menyelesaikan permasalahan-permasalahan ini dengan menghapus ketergantungan langsung antar class. Bagaimana caranya? Kita dapat mengubah ketergantungan antar class dengan membuat class-class tersebut bergantung pada abstraksi, seperti interface atau abstract class.

Pada lower-level, class-class yang ada dapat mengimplementasikan interfaces, atau mewariskan fungsi-fungsi dari abstract class. Dengan begitu, perubahan yang ada pada class-class di lower-level tidak akan mempengaruhi hirarki di atasnya, dengan syarat kita tidak mengubah abstraksi yang dibutuhkan.

Manfaat lainnya dari penggunaan atau penerapan prinsip ini dapat meningkatkan kekukuhan dan fleksibilitas dari sistem yang kita kembangkan. Tanpa penerapan prinsip Dependency,Inversion, hanya class-class lower-level saja yang mudah digunakan kembali.

~~~
class PaymentService {
    
    private let database: MySQLDatabase = MySQLDatabase()
    
    func paymentIsValid() {
       // Implementation code
    }
    
    func openDatabase() {
       // Implementation code
    }
    
    func addNewPayment() {
       // Implementation code
    }
    
    func removePaymentByID() {
       // Implementation code
    }
    
    func updatePaymentByID() {
       // Implementation code
    }
}
 
class MySQLDatabase {
    
    func insert() {
        // Implementation code
    }
    
    func update() {
        // Implementation code
    }
    
    func delete() {
        // Implementation code
    }
}
~~~

Untuk memperbaiki contoh kode di atas agar sesuai dengan prinsip Dependency Inversion, kita dapat menghapus ketergantungan langsung class PaymentService terhadap class MySQLDatabase.

Kita akan menambahkan abstract class baru sehingga nantinya ketika kita menambahkan implementasi baru untuk database, kita hanya akan mewariskan dari class Database.

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/2020040610510835998319833072e8f02f1489525746db.jpeg)

Class abstract yang akan kita tambahkan, yaitu class Database, akan berada pada high-level dari hierarki class. Sedangkan class MySQLDatabase dan MongoDatabase akan menjadi SubClass dari class tersebut sehingga tidak ada ketergantungan langsung pada class yang menjadi implementasi database.

Hal ini akan memudahkan kita untuk menambahkan atau mengganti kode pada class di bawahnya tanpa mempengaruhi class pada hirarki di atasnya.

~~~
class PaymentService {
 
    private let _database: Database
    
    init(database: Database) {
        _database = database
    }
 
    func paymentIsValid() {
       // Implementation code
    }
    
    func openDatabase() {
       // Implementation code
    }
    
    func addNewPayment() {
       // Implementation code
    }
    
    func removePaymentByID() {
       // Implementation code
    }
    
    func updatePaymentByID() {
       // Implementation code
    }
}
 
 
protocol Database {
    func insert()
    func update()
    func delete()
}
 
 
class MySQLDatabase : Database {
 
    func insert() {
        // Implementation code
    }
    
    func update() {
        // Implementation code
    }
    
    func delete() {
        // Implementation code
    }
}
 
class MongoDatabase : Database {
 
    func insert() {
        // Implementation code
    }
    
    func update() {
        // Implementation code
    }
    
    func delete() {
        // Implementation code
    }
}
~~~

Dependency Inversion Principle merupakan prinsip ke-5 dan terakhir dari S.O.L.I.D. Dalam prinsip ini dikenalkan abstraksi sebagai antarmuka antara komponen yang memilik hierarki tinggi (higher-level) dan komponen yang memiliki hierarki rendah (lower-level) untuk menghilangkan ketergantungan antara kedua hierarki tersebut.