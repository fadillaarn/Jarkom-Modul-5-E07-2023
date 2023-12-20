# Jarkom-Modul-5-E07-2023
Laporan Resmi Praktikum Modul 5 Jaringan Komputer 2023

### Kelompok E07
| Nama | NRP |
|:----:|:---:|
| [Akmal Sulthon Fathulloh](https://github.com/afsulthon) | 5025211047 |
| [Fadilla Rizky Nurhidayah](https://github.com/fadillaarn) | 5025211110 |

## Daftar Isi
- [Prasoal](#prasoal)
  - [(A) Topologi](#a-topologi)
  - [(B) VLSM dan Subnetting](#b-vlsm-dan-subnetting)
  - [(C) Routing](#c-routing)
  - [(D) DHCP](#d-dhcp)
- [Nomor 1](#nomor-1)
- [Nomor 2](#nomor-2)
- [Nomor 3](#nomor-3)
- [Nomor 4](#nomor-4)
- [Nomor 5](#nomor-5)
- [Nomor 6](#nomor-6)
- [Nomor 7](#nomor-7)
- [Nomor 8](#nomor-8)
- [Nomor 9](#nomor-9)
- [Nomor 10](#nomor-10)
- [Kendala](#kendala)

## Prasoal
### (A) Topologi
> Tugas pertama, buatlah peta wilayah sesuai berikut ini!

Berikut adalah peta wialyah (topologi) jaringan yang telah dibuat.  
![Screenshot (114)](https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/107914177/8587de49-f3df-472b-ae74-b64d3c1c5983)

### (B) VLSM dan Subnetting
> Untuk menghitung rute-rute yang diperlukan, gunakan perhitungan dengan metode VLSM. Buat juga pohonnya, dan lingkari subnet yang dilewati.

Berdasarkan perhitungan VLSM yang sudah dilakukan berikut adalah konfigurasi IP yang digunakan pada masing-masing node.
- Aura
```bash
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.40.0.1
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.40.0.5
	netmask 255.255.255.252
```
- Heiter (DHCP Relay)
```bash
auto eth0
iface eth0 inet static
	address 10.40.0.2
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.40.8.1
	netmask 255.255.248.0

auto eth2
iface eth2 inet static
	address 10.40.4.1
	netmask 255.255.252.0
```
- Frieren
```bash
auto eth0
iface eth0 inet static
	address 10.40.0.6
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.40.0.13
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.40.0.9
	netmask 255.255.255.252
```
- Himmel (DHCP Relay)
```bash
auto eth0
iface eth0 inet static
	address 10.40.0.14
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.40.2.1
	netmask 255.255.254.0

auto eth2
iface eth2 inet static
	address 10.40.0.129
	netmask 255.255.255.128
```
- Fern
```bash
auto eth0
iface eth0 inet static
	address 10.40.0.130
	netmask 255.255.255.128

auto eth1
iface eth1 inet static
	address 10.40.0.17
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.40.0.21
	netmask 255.255.255.252
```
- Revolte (DHCP Server)
```bash
auto eth0
iface eth0 inet static
	address 10.40.0.22
	netmask 255.255.255.252
	gateway 10.40.0.21
```
- Richter (DNS Server)
```bash
auto eth0
iface eth0 inet static
	address 10.40.0.18
	netmask 255.255.255.252
	gateway 10.40.0.17
```
- Sein (Web Server)
```bash
auto eth0
iface eth0 inet static
	address 10.40.4.2
	netmask 255.255.252.0 
	gateway 10.40.4.1
```
- Stark (Web Server)
```bash
auto eth0
iface eth0 inet static
	address 10.40.0.10
	netmask 255.255.255.252
	gateway 10.40.0.9
```
- TurkRegion, GrobeForest, LaubHills, SchwerMountain (Clients)
```bash
auto eth0
iface eth0 inet dhcp
```

### (C) Routing
> Kemudian buatlah rute sesuai dengan pembagian IP yang kalian lakukan.

Berikut adalah konfigurasi routing berdasarkan pembagian IP yang telah dilakukan.
- Aura
```bash
# Gateway Heiter
route add -net 10.40.8.0 netmask 255.255.248.0 gw 10.40.0.2 # A2
route add -net 10.40.4.0 netmask 255.255.252.0 gw 10.40.0.2 # A3
# Gateway Frieren
route add -net 10.40.0.8 netmask 255.255.255.252 gw 10.40.0.6 # A5
route add -net 10.40.0.12 netmask 255.255.255.252 gw 10.40.0.6 # A6
route add -net 10.40.2.0 netmask 255.255.254.0 gw 10.40.0.6 # A7
route add -net 10.40.0.128 netmask 255.255.255.128 gw 10.40.0.6 # A8
route add -net 10.40.0.16 netmask 255.255.255.252 gw 10.40.0.6 # A9
route add -net 10.40.0.20 netmask 255.255.255.252 gw 10.40.0.6 # A10
```
- Heiter
```bash
# Bind anywhere
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.40.0.1
```
- Frieren
```bash
# Bind anywhere
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.40.0.5
# Gateway Himmel
route add -net 10.40.2.0 netmask 255.255.254.0 gw 10.40.0.14 # A7
route add -net 10.40.0.128 netmask 255.255.255.128 gw 10.40.0.14 # A8
route add -net 10.40.0.16 netmask 255.255.255.252 gw 10.40.0.14 # A9
route add -net 10.40.0.20 netmask 255.255.255.252 gw 10.40.0.14 # A10
```
- Himmel
```bash
# Bind anywhere
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.40.0.13
# Gateway Fern
route add -net 10.40.0.16 netmask 255.255.255.252 gw 10.40.0.130 # A9
route add -net 10.40.0.20 netmask 255.255.255.252 gw 10.40.0.130 # A10
```
- Fern
```bash
# Bind anywhere
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.40.0.129
```

### (D) DHCP
> Tugas berikutnya adalah memberikan IP pada subnet SchwerMountain, LaubHills, TurkRegion, dan GrobeForest menggunakan bantuan DHCP.

Untuk memberikan IP pada subnet SchwerMountain, LaubHills, TurkRegion, dan GrobeForest menggunakan bantuan DHCP, maka dilakukan konfigurasi sebagai berikut pada masing-masing node.
```bash
auto eth0
iface eth0 inet dhcp
```
Setelah itu, lakukan konfigurasi pada DHCP Server (Revolte) dengan menjalankan script berikut. Pastikan sudah terinstall `isc-dhcp-server` pada node Revolte.
```bash
echo 'INTERFACES="eth0"' > /etc/default/isc-dhcp-server

echo '
# A10
subnet 10.40.0.20 netmask 255.255.255.252 {
}

# A9
subnet 10.40.0.16 netmask 255.255.255.252 {
}

# SchwerMountain (A8)
subnet 10.40.0.128 netmask 255.255.255.128 {
    range 10.40.0.130 10.40.0.193;
    option routers 10.40.0.129;
    option broadcast-address 10.40.0.255;
    default-lease-time 600;
    max-lease-time 7200;
}

# LaubHills (A7)
subnet 10.40.2.0 netmask 255.255.254.0 {
    range 10.40.2.2 10.40.3.1;
    option routers 10.40.2.1;
    option broadcast-address 10.40.3.255;
    default-lease-time 600;
    max-lease-time 7200;
}

# A6
subnet 10.40.0.12 netmask 255.255.255.252 {
}

# A5
subnet 10.40.0.8 netmask 255.255.255.252 {
}

# A4
subnet 10.40.0.4 netmask 255.255.255.252 {
}

# A1
subnet 10.40.0.0 netmask 255.255.255.252 {
}

# TurkRegion (A2)
subnet 10.40.8.0 netmask 255.255.248.0 {
    range 10.40.8.2 10.40.11.255;
    option routers 10.40.8.1;
    option broadcast-address 10.40.15.255;
    default-lease-time 600;
    max-lease-time 7200;
}

# GrobeForest (A3)
subnet 10.40.4.0 netmask 255.255.252.0 {
    range 10.40.4.2 10.40.6.1;
    option routers 10.40.4.1;
    option broadcast-address 10.40.7.255;
    default-lease-time 600;
    max-lease-time 7200;
}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```
Selanjutnya, lakukan konfigurasi pada DHCP Relay (Heiter dan Himmel) dengan menjalankan script berikut. Pastikan sudah terinstall `isc-dhcp-relay` pada node Heiter dan Himmel.
```bash
echo '
SERVERS="10.40.0.22"  
INTERFACES="eth0 eth1 eth2"
OPTIONS=
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' > /etc/sysctl.conf

service isc-dhcp-relay restart
```
Lakukan restart pada node client untuk mendapatkan IP dari DHCP Server.

## Nomor 1
> Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

Agar bisa mengakses internet keluar tanpa menggunakan MASQUERADE, maka jalankan perintah berikut pada node Aura.
```bash
ETH0_IP=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP
```
Script di atas akan mengambil informasi alamat IPv4 dari antarmuka jaringan eth0 Aura dan mengisinya dalam variabel `ETH0_IP`. Selanjutnya, akan dilakukan konfigurasi iptables untuk melakukan SNAT pada antarmuka jaringan eth0 dengan alamat IPv4 yang telah didapatkan sebelumnya.

## Nomor 2
> Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

Untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP, jalankan perintah berikut pada salah satu node client (misalnya, TurkRegion).
```bash
# Bersihkan semua aturan atau filter
iptables -F
# Drop semua koneksi TCP kecuali port 8080
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -p tcp -j DROP
# Drop semua koneksi UDP
iptables -A INPUT -p udp -j DROP
```
Untuk melakukan pengetesan, install `netcat` pada salah satu node client yang telah dilakukan konfigurasi iptables sebelumnya (dalam hal ini, TurkRegion), kemudian jalankan perintah berikut.
```bash
nc -l -p 8080
```
Perintah di atas akan membuat node client yang bersangkutan menjadi server yang mendengarkan koneksi pada port 8080. Selanjutnya, lakukan pengetesan dengan menjalankan perintah berikut pada node client lain (misalnya, GrobeForest).
```bash
nmap -p 8080 (IP TurkRegion)
```
Perintah di atas akan melakukan scanning port pada node client yang bersangkutan dengan port 8080. Jika berhasil, maka akan muncul output sebagai berikut.  
![image](https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/107914177/919167ae-d13d-4afd-bef0-ee4aeaca31cf)
Lakukan juga scanning port pada port selain 8080 (misalnya, 80) dengan menjalankan perintah berikut.
```bash
nmap -p 80 (IP TurkRegion)
```
Jika berhasil, maka akan muncul output sebagai berikut.  
![image](https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/107914177/566ff1fb-f78e-4fa0-bb73-108a5a998765)

## Nomor 3
> Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

Untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, maka jalankan perintah berikut pada node Richter dan Revolte.
```bash
# Membatasi jumlah koneksi ICMP yang masuk supaya tidak lebih dari 3
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```
Pengetesan dilakukan dengan cara melakukan ping pada node Richter atau Revolte dengan lebih dari 3 node client yang berbeda secara bersamaan. Jika ping tidak berhasil pada node client ke-4, maka konfigurasi telah berhasil.  
![image](https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/107914177/3a8f7f46-8ffb-4d90-bbe7-a9b0dc39ac1f)

## Nomor 4
> Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

Supaya koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest, maka jalankan perintah berikut pada node Stark dan juga Sein.
```bash
# Izinkan koneksi SSH hanya dari GrobeForest
iptables -A INPUT -p tcp --dport 22 ! -s 10.40.10.4 -j REJECT
```
Pengetesan dilakukan dengan cara melakukan koneksi SSH pada node Stark atau Sein. Buka terlebih dahulu koneksi SSH pada node Stark atau Sein dengan menjalankan perintah berikut.
```bash
service ssh start
```
Selanjutnya, lakukan koneksi SSH pada node Stark atau Sein dengan menggunakan GrobeForest (misalnya, TurkRegion). Jika koneksi SSH berhasil, maka konfigurasi telah berhasil.  
![image](https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/107914177/e07bdf03-add7-4ea5-b3d4-5c1a93772df1)

Lakukan juga koneksi SSH pada node Stark atau Sein dengan menggunakan node selain GrobeForest (misalnya, TurkRegion). Jika koneksi SSH tidak berhasil, maka konfigurasi telah berhasil.  
![image](https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/107914177/cd783bca-795b-4d9e-b193-2a8004fd9053)

## Nomor 5
> Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

Untuk membatasi akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00, maka jalankan perintah berikut pada node Stark dan juga Sein.
```bash
# Izinkan akses ke Web Server pada jam kerja (Senin-Jumat pukul 08.00-16.00)
iptables -A INPUT -p tcp --dport 22 -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
# Drop akses selain dari ketentuan
iptables -A INPUT -p tcp --dport 22 -j DROP
```
Pengetesan dilakukan dengan cara melakukan koneksi SSH, mirip dengan nomor sebelumnya. Hanya saja untuk kali ini pengetesan dilakukan pada jam kerja (Senin-Jumat pukul 08.00-16.00). Atur terlebih dahulu jam pada node tester (misalnya, TurkRegion) agar sesuai dengan jam kerja.
```bash
date -s "13 dec 2023 10:00" # jam kerja
```
Jika koneksi SSH berhasil, maka konfigurasi telah berhasil.  
![image](https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/107914177/365037a6-776d-4566-862c-658085b84470)

Lakukan juga koneksi SSH pada jam selain jam kerja. 
```bash
date -s "16 dec 2023 10:00" # bukan jam kerja
```
Jika koneksi SSH tidak berhasil, maka konfigurasi telah berhasil.  
![image](https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/107914177/892a29bd-03e6-40a2-a8fc-a52c8c21a016)

## Nomor 6
> Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

Pada WebServer gunakan syntac berikut:
```bash
iptables -A INPUT -p tcp --dport 22 -s 10.40.4.0/22 -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j DROP

iptables -A INPUT -p tcp --dport 22 -s 10.40.4.0/22 -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j DROP
```

Testing dengan ubah datenya menggunakan node client lalu `nmap` ke webserver, sehingga hasil testing akan seperti berikut:
<img width="817" alt="Screenshot 2023-12-15 at 14 19 59" src="https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/91003946/3835fc0e-74cd-4cc1-bbef-278b012374d0">

<img width="818" alt="Screenshot 2023-12-15 at 14 19 47" src="https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/91003946/80e9580f-f33c-4ee0-b336-2f3c26040ebe">

## Nomor 7
> Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

Pada Heiter dan Frieren gunakan syntax berikut: 
```bash
iptables -A PREROUTING -t nat -p tcp --dport 80 -d 10.40.4.2 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.40.4.2

iptables -A PREROUTING -t nat -p tcp --dport 80 -d 10.40.4.2 -j DNAT --to-destination 192.177.0.18

iptables -A PREROUTING -t nat -p tcp --dport 443 -d 10.40.0.18 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.40.0.18

iptables -A PREROUTING -t nat -p tcp --dport 443 -d 10.40.0.18 -j DNAT --to-destination 10.40.4.2
```

lalu testing dengan membuka koneksi webserver sein dan stark dengan syntax berikut untuk port 80:
```bash
while true; do nc -l -p 80 -c 'echo "ini sein"'; done
```
dan
```bash
while true; do nc -l -p 443 -c 'echo "ini stark"'; done
```

sedangkan port 443 gunakan syntax:
```bash
while true; do nc -l -p 443 -c 'echo "ini sein"'; done
```
dan 
```bash
while true; do nc -l -p 443 -c 'echo "ini stark"'; done
```

Sehingga hasil testingnya akan seperti berikut:
<img width="1680" alt="Screenshot 2023-12-15 at 23 35 37" src="https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/91003946/bad32970-6c14-4659-abc1-cfa6eb2a705e">

## Nomor 8
> Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

Pada webserver gunakan syntax berikut:
```bash
Revolte_Subnet="10.40.0.0/30"

Pemilu_Start=$(date -d "2023-10-19T00:00" +"%Y-%m-%dT%H:%M")

Pemilu_End=$(date -d "2024-02-15T00:00" +"%Y-%m-%dT%H:%M")

iptables -A INPUT -p tcp -s $Revolte_Subnet --dport 80 -m time --datestart "$Pemilu_Start" --datestop "$Pemilu_End" -j DROP
```

Testing dengan mengubah date sesuai yang diminta pada soal, sehingga hasilnya akan seperti berikut:
<img width="1680" alt="Screenshot 2023-12-15 at 23 52 23" src="https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/91003946/958a7df8-aee6-4cd8-b621-01c0b034adf3">

<img width="1680" alt="Screenshot 2023-12-15 at 23 50 53" src="https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/91003946/3056869c-f7bd-4615-939a-6470e6976460">


## Nomor 9
> Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit.  (clue: test dengan nmap)\



## Nomor 10
> Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.

Gunakan syntax berikut:
```bash
iptables -A INPUT  -j LOG --log-level debug --log-prefix 'Dropped Packet' -m limit --limit 1/second --limit-burst 10
```

Berikut adalah hasil dari test syntax yang telah dijalankan:
<img width="1680" alt="Screenshot 2023-12-16 at 02 46 34" src="https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/91003946/91731c99-63cf-486d-921c-5ce77f8942c9">

<img width="1680" alt="Screenshot 2023-12-16 at 02 46 07" src="https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/91003946/2f090267-8557-4f34-ad7e-1c60d19c0373">

<img width="1680" alt="Screenshot 2023-12-16 at 02 38 07" src="https://github.com/fadillaarn/Jarkom-Modul-5-E07-2023/assets/91003946/33cb3aa9-60a1-40b4-b6b2-8e8224bd5112">

## Kendala
