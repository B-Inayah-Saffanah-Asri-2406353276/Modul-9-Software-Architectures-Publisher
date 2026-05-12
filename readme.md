# Modul 9 Software Architecture - Publisher

### Questions
1. **How much data your publisher program will send to the message broker in one run?**

Publisher mengirimkan 5 event ke message broker. Setiap event berisi `UserCreatedEventMessage` yang memiliki atribut `user_id` dan `user_name`.

2. **The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?***

Hal tersebut berarti publisher dan subscriber terhubung ke server AMQP yang sama. Karena menggunakan koneksi yang sama, keduanya dapat saling komunikasi melalui message broker RabbitMQ yang sama.

### Running RabbitMQ
![alt text](<Screenshot 2026-05-11 213853.png>)

### Processing event
![alt text](image.png)
Program berhasil berjalan dan menerima pesan dari publisher melalui RabbitMQ menggunakan protokol AMQP. Publisher mengirimkan event `UserCreatedEventMessage` berisi data user `user_id` dan `user_name` ke sebuah queue bernama `user_created`, kemudian subscriber yang sedang listen pada queue yang sama menerima dan mencetak pesan-pesan tersebut ke terminal, membuktikan bahwa komunikasi asynchronous antara dua service menggunakan pola publish-subscribe berhasil berjalan dengan baik.

### Monitoring Chart
![alt text](image-1.png)
Pada grafik **Message rates** di RabbitMQ, terlihat adanya spike pada kurva yang terjadi dua kali sekitar pukul 14:37:10 dan 14:37:30. Spike tersebut muncul setiap kali publisher dijalankan, karena publisher mengirimkan sejumlah pesan sekaligus ke queue `user_created` dalam waktu singkat, sehingga message rate melonjak sesaat lalu kembali ke 0 setelah semua pesan selesai dikirim dan dikonsumsi oleh subscriber. Hal ini membuktikan bahwa RabbitMQ berhasil menerima, menyalurkan, dan mengosongkan pesan secara real-time setiap kali publisher dieksekusi.
