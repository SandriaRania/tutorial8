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

3. Edit your publisher readme.md again, capture your browser, and explain how the spike got to do
   with running the publisher. Put it on readme.md.
Tanjakan pada grafik adalah tanjakan pada pengukuran Customer ack, yang menurut definisi RabbitMQ adalah kecepatan di mana
pesan diterima oleh consumers. Dalam kasus ini, grafik menanjak ketika publisher cargo run karena mengirim kima pesan yang telah 
disebutkan sebelumnya, tanjakan itu terjadi ketika subscriber(consumer) menerima pesan dan akan menanjak lagi jika publisher
di cargo run lagi.

<img src="images/Screenshot (369).png">

4. In your subscriber directory, edit your Readme.md, add the screen capture of yours, and answer
   why the total number of queue is as such (in my machine is 20, what about yours?)
Queue saya juga berangka 20, hal ini disebabkan karena thread::sleep(ten_millis) membuat setiap pemanggilan thread terjadi
delay selama 1000 milisekon (sesuai definisi di fungsinya) atau setara 1 sekon. Saya memanggil cargo run 5 kali, maka kemungkinan
terdapat total 25 pesan yang harus diqueue, namun kita melihat bahwa puncak 20 queue berada diantara 22:27:10 dan 22:27:20, sekitar
kedua angka tersebut, maka ada kemungkinan delay 5 sekon di mana kelima perintah dipanggil terjadi di jangka waktu tersebut, serta
5 pesan juga sudah dikirim dalam jangka waktu itu. Maka, karena pemanggilan sudah selesai dan saat 22:27:20 sudah tidak ada delay, server
pun bisa mengirim pesan satu-satu sehingga setelah 22:27:20, grafik menurun.

<img src="images/Screenshot (370).png">

5. Edit your subscriber readme.md, put your capture in the readme.md, and also add some
explanation/reflection of why it is like that. Take a look at the code of publisher and subscriber,
do you see something to improve?
Saya melihat bahwa subscriber pertama menerima Amir(1) dan Dira(4), subscriber kedua Cica(3), dan subscriber ketiga menerima
Budi (2) dan Emir(5). Dari observasi ini saya mengetahui bahwa ternyata kecepatan meningkat karena pesan terbagi menuju tiga 
consumer sehingga ratenya juga meningkat. Hal ini terlihat di grafik. Mengenai kode yang dicontohkan sebenarnya konsepnya 
sudah cukup simpel, namun mungkin bisa ditambah dan dilengkapi dengan kasus jika error dan prevensinya, seperti jika gagal 
terkoneksi karena masalah di url yang tidak sama atau semacamnya. Bisa juga dilengkapi fungsi agar bisa menambah lebih dari 
lima messages per thread, mungkin dengan loop atau semacamnya.

<img src="images/Screenshot (371).png">
<img src="images/Screenshot (372).png">
<img src="images/Screenshot (374).png">