1a. what is amqp?
AMQP adalah Advanced Message Queuing Protocol yang merupakan sebuah protokol middleware yang bisa digunakan
untuk mengirimkan pesan, queuing, routing, serta fungsi sekuritas. AMQP juga merupakan deskripsi format data berupa byte
untuk penyaluran pesan terenkripsi antara klien/server dan manajemen perangkat IoT(Internet of Things).

1b. what it means? guest:guest@localhost:5672 , what is the first quest, and what is
the second guest, and what is localhost:5672 is for? guest:guest@localhost:5672 merupakan string yang mendeskripsikan koneksi
menuju server RabbitMQ di port 5672. Guest pertama digunakan sebagai username default untuk autentikasi. Guest kedua digunakan
sebagai default password dari username guest. localhost:5672 adalah alamat lokal yang menuju port 5672, RabbitMQ.
docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3.13-management

2a. How many data your publisher program will send to the message broker in one
run?
Lima messages, masing-masing berisi npm saya, 2206025363, lalu nama Amir, Budi, Cica, Dira, dan Emir.

2b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber
program, what does it mean?
Jika url publisher dan subscriber sama, maka itu berarti mereka menggunakan koneksi yang sama. Mereka menggunakan server AMQP
RabbitMQ yang sama agar bisa terhubung dan berkomunikasi.

<img src="images/Screenshot (366).png">
<img src="images/Screenshot (367).png">
<img src="images/Screenshot (368).png">