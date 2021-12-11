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

Dengan melakukan Rooting pada node `Foosha` seperti berikut

### FOOSHA

```
route add -net 192.205.0.16 netmask 255.255.255.248 gw 192.205.0.2

route add -net 192.205.4.0 netmask 255.255.252.0 gw 192.205.0.2

route add -net 192.205.0.128 netmask 255.255.255.128 gw 192.205.0.2

route add -net 192.205.1.0 netmask 255.255.255.0 gw 192.205.0.6

route add -net 192.205.2.0 netmask 255.255.254.0 gw 192.205.0.6

route add -net 192.205.0.24 netmask 255.255.255.248 gw 192.205.0.6
```

## D . Pemberian IP
Tugas berikutnya adalah memberikan ip pada subnet Blueno, Cipher, Fukurou, dan Elena secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

### Setting GNS3

#### FOOSHA

Konfigurasi sebagai DHCP Relay dan Router

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.205.0.1
	netmask 255.255.255.252
	
auto eth2
iface eth2 inet static
	address 192.205.0.5
	netmask 255.255.255.252

```

#### Guanhao

Konfigurasi sebagai DHCP Relay dan Router

```
auto eth0
iface eth0 inet static
	address 192.205.0.6
	netmask 255.255.255.252
	gateway 192.205.0.5

auto eth1
iface eth1 inet static
	address 192.205.2.1
	netmask 255.255.254.0

auto eth2
iface eth2 inet static
	address 192.205.1.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.205.0.25
	netmask 255.255.255.248

```

#### Water7

Konfigurasi sebagai DHCP Relay dan Router

```
auto eth0
iface eth0 inet static
	address 192.205.0.2
	netmask 255.255.255.252
	gateway 192.205.0.1

auto eth1
iface eth1 inet static
	address 192.205.0.129
	netmask 255.255.255.128

auto eth2
iface eth2 inet static
	address 192.205.0.17
	netmask 255.255.255.248

auto eth3
iface eth3 inet static
	address 192.205.4.1
	netmask 255.255.252.0

```

#### Doriki

Konfigurasi sebagai DNS Server

```
auto eth0
iface eth0 inet static
	address 192.205.0.18
	netmask 255.255.255.248
gateway 192.205.0.17

```

#### Jipangu

Konfigurasi sebagai DNS Server

```
auto eth0
iface eth0 inet static
	address 192.205.0.19
	netmask 255.255.255.252
gateway 192.205.0.17

```

#### JORGE

Konfigurasi sebagai WEB server

```
auto eth0
iface eth0 inet static
	address 192.205.0.27
	netmask 255.255.255.248
	gateway 192.205.0.25
```

#### Maingate

Konfigurasi sebagai WEB server

```
auto eth0
iface eth0 inet static
	address 192.205.0.26
	netmask 255.255.255.248
	gateway 192.205.0.25

```

#### BLUENO(100Host)

Client
```
auto eth0
iface eth0 inet dhcp
	address 192.205.0.130
	netmask 255.255.255.128
gateway 192.205.0.129

```
#### CIPHER(700Host)

Client
```
auto eth0
iface eth0 inet dhcp
	address 192.205.4.2
	netmask 255.255.252.0
gateway 192.205.4.1

```

#### ELENA(300Host)

Client
```
auto eth0
iface eth0 inet dhcp
	address 192.205.2.2
	netmask 255.255.254.0
	gateway 192.205.2.1

```

#### FUKUROU(200Host)

Client
```
auto eth0
iface eth0 inet dhcp
	address 192.205.1.2
	netmask 255.255.255.0
	gateway 192.205.1.1
```




### Setting DHCP Relay 

dengan meletakkan command tersebut di script masing masing 

#### FOOSHA

```
apt-get update
apt-get install isc-dhcp-relay -y

echo '
# Defaults for isc-dhcp-relay initscript
# sourced by /etc/init.d/isc-dhcp-relay
# installed at /etc/default/isc-dhcp-relay by the maintainer scripts

#
# This is a POSIX shell fragment
#

# What servers should the DHCP relay forward requests to?
SERVERS="192.205.0.19"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth0 eth1 eth2 "

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
' > /etc/default/isc-dhcp-relay

