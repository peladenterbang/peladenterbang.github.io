---
description: command basic yang sering di gunakan pada docker
---

# Command Basic

1. Menampilkan container&#x20;

```
docker ps -a 
```

2. Menampilkan image yang sudah di download dari docker registry

```
docker images
```

3. Mendownload image nginx, check ketersediaan image pada [https://hub.docker.com/](https://hub.docker.com/)

```
docker pull nginx
```

4. Menjalankan docker container

```
docker run --name some-nginx -d -p 8080:80 nginx
```

* \--name : nama container (whatever)
* \-d : jalankan container di background&#x20;
* \-p : expose nginx port ke port 8080

5. delete docker container&#x20;

```
docker stop <id container>
docker remove <id container>
```

