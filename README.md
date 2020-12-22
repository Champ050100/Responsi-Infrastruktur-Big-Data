# Responsi Infrastruktur Big Data
 Login ke VM  Kemudian masukkan username dan password VM untuk memulai membangun infrastruktur apache spark.

Sebelum memasang perangkat lunak baru, ada baiknya untuk menyegarkan basis data paket perangkat lunak lokal Anda untuk memastikan Anda mengakses versi terbaru. Buka terminal dan ketik perintah dibawah ini :

sudo apt-get update

Install Java Untuk melakukan instalasi pada java bisa menggunakan perintah dibawah :
sudo apt-get install default-jdk

Jika sudah dilakukan selanjutnya kita mengecek kembali versi java yang digunakan :

java –version

Create Direktori Membuat Direktori baru untuk minyampan file apache
mkdir –p /opt/responsi

dan kemudian

cd /opt/responsi

Download apche spark package Selanjutnya kita harus mendownload paket-paket dari apache spark dengan menggunakan perintah dibawah. Untuk mendownload bisa mengakses https://spark.apache.org/downloads.html dan pilih spark yang ingin digunakan dan download. Atau bisa menggunakan perintah dibawah ini :
wget https://downloads.apache.org/spark/spark-2.4.7/spark-2.4.7-bin-hadoop2.7.tgz

Ekstrak Selanjutnya melakukan proses ekstrak dari file apche yang telah didownload dengan menggunakan perintah :
tar -xvf spark-2.4.7-bin-hadoop2.7.tgz

Configure the Environment Sebelum memulai server master Spark, ada beberapa variabel yang perlu dikonfigurasi.
vi~/.bashrc

Dan masukkan

export SPARK_HOME=/opt/reesponsi/spark-2.4.7-bin-hadoop2.7 export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin

Start Apcahe Spark Setelah dikonfigurasi, selanjutnya adalah memulai server master Spark. Perintah sebelumnya menambahkan direktori yang diperlukan ke variabel PATH sistem, jadi perintah ini dapat dijalankan dari direktori mana pun:
start-master.sh

Web interface
ss –tunelp | grep 8080

Perintah ini untuk mengetahui proses yang berjalan dan lokasi spark yang dapat di akses melalui web. Selain itu juga untuk mengetahui url spark untuk digunakan menjalankan perintah slave nantinya.

Create new File Membuat sebuah file dapat menggunakan perintah dibawah :
pico input.text

Text yang dimasukan bisa terserah, atau bisa melihat file input yang ada pada repository ini untuk melihat text yang saya gunakan. Setelah itu di save.

Untuk memverifikasi apakah spark-shell dipasang dengan benar. Ketik spark-shell di terminal.
Spark-shell

Seperti ini tampilan dari spark kita bisa memasukan text didalamnya. Karena tadi sudah dibuatkan sebelumnya jadi kita tinggal memanggil file ke dalam sini dengan cara mengetikan perintah dibawah :

val inputfile = sc.textFile(“input.text”)

val counts = inputfile.flatMap(line => line.split(" ")).map(word =>(word, 1)).reduceByKey(+);

counts.cache()

counts.saveAsTextFile("output")

Seluruh hasil akan tersimpan dalam direktori output dan kemudian save

Exit Spar-Shell Untuk keluar dari spark-shella, tekan CTRL C. Kemudian masuk ke dalam direktori output untuk mengecek hasil spark
cd output/

Setelah itu jalankan perintah dibawah ini untuk melihat hasilnya.

Cat part-00000
