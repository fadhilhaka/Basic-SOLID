# Software Design Principle

Dalam pengembangan sebuah perangkat lunak, architecture berada pada tingkat tertinggi atau yang dikenal dengan istilah high-level, di mana definisinya merupakan sebuah pola arsitektur yang menentukan bentuk dan struktur keseluruhan  perangkat lunak. 

Sedangkan desain memiliki posisi di tingkat rendah atau istilahnya adalah low-level di bawah architecture. Desain juga memiliki definisi yaitu interkoneksi antara modul dan beberapa entitas perangkat lunak seperti packages, components, dan classes.

Software Design Principle merupakan sebuah pedoman yang dapat kita gunakan untuk menghindari design yang buruk saat mengembangkan sebuah perangkat lunak. 

Menurut Robert C. Martin, terdapat 3 (tiga) karakteristik penting dari design yang buruk yang perlu kita perhatikan dan sebaiknya dihindari.

## Rigidity

Dimulai dari rigidity atau kekakuan. Rigidity adalah kondisi suatu sistem yang sulit diubah, bahkan untuk perubahan yang paling sederhana [1](http://www.cvc.uab.es/shared/teach/a21291/temes/object_oriented_design/materials_adicionals/principles_and_patterns.pdf). 

Saat kita ingin melakukan perubahan, perubahan tersebut menyebabkan ketergantungan untuk mengubah item lain di dalam suatu modul. Alhasil, perubahan yang seharusnya dapat dilakukan dalam waktu yang singkat,  malah sebaliknya. Belum lagi dampaknya pada modul-modul lain yang saling berkaitan.

## Fragility

Selanjutnya adalah fragility. Fragility (kerapuhan) masih memiliki keterkaitan dengan rigidity. Fragility adalah kecenderungan perangkat lunak yang salah di beberapa bagian setiap kali melakukan perubahan [1](http://www.cvc.uab.es/shared/teach/a21291/temes/object_oriented_design/materials_adicionals/principles_and_patterns.pdf).

Seringkali kesalahan terjadi di area yang tidak memiliki hubungan konseptual dengan area yang diubah. Sehingga jika melakukan perbaikan, kadang takut timbul kesalahan dengan cara yang tidak terduga.

Ketika fragility ada di dalam suatu perangkat lunak, kemungkinan kesalahan akan meningkat seiring berjalannya waktu. Perangkat lunak semacam itu tak hanya sulit dipelihara, bahkan sulit juga dipertahankan.

## Immobility

Terakhir yang harus kita perhatikan dan hindari adalah Imobilitas. Yaitu sebuah ketidakmampuan untuk menggunakan kembali perangkat lunak dari proyek lain atau bagian-bagian dari proyek yang sama [1](http://www.cvc.uab.es/shared/teach/a21291/temes/object_oriented_design/materials_adicionals/principles_and_patterns.pdf).

Seorang engineer tentu akan mengalami kondisi di mana ia membutuhkan modul atau sistem yang sebelumnya sudah pernah ditulis atau dibuat oleh engineer lain. Namun, sering juga terjadi bahwa modul yang dibutuhkan tersebut memiliki terlalu banyak bobot yang bergantung padanya.

Setelah mencoba untuk memisahkan, para engineer menemukan bahwa pekerjaan dan risiko yang diperlukan untuk memisahkan bagian yang diinginkan (dari bagian yang tidak diinginkan), terlalu besar untuk ditoleransi. Sehingga alih-alih menulis ulang (re-write), sang engineer akan menggunakannya kembali untuk project lain.