/etc/init.d/isc-dhcp-relay restart

```

#### Water7

```
apt-get update 
apt-get install isc-dhcp-relay -y

echo '
# Defaults for isc-dhcp-relay initscript
# sourced by /etc/init.d/isc-dhcp-relay
# installed at /etc/default/isc-dhcp-relay by the maintainer scripts

#
# This is a POSIX shell fragment
#

# What servers should the DHCP relay forward requests to?
SERVERS="192.205.0.19"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth0 eth1 eth2 eth3"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
' > /etc/default/isc-dhcp-relay

/etc/init.d/isc-dhcp-relay restart

```
### Setting DHCP SERVER

#### Guanhao

```
apt-get update
apt-get install isc-dhcp-server -y

echo '

INTERFACES="eth0" ' >/etc/default/isc-dhcp-server

option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

log-facility local7;

subnet 192.205.0.128 netmask 255.255.255.128 {
        range 192.205.0.131 192.205.0.232;
        option routers 192.205.0.129;
        option broadcast-address 192.205.0.255;
        option domain-name-servers 192.168.122.1;
        default-lease-time 720;
        max-lease-time 720;
        }

subnet 192.205.1.0 netmask 255.255.255.0 {
        range 192.205.1.3 192.205.1.104;
        option routers 192.205.1.1;
        option broadcast-address 192.205.1.255;
        option domain-name-servers 192.168.122.1;
        default-lease-time 720;
        max-lease-time 720;
        }

        subnet 192.205.4.0 netmask 255.255.252.0 {
        range 192.205.4.3 192.205.6.195;
        option routers 192.205.4.1;
        option broadcast-address 192.205.4.255;
        option domain-name-servers 192.168.122.1;
        default-lease-time 720;
        max-lease-time 720;
        }

subnet 192.205.0.16 netmask 255.255.255.248 {
        option routers 192.205.0.17;
        option broadcast-address 192.205.0.255;
        }
 subnet 192.205.0.24 netmask 255.255.255.248 {
        option routers 192.205.0.25;
        option broadcast-address 192.205.0.255;
        }
subnet 192.205.0.4 netmask 255.255.255.252 {
        option routers 192.205.0.5;
        option broadcast-address 192.205.0.255;
        }

        subnet 192.205.0.0 netmask 255.255.255.252 {
        option routers 192.205.0.1;
        option broadcast-address 192.205.0.255;
        } ' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart

```


## Soal 1
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Foosha menggunakan iptables, tetapi Luffy tidak ingin menggunakan MASQUERADE.

Untuk Dapat melakukan konfigurasi Foosha tanpa MASQUERADE maka kami menggunakan command `SNAT`

```
iptables -F
iptables -t nat -F
iptables -t nat -A POSTROUTING -s 192.205.0.0/16 -o eth0 -j SNAT --to 192.168.1$.168.122.223
```
Dengan cara tersebut maka dapat berjalan tanpa MASQUERADE.

## Soal 2
Kalian diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.

Sehingga solusinya dengan melakukan drop atau recject connection apabila melalui `port 80` yang merupakan port `HTTP`

### FOOSHA
```
iptables -F
iptables -t nat -F
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.205.0.0/16
iptables -A INPUT -p tcp --dport 80 -s 192.205.0.17 -j DROP

```

### Water7

```
iptables -A FORWARD -d 192.205.0.16/29 -p tcp --dport 80 -j REJECT

