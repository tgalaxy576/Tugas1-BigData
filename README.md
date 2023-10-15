# Cara Mengimport File Bertipe .json ke MongoDB
Hi! kali ini kami akan mejelaskan cara untuk melakukan import ke MongoDB dengan file yang bertipe .json

1. ### Install Docker
   Langkah pertama adalah menginstall docker karena kita akan menginstall MongoDB pada docker, untuk melakukan installasi docker dapat dilihat pada link berikut :
   <br>
   https://docs.docker.com/engine/install/

2. ### Pull Image MongoDB
   Lakukan pull image MongoDB di CMD untuk ditambahkan ke Docker
    ```bash
    docker pull mongo
    ```
3. ### Melakukan Run Image MongoDB
   Menjalankan Image Mongodb pada Docker, mengatur Port yang dipakai serta menambahkan nama pada Container yang akan dibuat
   ```bash
   docker run -d -p 27017:27017 --name your-container-name mongo
   ```

4. ### Menyalin File .json Ke Container
   Menyalin file .json yang akan ke dalam container
   ```bash
   docker cp your-file-name.json your-container-name:/your-file-name.json
   ```

5. ### Masuk Ke Dalam MongoDB
   Melakukan akses ke MongoDB yang telah dijalankan
   ```bash
   docker exec -it your-container-name mongo
   ```

6. ### Membuat Database
   Membuat database untuk menampung file .json yang ingin kita import, kita dapat menggunakan
   ```docker
   use your-database
   ```
   jika database dengan nama ```your-database``` belum ada, maka docker akan langsung membuatkannya

7. ### Mengimport File .json Ke Dalam MongoDB
   Melalukan import ke dalam MongoDB dengan perintah seperti berikut:
   ```docker
   db.your_collection_name.insertMany(
    JSON.parse(cat("/your-file-name.json"))
    );
   ```

8. ### Melihat Hasil Yang Telah diimport
   Untuk melihat hasil yang telah diimport sebelumnya, dapat menggunakan perintah seperti berikut:
   ```docker
   db.your_collection_name.find()
   ```
