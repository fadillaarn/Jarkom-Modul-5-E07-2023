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

## Nomor 2
> Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

## Nomor 3
> Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

## Nomor 4
> Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

## Nomor 5
> Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

## Nomor 6
> Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

## Nomor 7
> Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

## Nomor 8
> Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

## Nomor 9
> Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit.  (clue: test dengan nmap)

## Nomor 10
> Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.

## Kendala