```





## Soal 3
Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

Untuk melakukan hal tersebut, pada DNS Server Doriki kita akan menggunakan command :

```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```
command tersebut akan menjadikan pembatasan penerimaan koneksi ICMP menjadi maksimal 3 dan jika lebih akan di drop.

## Soal 4
Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut :
Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.

Untuk melakukan hal tersebut, pada DNS server Doriki kita akan menambahkan command berikut :

```
iptables -A INPUT -s 192.205.0.128/25 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.205.0.128/25 -j REJECT
iptables -A INPUT -s 192.205.4.0/22 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.205.4.0/22 -j REJECT
```
Ini akan menyebabkan pembatasan akses ke Doriki dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 sampai 15.00 pada hari Senin sampai Kamis, dan jika diluar jam dan hari tersebut maka akan di reject.

Untuk mengecek apakah konfigurasi yang dilakukan sudah benar, kita bisa melakukan hal berikut :

Pada Blueno

[![Whats-App-Image-2021-12-10-at-23-34-38.jpg](https://i.postimg.cc/N02WLQ6N/Whats-App-Image-2021-12-10-at-23-34-38.jpg)](https://postimg.cc/SXqZvFt8)


Pada Cipher

[![Whats-App-Image-2021-12-10-at-23-36-03.jpg](https://i.postimg.cc/q7K54jrS/Whats-App-Image-2021-12-10-at-23-36-03.jpg)](https://postimg.cc/HJp2t0V9)

Pada kedua gambar tersebut, jika pada Blueno dan Cipher di set pada tanggal 6 Desember 2021 (Senin) pada jam 10.00 (Masuk kriteria akses), maka masih bisa melakukan ping ke Server Doriki, dan jika pada Blueno dan Cipher di set pada tanggal yang sama tetapi pada jam 18.00 (Diluar jam syarat) maka akses akan di reject.


## Soal 5
Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut :
Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.
Selain itu di reject

Untuk melakukan hal tersebut, pada DNS Server Doriki akan dijalankan command berikut :
```
iptables -A INPUT -s 192.205.2.0/23 -m time --timestart 15:01 --timestop 23:59 -j ACCEPT
iptables -A INPUT -s 192.205.2.0/23 -m time --timestart 00:00 --timestop 06:59 -j ACCEPT
iptables -A INPUT -s 192.205.1.0/24 -m time --timestart 15:01 --timestop 23:59 -j ACCEPT
iptables -A INPUT -s 192.205.1.0/24 -m time --timestart 00:00 --timestop 06:59 -j ACCEPT
iptables -A INPUT -s 192.205.2.0/23 -j REJECT
iptables -A INPUT -s 192.205.1.0/24 -j REJECT
```

Hal ini menyebabkan akses dari subnet Elena dan Fukurou ke DNS Server Doriki hanya bisa dilakukan setiap hari mulai pukul 15.01 sampai dengan pukul 06.59 dan selain jam tersebut akan di reject.

Untuk melakukan pengetesan atasa konfigurasi yang telah dilakukan, bisa melakukan hal berikut :

Pada Elena

[![Whats-App-Image-2021-12-10-at-23-41-28.jpg](https://i.postimg.cc/TwtdJRsr/Whats-App-Image-2021-12-10-at-23-41-28.jpg)](https://postimg.cc/34DQKHYR)

Pada Fukurou

[![Whats-App-Image-2021-12-10-at-23-41-48.jpg](https://i.postimg.cc/7YFxVtKQ/Whats-App-Image-2021-12-10-at-23-41-48.jpg)](https://postimg.cc/KR5ScfSn)

Pada kedua gambar tersebut, jika pada Elena dan Fukurou di set pada tanggal 6 Desember 2021 (Senin) pada jam 12.00 (Diluar kriteria akses), maka akan direjet ketika melakukan ping ke Server Doriki, dan jika pada Elena dan Fukurou di set pada tanggal yang sama tetapi pada jam 19.00 (Di dalam jam akses) maka bisa melakukan ping ke server Doriki.

## Soal 6
Karena kita memiliki 2 Web Server, Luffy ingin Guanhao disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate.

Pada Gunhao, dijalankan command seperti berikut :

```
iptables -A -PREROUTING -t -nat -p tcp -d 192.205.0.18 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.205.0.26
iptables -A -PREROUTING -t nat -p tcp -d 192.205.0.18 -j DNAT --to-destination 192.205.0.26
```
Hal ini dilakukan dengan metode round robin, sehingga request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate.

[![Whats-App-Image-2021-12-10-at-23-46-40.jpg](https://i.postimg.cc/gjcK1K4C/Whats-App-Image-2021-12-10-at-23-46-40.jpg)](https://postimg.cc/62SRvnkc)

Pada gambar diatas, dapat dilihat bahwa request dari Fukurou yang mengakses server Doriki akan didistribusikan ke Jorge dan Maingate secara bergantian.
