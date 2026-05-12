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