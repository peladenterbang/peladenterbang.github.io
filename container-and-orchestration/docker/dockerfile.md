# Dockerfile

docker file adalah file yang di gunakan untuk blueprint docker image, di dalam docker file akan di deskripsikan bagaiman container berjalan.

Example:&#x20;

menjalankan node js menggunakan docker file&#x20;

1. siapkan source code

```
git clone https://github.com/docker/getting-started-app.git
cd getting-started-app
nano Dockerfile
```

2. Masukkan syntax berikut&#x20;

<pre><code><strong>FROM node:18-alpine
</strong>WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
</code></pre>

3. Lalu buat image dengan command

```
docker build -t getting-started .
```

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

4. Check image yang telah di buat bernama `getting-started`

```
docker images | grep getting-started
```

5. Coba jalankan container&#x20;

```
docker run -dp 3000:3000 getting-started
```

6. check container&#x20;

```
docker ps -a | grep getting-started
```

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

7. Test dengan akses \<ip-address-docker-host:3000>

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
