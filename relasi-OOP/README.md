# Relasi pada OOP

Hubungan antar objek mendefinisikan bagaimana objek-objek tersebut akan berinteraksi atau berkolaborasi satu sama lainnya. 

Dalam hubungan antar objek terdapat 3 kategori:

* Association: memiliki hubungan “has-a” yang menyatakan bahwa sebuah kelas memiliki hubungan dengan kelas lainnya.
* Dependency: hubungan ini memiliki arti bahwa sebuah kelas memiliki ketergantungan terhadap kelas lain.
* Generalization: memiliki hubungan “is-a” dari kelas yang spesifik ke kelas yang lebih umum.

## Association

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200408220115ba016e06c411662a267ee82957c09b81.png)

Asosiasi didefinisikan sebagai hubungan yang terstruktur, yang secara konsep memiliki arti bahwa dua komponen saling terhubung satu sama lain. 

Jika dilihat pada gambar di atas, hubungan asosiasi digambarkan dengan garis tidak putus-putus dan tidak memiliki anak panah pada kedua ujungnya. Setiap objek tersebut memiliki siklus hidupnya sendiri dan tidak memiliki “ownership” antaranya.

### Kardinalitas

Hubungan asosiasi memiliki beberapa tipe: hubungan one-to-one, one-to-many, many-to-one, dan many-to-many, atau yang biasa disebut sebagai kardinalitas.

**One-to-one relationship**

Hubungan satu ke satu terjadi ketika satu objek A memiliki referensi dari satu objek B. Sebaliknya, satu objek B memiliki referensi dengan satu dari objek A. 

Sebagai contoh, kelas User hanya memiliki satu data diri dan tidak lebih.

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/2020040822081007d3f5107d6ad6c41c8287e3499beb1a.png)

**One-to-many relationship**

Hubungan satu ke banyak ini diartikan dengan hubungan antara dua objek A dan B di mana objek A terhubung dengan lebih dari satu objek B, tetapi anggota dari objek B hanya terhubung dengan satu anggota A.

Sebagai contoh, seorang pembeli dapat memiliki atau memesan minimal satu hingga beberapa pesanan. Semisal, class User dapat memiliki hubungan one-to-many terhadap class Order.

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200408220941e5064708e11dcae84073f25e6158db35.png)

**Many-to-many relationship**

Hubungan banyak ke banyak merupakan hubungan antara dua buah objek A dan B, di mana setiap anggota dari objek A maupun B memiliki hubungan lebih dari satu objek A dan B.

Sebagai contoh, seorang pengguna dapat membeli beberapa barang, tetapi satu buah barang juga dapat dibeli oleh beberapa pengguna.

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200408221052f1c7e15a1183a40b3b99336fd19b1b38.png)

Dalam hubungan asosiasi antara dua objek, terdapat dua bentuk relasi yaitu, agregasi dan komposisi. Kedua bentuk hubungan asosiasi ini dibedakan berdasarkan aturan khusus yang berlaku pada bentuk hubungan tersebut. 

### Aggregation

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/2020040822143239c50cc5834456bfb351ddbee1eb246b.png)

Bentuk hubungan pertama dari asosiasi adalah agregasi yang digambarkan dengan dengan garis yang tidak putus-putus dengan ujung simbol diamond putih yang mengarah pada class yang memiliki.

Meskipun sama-sama berupa hubungan yang “memiliki,”  perbedaan dengan bentuk hubungan komposisi adalah bentuk hubungan ini tidak terikat, yang berarti setiap class dapat berdiri sendiri. Kedua class dapat dibuat secara independen tanpa harus terdapat class lain saat pembuatannya. 

Seperti contoh pada gambar di atas, meskipun class Shop dihancurkan, class Seller masih dapat digunakan. Tapi tidak sebaliknya. Jika class Seller tidak ada, maka class Shop sudah tidak relevan lagi untuk digunakan.

### Composition

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/202004082215452de88d6950ab3a492945bd009a09e967.png)

Bentuk hubungan kedua yaitu komposisi, sebuah hubungan dapat dikatakan komposisi jika sebuah kelas “memiliki” class lainnya.

Sebuah class User memiliki bentuk hubungan komposisi dengan class Address yang ditandai dengan adanya anak panah dengan ujung diamond hitam penuh, yang mengarah pada class yang “memiliki” objek tersebut. Ketika class User hancur, maka class Address yang memiliki hubungan dengan class User tersebut akan ikut hancur dan tidak bisa digunakan lagi.

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200408221938befc8a123256ab7fa8a05d7efccfd2a9.png)

Bentuk hubungan komposisi lebih kuat dibandingkan dengan agregasi. Kita dapat melihat gambar di atas bahwa hubungan komposisi adalah bentuk hubungan terkuat dari ketiganya dan agregasi merupakan hubungan yang lebih umum lagi. 

Kedua bentuk hubungan ini merupakan bentuk hubungan antar objek yaitu asosiasi, hubungan asosiasi dapat dikatakan komposisi jika hubungan tersebut adalah hubungan “memiliki” dan dapat dikatakan hubungan agregasi jika terdapat objek yang “menggunakan” objek lainnya.

## Dependency

