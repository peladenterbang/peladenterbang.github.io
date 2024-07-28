# Docker

Docker merupakan perangkat lunak management container yang banyak di gunakan di tech company.

Kemudahan dalam pengelolaan nya membuat docker banyak diminati oleh developer, devops maupun sysadmin.

Berikut penjelasan dalam proses docker dalam pembuatan nya&#x20;

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Docker client merupakan antarmuka yang di operasikan oleh manusia.

Docker host adalah computer, VM , atau instance dimana container akan berjalan.

Docker Registry adalah penyedia base untuk image yang nanti nya akan di gunakan container.

* Command docker build digunakan untuk membuat image custom dan dapat di masukan source code di dalam nya. Proses nya sebagai berikut:&#x20;

docker build di eksekusi -> service docker pada host menerima perintah -> mengambil bahan image pada docker registry -> inject source code di docker host  -> create image baru&#x20;

* Command docker pull di gunakan untuk mengambil image pada docker registry, tanpa ada menyelipkan source code

docker build di eksekusi -> service docker pada host menerima perintah -> mengambil image pada docker registry.

* Command docker run di gunakan untuk menjalankan container berdasarkan image yang sudah di definisikan, bisa mengambil dari yang sudah ada pada docker host maupun harus mengambil terlebih dahulu pada docker registry.
