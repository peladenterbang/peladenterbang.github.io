# Background

Dalam sebuah penyimpanan laptop, desktop, maupun server memerlukan alat untuk menyimpan secara permanent. Tentu untuk mengantikan RAM yang hanya sebatas menyimpan data secara sementara. Karena ketika ram di isi data, saat dimatikan/direstart data tersebut akan hilang.Teknologi ram digunakan hanya untuk sebatas mengsupport prossesor karena kecepatan nya.Tapi bukan itu point yang di bahas kali ini, di perlukan alat yang di gunakan untuk menyimpan data secara permanent yaitu menggunakan HDD/SSD/NVMe yang teknologi didalam nya dengan menulis dalam sebuah piringan atau mencharge transistor agar saat dimatikan data tersebut tidak hilang selama data tersebut tidak dihapus atau perangkat tersebut rusak.

Sekarang kita ber alih ke perangkat lain yaitu server.Server merupakan perangkat computer yang di jalankan secaara terus-menerus guna dapat melayani client secara optimal berupa website,game,applikasi dan lain sebagainya. Server membutuhkan perangkat storage data dengan kapasitas besar dan performa yang sangat optimal.&#x20;

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Kasus, **pertama** ketika kita membutuhkan data storage dengan kapasitas **100TB** ? bagaimana kita dapat menyediakan storage tersebut, padahal **1 storage paling besar** saat ini adalah **26TB.** Lalu yang **kedua,** apabila storage tersebut rusak, bagaimana kita mengatasi nya ? kita tidak mau data data yang ada di dalam storage tersebut hilang tentunya saat storage kita rusak. **Ketiga** , ketika storage storage yang tersedia besar apaka menjamin I/O bekerja dengan maximal?, karena membutuhkan lebih banyak block yang harus di baca.

Dengan kasus kasus diatas tentunya insinyur IT telah memikirkan itu semua. Apa pemecahan masalah yang di hadapi saat ini ? Teknologi apa yang harus di terapkan ? lalu bagaimana penerapan nya ?, untuk itu kita bahas satu persatu.

Untuk menyediakan kapasitas yang besar kita membutuhkan beberapa storage yang di gabung menjadi satu kesatuan, dan yang satu kesatuan itu dapat di pecah lagi menjadi ukuran ukuran volume yang kita inginkan. Lalu storage tersebut sudah otomatis ter replikasi agar saat salah satu disk rusak masih ada data yang tersimpan dalam storage lain  nya. Ketika jumlah disk storage yang banyak maka I/O yang di hasilkan seharus nya lebih besar di bandingkan dengan 1 disk storage dengan kamasitas besar.

Dalam penyelesaian masalah di atas, sederhana nya dapat kita gambarkan sebagai berikut : &#x20;

<img src="../../.gitbook/assets/file.drawing (2).svg" alt="" class="gitbook-drawing">

Teknologi apa yang memungkinkan untuk menerapkan pendekatan seperti gambar di atas? apakah bisa menggunkana RAID ? atau NAS? keduanya hanya terbatas dalam 1 node untuk management nya , ketika butuh backup ke node lain kita harus mengatur secara manual agar data ter backup ke dalam node lain nya, kita butuh yang lebih canggih. Ceph, moosefs, LeoFS, XtreemFS, GlusterFS dan masih banyak lagi pihak ke tiga yang meyediakan software Distributed File System (DFS). Kali ini kita akan fokus ke ceph.&#x20;

Halaman berikut nya kita akan belajar tentang ceph. bagaimana dia bekerja dalam me manage disk storage yang ada.
