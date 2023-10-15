# Cara Mengambil Data dari Reddit dan Menyimpannya ke Dalam File .json di Google Colab

Berikut adalah langkah-langkah untuk mengambil data dari Reddit dan menyimpannya ke dalam file .json:

1. ### Menginstall Library "praw"
   Pertama-tama, kita perlu menginstall library praw yang digunakan untuk mengakses API Reddit. Pada Google Colab, kita dapat menggunakan perintah berikut:
   <br>
   ```bash
   !pip install praw
   ```

2. ### Impor Modul yang Diperlukan
   Anda harus mengimpor beberapa modul yang akan digunakan:
   <br>
   ```bash
   import praw
   import json
   from google.colab import files
   ```
3. ### Mengatur Autentikasi dengan API Reddit
   Anda harus mengatur autentikasi untuk mengakses API Reddit:
   ```bash
   Reddit = praw.Reddit(
    client_id="CLIENT_ID",
    client_secret="CLIENT_SECRET",
    user_agent="Tugas 1 by US",
   )
   ```
4. ### Mengambil Data dari Subreddit (Contoh: Technology)
   Selanjutnya, Anda dapat mulai mengambil postingan dari subreddit 'Technology':
   ```bash
   today_posts = Reddit.subreddit('Technology').top(limit=10000)
   ```
5. ### Mengolah Data dan Menyimpannya ke Dalam List
   Ambil data yang diperlukan dari setiap postingan dan simpan ke dalam list:
   ```bash
   post_list = []

   for post in today_posts:
    print(f"Fetching post: {post.title}")  # Diagnostic print for each post
    post_details = {
        "ID": post.id,
        "Title": post.title,
        "Author": str(post.author),
        "URL": post.url,
        "Upvote Ratio": post.upvote_ratio,
        "Score": post.score,
        "Comment Count": post.num_comments,
        "Created": post.created_utc
    }
    post_list.append(post_details)
   ```
6. ### Menyimpan Data ke Dalam File .json
   Gunakan kode berikut untuk menyimpan data yang telah diambil ke dalam file .json:
   ```bash
   with open('reddit_posts.json', 'w') as json_file:
    json.dump(post_list, json_file, indent=4)
   ```
7. ### Mengunduh File .json
   Jika Anda menggunakan Google Colab, Anda dapat mengunduh file .json langsung ke komputer Anda dengan:
   ```bash
   files.download('reddit_posts.json')
   ```
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