Hubungan dependensi diartikan sebagai hubungan antara dua buah class, di mana satu class memiliki ketergantungan dengan class lainnya tetapi class lainnya tidak/mungkin memiliki ketergantungan terhadap class pertama tadi. 

Jadi apa pun perubahan yang terjadi pada class pertama dapat mempengaruhi fungsi class yang memiliki ketergantungan pada class tersebut.

Hubungan dependensi terjadi apabila, sebuah fungsi pada class A membutuhkan class B sebagai parameter, fungsi pada class A memiliki nilai kembalian berupa class B, dan class A menggunakan class B tetapi class B bukan merupakan sebuah atribut. 

Kok mirip seperti hubungan asosiasi? Sebenarnya hubungan asosiasi sudah pasti memiliki hubungan dependensi. Hubungan asosiasi dapat  menjadi hubungan dependensi jika kelas yang dibutuhkan bukan merupakan atribut dari class yang membutuhkannya.

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200408222919f9805025821d67c40a3a89026fcbb1d2.png)

Hubungan dependensi digambarkan dengan garis putus-putus yang memiliki anak panah, di mana arah anak panah menunjukkan dependensinya. Pada gambar di atas kita dapat melihat bahwa kelas ShopService memiliki hubungan dengan kelas Product, tetapi kelas ShopService tidak memiliki atribut berupa kelas Product.

~~~
class ShopService {
    …
 
    func changeProductPrice(price: String, product: Product) {
        product.changePrice(price)
    }
}
 
class Product{
    private var _id: String
    private var _name: String
    private var _price: String
    
    init(id: String, name: String, price: String) {
        _id = id
        _name = name
        _price = price
    }
 
    ...
    
    func changePrice(_ value: String) {
        _price = value
    }
}
~~~

## Generalization and Specialization

### Generalization

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/202004082249296809bdbabc85f6dfd3aec55d00d67823.png)

Dalam hubungan generalisasi terjadi proses memisahkan karakteristik dari dua atau lebih class dan menggabungkannya jadi satu class yang lebih umum atau biasa kita sebut SuperClass. Karakteristik ini bisa seperti atribut, hubungan asosiasi, atau fungsi pada beberapa class.

Pada gambar di atas kita dapat melihat bahwa class Product merupakan SuperClass dari beberapa class lainnya. Sebabnya, class HealthProduct, ElectricProduct, dan ConsumeableProduct memiliki beberapa kesamaan yang bisa berupa atribut ataupun fungsi dari class-class tersebut dan dapat disatukan menjadi sebuah class yang lebih umum yaitu class Product.

### Specialization

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/202004082252495ac4f060f90fbaadcc03530a8ab4601b.png)

Berbanding terbalik dengan generalisasi, hubungan spesialisasi berarti membuat sebuah SubClass dari class yang sudah ada.

Pada gambar di atas jika kita membuat sebuah class Product yang memiliki beberapa atribut ataupun fungsi yang tidak diperlukan oleh class lainnya, maka kita dapat memecah class Product tersebut menjadi beberapa class lainnya. 

Misal, ketika pada sistem yang kita kembangkan akan menjual produk seperti baterai dan makanan ringan. Jika kita hanya membuat satu class saja yaitu class Product maka akan terdapat atribut seperti batteryCapacity yang tidak dibutuhkan oleh produk makanan ringan.

~~~
protocol Product {
    var id: String { get set }
    var name: String { get set }
    var price: String { get set }
}
 
class ElectronicProduct : Product {
    var id: String
    var name: String
    var price: String
    var productionDate: String    
    init(id: String, name: String, price: String, productionDate: String) {
        self.id = id
        self.name = name
        self.price = price
        self.productionDate = productionDate
    }
}
 
class ConsumableProduct : Product {
    var id: String
    var name: String
    var price: String
    var expirationDate: String
    init(id: String, name: String, price: String, expirationDate: String) {
        self.id = id
        self.name = name
        self.price = price
        self.expirationDate = expirationDate
    }
}
~~~

## Realization atau Implementation

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20200421084545f9a0da91f2b1678cca8e657fc298c0e5.png)

Hubungan realisasi atau implementasi adalah hubungan abstraksi khusus antara dua kelas, satu mewakili interface yang menjadi spesifikasinya (ProductService) dan yang lainnya mewakili kelas implementasi yang menjadi realisasinya (ProductServiceImpl).

Realisasi dapat digunakan dalam beberapa hal seperti untuk menyempurnakan sebuah kelas, optimasi, transformasi, template, model sintesis, komposisi kerangka kerja, dll. 

Jika melihat gambar di atas, hubungan realisasi ditandai dengan garis putus-putus yang memiliki simbol segitiga putih pada ujungnya yang mengarah pada kelas yang direalisasikan (supplier). 

Interface realization adalah hubungan realisasi khusus antara classifier dan interface. Hubungan ini menandakan bahwa classifier mengimplementasikan kontrak yang telah ditentukan oleh kelas interface.

Kelas classifier dapat mengimplementasikan satu atau beberapa kelas interface. Classifier yang mengimplementasikan interface mendukung serangkaian fitur yang dimiliki oleh kelas interface.

Selain mendukung fitur, kelas classifier harus mematuhi batasan yang dimiliki oleh kelas interface. Mari kita lihat implementasi pada kode berikut.