# Jarkom-Modul-5-E11-2021
## Anggota Kelompok :
| Nama | NRP |
|------|-----|
|Rizqi Rifaldi|05111940000068|
|Yusuf Anfasya|05111940000077|
|Muhammad Subhan|05111940000204|

Pada soal shift Modul 4 kita disuruh untuk menjawab soal mengenai firewall.

## A . Topologi :

[![Whats-App-Image-2021-12-10-at-21-44-45.jpg](https://i.postimg.cc/qR88Yrjz/Whats-App-Image-2021-12-10-at-21-44-45.jpg)](https://postimg.cc/YGCGG5cH)

Dengan keterangan :

Doriki adalah DNS Server

Jipangu adalah DHCP Server

Maingate dan Jorge adalah Web Server

Jumlah Host pada Blueno adalah 100 host

Jumlah Host pada Cipher adalah 700 host

Jumlah Host pada Elena adalah 300 host

Jumlah Host pada Fukurou adalah 200 host

## B . Subnetting
Luffy ingin meminta kalian untuk membuat topologi tersebut menggunakan teknik CIDR atau VLSM. setelah melakukan subnetting. Disini kelompok kami menggunakan subnetting VLSM :

[![Whats-App-Image-2021-12-10-at-22-14-24.jpg](https://i.postimg.cc/5NSdqFJC/Whats-App-Image-2021-12-10-at-22-14-24.jpg)](https://postimg.cc/hfv5KvfD)

Dengan tabel seperti berikut :

|Subnet|Jumlah IP|Netmask|
|------|----------|-------|
|  A1  | 	  2     |	/30  |
|  A2  |	  2     | /30  |
|  A3  |	  3     |	/29  |
|  A4  |	  3     |	/29  |
|  A5  |	 101    |	/25  |
|  A6  |	 701    |	/22  |
|  A7  |	 201    |	/24  |
|  A8  |	 301    |	/23  |

dan dengan VLSM tree sebagai berikut :

[![Whats-App-Image-2021-12-10-at-21-55-52.jpg](https://i.postimg.cc/zvGFRMFv/Whats-App-Image-2021-12-10-at-21-55-52.jpg)](https://postimg.cc/tZ8xKBfG)

maka didapatkan ip pada masing-masing subnet sebagai berikut :

|Subnet|  Network ID   | Netmask |
|------|---------------|---------|
|  A1  | 192.205.0.0   |  /30    |
|  A2  | 192.205.0.4   |  /30    |
|  A3  | 192.205.0.16  |  /29    |
|  A4  | 192.205.0.24  |  /29    |
|  A5  | 192.205.0.128 |  /25    |
|  A6  | 192.205.4.0   |  /22    |
|  A7  | 192.205.1.0   |  /24    |
|  A8  | 192.205.2.0   |  /23    |

## C . Routing
diharuskan melakukan Routing agar setiap perangkat pada jaringan tersebut dapat terhubung.

## D . Pemberian IP
Tugas berikutnya adalah memberikan ip pada subnet Blueno, Cipher, Fukurou, dan Elena secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

## Soal 1
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Foosha menggunakan iptables, tetapi Luffy tidak ingin menggunakan MASQUERADE.

## Soal 2
Kalian diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.

## Soal 3
Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

## Soal 4
Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut :
Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.

## Soal 5
Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut :
Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.
Selain itu di reject

## Soal 6
Karena kita memiliki 2 Web Server, Luffy ingin Guanhao disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate
