# Jarkom-Modul-5-D01-2021
Kelompok D01:
1. Zelda Elma Sibuea / 05111940000038
2. Rosa Amalia / 05111940000106
3. Raharja Dui Putra Sutedjo / 05111940000222

## Soal A
Tugas pertama kalian yaitu membuat topologi jaringan dengan keterangan sebagai berikut: <br>
- Doriki adalah DNS Server
- Jipangu adalah DHCP Server
- Maingate dan Jorge adalah Web Server
- Jumlah Host pada Blueno adalah 100 host
- Jumlah Host pada Cipher adalah 700 host
- Jumlah Host pada Elena adalah 300 host
- Jumlah Host pada Fukurou adalah 200 host
<img alt="image" src="https://user-images.githubusercontent.com/68428942/145133336-57d8feb6-9a5c-4bf6-b091-e15d7c991eee.png">

## Soal B
Luffy ingin meminta kalian untuk membuat topologi tersebut menggunakan teknik CIDR atau VLSM. Teknik subnetting yang digunakan adalah teknik VLSM dengan pengerjaan sebagai berikut.

### Pembagian Subnet
![image](https://user-images.githubusercontent.com/68428942/145132079-e7b37a13-8535-47cc-bc9c-35c3db228939.png)

### Tabel Jumlah Host
<img width="605" src="https://user-images.githubusercontent.com/68428942/145132383-f1017266-368c-4a3b-b395-967fdcf1dcc3.png">

### Tree Pembagian IP
![Jarkom](https://user-images.githubusercontent.com/68428942/145132327-54e75f5c-b173-419b-a958-0e489bfc0953.jpg)

### Tabel NID Subnet
<img width="605" src="https://user-images.githubusercontent.com/68428942/145132410-a8b5ac97-6449-411b-a3de-adb4224e141a.png">

## Soal C
Kalian juga diharuskan melakukan Routing agar setiap perangkat pada jaringan tersebut dapat terhubung.

### Konfigurasi Setiap Node
- Foosha
  ```bash
  auto eth0
  iface eth0 inet static
    address 192.168.122.2
    netmask 255.255.255.0
    gateway 192.168.122.1
  
  # A4 Water7
  auto eth1
  iface eth1 inet static
    address 192.192.0.1
    netmask 255.255.255.252
  
  # A5 Guanhao
  auto eth2
  iface eth2 inet static
    address 192.192.0.5
    netmask 255.255.255.252
  ```
- Water7
  ```bash
  # A4 Foosha
  auto eth0
  iface eth0 inet static
    address 192.192.0.2
    netmask 255.255.255.252
    gateway 192.192.0.1
    
  # A3 Chiper
  auto eth1
  iface eth1 inet static
    address 192.192.4.1
    netmask 255.255.252.0
  
  # A1 Doriki Jipangu
  auto eth2
  iface eth2 inet static
    address 192.192.0.9
    netmask 255.255.255.248
  
  # A2 Blueno
  auto eth3
  iface eth3 inet static
    address 192.192.0.129
    netmask 255.255.255.128
  ```
- Guanhao
  ```bash
  # A5 Foosha
  auto eth0
  iface eth0 inet static
    address 192.192.0.6
    netmask 255.255.255.252
    gateway 192.192.0.5
    
  # A7 Fukurou
  auto eth1
  iface eth1 inet static
    address 192.192.1.1
    netmask 255.255.255.0
  
  # A8 Jorge Maingate
  auto eth2
  iface eth2 inet static
    address 192.192.0.25
    netmask 255.255.255.248
    
  # A6 Elena
  auto eth3
  iface eth3 inet static
    address 192.192.2.1
    netmask 255.255.254.0
  ```
- Doriki
  ```bash
  # A1 Water7 Jipangu
  auto eth0
  iface eth0 inet static
    address 192.192.0.10
    netmask 255.255.255.248
    gateway 192.192.0.9
  ```
- Jipangu
  ```bash
  # A1 Water7 Doriki
  auto eth0
  iface eth0 inet static
    address 192.192.0.11
    netmask 255.255.255.248
    gateway 192.192.0.9
  ```
- Blueno
  ```bash
  # A2 Water7
  auto eth0
  iface eth0 inet static
    address 192.192.0.130
    netmask 255.255.255.128
    gateway 192.192.0.129
  ```
- Chiper
  ```bash
  # A3 Water7
  auto eth0
  iface eth0 inet static
    address 192.192.4.2
    netmask 255.255.252.0
    gateway 192.192.4.1
  ```
- Jorge
  ```bash
  # A8 Guanhao Maingate
  auto eth0
  iface eth0 inet static
    address 192.192.0.26
    netmask 255.255.255.248
    gateway 192.192.0.25
  ```
- Maingate
  ```bash
  # A8 Guanhao Jorge
  auto eth0
  iface eth0 inet static
    address 192.192.0.27
    netmask 255.255.255.248
    gateway 192.192.0.25
  ```
- Elena
  ```bash
  # A6 Guanhao
  auto eth0
  iface eth0 inet static
    address 192.192.2.2
    netmask 255.255.254.0
    gateway 192.192.2.1
  ```
- Fukurou
  ```bash
  # A7 Guanhao
  auto eth0
  iface eth0 inet static
    address 192.192.1.2
    netmask 255.255.255.0
    gateway 192.192.1.1
  ```

### Penambahan Routing
Pengaturan routing hanya dilakukan di router Foosha dengan command berikut.
```
route add -net 192.192.0.8 netmask 255.255.255.248 gw 192.192.0.2
route add -net 192.192.0.128 netmask 255.255.255.128 gw 192.192.0.2
route add -net 192.192.4.0 netmask 255.255.252.0 gw 192.192.0.2
route add -net 192.192.2.0 netmask 255.255.254.0 gw 192.192.0.6
route add -net 192.192.1.0 netmask 255.255.255.0 gw 192.192.0.6
route add -net 192.192.0.24 netmask 255.255.255.248 gw 192.192.0.6
```

## Soal D
Tugas berikutnya adalah memberikan ip pada subnet Blueno, Cipher, Fukurou, dan Elena secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

### Water7, Foosha, Guanhao sebagai DHCP Relay
Lakukan instalasi berikut pada router yang bertindak sebagai DHCP Relay.
```
apt-get update
apt-get install isc-dhcp-relay -y
```
Lakukan konfigurasi pada file `/etc/default/isc-dhcp-relay`. Pada bagian `SERVERS=`, masukkan IP milik DHCP Server (Jipangu) dan pada bagian `INTERFACES=` masukkan interface yang terhubung dengan DHCP Client dan DHCP Server. Berikut konfigurasi yang perlu ditambahkan untuk masing-masing router.
```shell
# Water7
SERVERS="192.192.0.11"
INTERFACES="eth0 eth1 eth2 eth3"

# Foosha
SERVERS="192.192.0.11"
INTERFACES="eth1 eth2"

# Guanhao
SERVERS="192.192.0.11"
INTERFACES="eth0 eth1 eth3"
```
Restart DHCP Relay dengan perintah `service isc-dhcp-relay restart`.
Lakukan konfigurasi pada file `/etc/sysctl.conf` untuk membuka IP Forwarding dengan menghapus komentar pada baris:
```
net.ipv4.ip_forward=1
```

### Jipangu sebagai DHCP Server
Lakukan instalasi berikut pada server Jipangu.
```
apt-get update
apt-get install isc-dhcp-server -y
```
Menambahkan interface pada file `/etc/default/isc-dhcp-server`. Pada bagian `INTERFACES=` diisi dengan interface yang akan diberi layanan DHCP. Klien DHCP terhubung dengan Jipangu melalui `eth0`.
```
INTERFACES= "eth0"
```
Konfigurasi pembagian IP di file `/etc/dhcp/dhcpd.conf` untuk masing-masing subnet klien DHCP.
- Subnet A1
  ```shell
  subnet 192.192.0.8 netmask 255.255.255.248 {
    option routers 192.192.0.11; # IP DHCP Server Jipangu
  }
  ```
- Blueno (Subnet A2)
  ```shell
  subnet 192.192.0.128 netmask 255.255.255.128 {
    range 192.192.0.130 192.192.0.254; # range IP yang diberikan
    option routers 192.192.0.129; # IP Gateway (Water7)
    option broadcast-address 192.192.0.255;
    option domain-name-servers 192.192.0.10; # IP Doriki (DNS Server)
    default-lease-time 600;
    max-lease-time 7200;
  }
  ```
- Cipher (Subnet A3)
  ```shell
  subnet 192.192.4.0 netmask 255.255.252.0 {
    range 192.192.4.2 192.192.7.254; # range IP yang diberikan
    option routers 192.192.4.1; # IP Gateway (Water7)
    option broadcast-address 192.192.7.255;
    option domain-name-servers 192.192.0.10; # IP Doriki (DNS Server)
    default-lease-time 600;
    max-lease-time 7200;
  }
  ```
- Fukurou (Subnet A7)
  ```shell
  subnet 192.192.1.0 netmask 255.255.255.0 {
    range 192.192.1.2 192.192.1.254; # range IP yang diberikan
    option routers 192.192.1.1; # IP Gateway (Guanhao)
    option broadcast-address 192.192.1.255;
    option domain-name-servers 192.192.0.10; # IP Doriki (DNS Server)
    default-lease-time 600;
    max-lease-time 7200;
  }
  ```
- Elena (Subnet A6)
  ```shell
  subnet 192.192.2.0 netmask 255.255.254.0 {
    range 192.192.2.2 192.192.3.254; # range IP yang diberikan
    option routers 192.192.2.1; # IP Gateway (Guanhao)
    option broadcast-address 192.192.3.255;
    option domain-name-servers 192.192.0.10; # IP Doriki (DNS Server)
    default-lease-time 600;
    max-lease-time 7200;
  }
  ```
  
Restart DHCP Server dengan perintah `service isc-dhcp-server restart`. Kemudian cek status DHCP dengan perintah `service isc-dhcp-server status`.

### Blueno, Cipher, Fukurou, Elena sebagai klien DHCP
Komentar konfigurasi lama (IP Statis) pada file `/etc/network/interfaces` dan tambahkan baris berikut di setiap klien DHCP.
```
auto eth0
iface eth0 inet dhcp
```
Untuk mengecek IP yang dipinjamkan di klien, cek dengan perintah `ip a`.

## Soal 1
Agar topologi yang dibuat dapat mengakses keluar, Pada soal ini diminta untuk mengkonfigurasi Foosha menggunakan iptables, tetapi Luffy tidak ingin menggunakan MASQUERADE.

Pada router Foosha, tambahkan perintah:
```
iptables -t nat -A POSTROUTING -s 192.192.0.0/16 -o eth0 -j SNAT --to-source 192.168.122.2
```
Dengan isi file `/etc/resolv.conf` DNS Server ke 192.168.122.1
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```
Dengan keterangan: <br>
- `t nat`: Menggunakan tabel NAT karena akan mengubah alamat asal dari paket <br>
- `A POSTROUTING`: Menggunakan chain POSTROUTING karena mengubah asal paket setelah routing <br>
- `s 192.192.0.0/16`: Mendifinisikan alamat asal dari paket yaitu semua alamat IP dari subnet 192.192.0.0/16 <br>
- `o eth0`: Paket keluar dari eth0 MASQUERADE <br>
- `j SNAT`: Menggunakan target SNAT untuk mengubah source atau alamat asal dari paket <br>
- `to-source 192.168.122.2`: Mendefinisikan IP source pengganti, di mana digunakan eth0 MASQUERADE <br>

Pengecekan dengan melakukan ping google.com di node lain, apakah sudah tersambung internet atau belum.
- Melakukan ping di node Guanhao sebelum menambahkan konfigurasi iptables <br>
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145661930-e96afb39-7521-433f-a92e-17746048110d.png">

- Melakukan ping di node Guanhao setelah menambahkan konfigurasi iptables <br>
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145661948-f999b804-9b20-4acb-aa04-8a6079ea65c1.png">
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145661960-28ee8592-2031-48bd-974a-1b0ff57eac24.png">

## Soal 2
Soal ini diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.

Pada router Water7, tambahkan perintah:
```
iptables -A FORWARD -d 192.192.0.10 -p tcp --dport 80 -j REJECT
iptables -A FORWARD -d 192.192.0.11 -p tcp --dport 80 -j REJECT
```
Keterangan:
- `-A FORWARD` : Menggunakan chain FORWARD karena ingin memfilter paket yang melewati Water7
- `-d 192.192.0.10` dan `-d 192.192.0.11` : Mendefinisikan alamat tujuan paket, yaitu Doriki dan Jipangu
- `-p tcp` : Protokol yang digunakan, yaitu tcp
- `--dport 80` : Port yang diguakan, yaitu port HTTP (80)
- `-j REJECT` : Paket ditolak

Untuk melakukan pengecekan, dengan `nmap -p 80 [IP_Jipangu/IP_Doriki]` untuk mendapatkan informasi bahwa akses HTTP sudah ditutup pada server Jipangu dan Doriki. <br>
<img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662025-320490ab-daeb-4b96-87c4-f06ab7dbc3a3.png">

## Soal 3
Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

Pada Jipangu (DHCP Server) dan Doriki (DNS Server), tambahkan perintah berikut.
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

Keterangan:
- `-A INPUT` : Menggunakan chain INPUT karena dikonfigurasikan langsung pada Jipangu dan Doriki
- `-p icmp` : Protokol yang digunakan, yaitu icmp (ping)
- `-m connlimit` : Menggunakan rule connection limit
- `--connlimit-above 3` : Limit yang ditangkap paket adalah di atas 3
- `--connlimit-mask 0` : Hanya memperbolehkan 3 koneksi setiap subnet dalam satu waktu
- `-j DROP` : Paket di drop

Pengecekan dengan melakukan ping IP Jipangu/Doriki di 4 node secara bersamaan. Untuk node ke-4, akan tidak berhasil.<br>
- Pengecekan untuk server Jipangu. Jorge merupakan node ke-4 yang melakukan ping ke server Jipangu <br>
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662253-bb05bda9-ebbb-4fa9-9494-efb4adf0f3f7.png">
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662261-97211ae8-010c-4761-be9a-90e443c6a64f.png">
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662264-bd4ce438-b8cf-4661-b87c-621588cf0ddb.png">
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662273-e89de065-0dd6-47f8-886a-f096b0cac71a.png">

- Pengecekan untuk server Doriki. Jorge merupakan node ke-4 yang melakukan ping ke server Doriki <br>
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662329-ff45189f-bb2a-45d1-b605-96f357ab68b1.png">
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662339-20f2ac38-1cd8-4f09-a9a0-4fba54e2f758.png">
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662343-0a742976-0fd2-472b-80a6-80b2630c22b1.png">
  <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662348-ecf895b3-8575-4959-8f1d-f5269b9f3158.png">

## Soal 4
Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut
- Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis. Selain itu di reject

Pada Doriki, tambahkan perintah berikut:
```bash
# Blueno
iptables -A INPUT -s 192.192.0.128/25 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.192.0.128/25 -j REJECT

# Cipher
iptables -A INPUT -s 192.192.4.0/22 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.192.4.0/22 -j REJECT
```

Keterangan:
- `-A INPUT` : Menggunakan chain INPUT karena langsung dikonfigurasi pada Doriki
- `-s 192.192.0.128/25` dan `-s 192.192.4.0/22` : Alamat asal paket, yaitu subnet A2 dan A3
- `-m time` : Menggunakan rule time
- `--timestart 07:00` : Waktu mulai
- `--timestop 15:00` : Waktu berakhir
- `--weekdays Mon,Tue,Wed,Thu` : Hari
- `-j ACCEPT` : Paket diterima

Untuk konfigurasi iptables paket ditolak:
- `-j REJECT` : Paket ditolak. Sehingga Doriki hanya bisa menerima paket dari waktu yang sudah dikonfigurasi sebelumnya

Pengecekan dengan mengganti tanggal di Blueno dan Cipher di luar dari waktu yang diperbolehkan. Kemudian ping Doriki melalui Blueno dan Cipher.
- Melalui Blueno
  - Setting waktu pada Rabu, jam 08:00 <br>
    <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662690-e438e351-558f-4e89-b08f-ba3546773a1c.png">
  - Setting waktu pada Jumat, jam 08:00 <br>
    <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662723-d8d4f008-0734-40a8-b380-27cf6cc2cfa9.png">
  
- Melalui Cipher
  - Setting waktu pada Rabu, jam 08:00 <br>
    <img width="537" alt="image" src="https://user-images.githubusercontent.com/68428942/145662762-6198c0ec-9f5a-45b3-8f5b-f77575946b0d.png">
  - Setting waktu pada Jumat, jam 08:00 <br>
    <img width="538" alt="image" src="https://user-images.githubusercontent.com/68428942/145662777-3611f822-729b-40c2-8787-4a739781bf70.png">

## Soal 5
Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut
- Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya. Selain itu di reject

Pada Doriki, tambahkan perintah berikut:
```bash
# Elena
iptables -A INPUT -s 192.192.2.0/23 -m time --timestart 15:01 --timestop 23:59 -j ACCEPT
iptables -A INPUT -s 192.192.2.0/23 -m time --timestart 00:00 --timestop 06:59 -j ACCEPT
iptables -A INPUT -s 192.192.2.0/23 -j REJECT

# Fukurou
iptables -A INPUT -s 192.192.1.0/24 -m time --timestart 15:01 --timestop 23:59 -j ACCEPT
iptables -A INPUT -s 192.192.1.0/24 -m time --timestart 00:00 --timestop 06:59 -j ACCEPT
iptables -A INPUT -s 192.192.1.0/24 -j REJECT
```
Keterangan:
- `-A INPUT` : Menggunakan chain INPUT karena langsung dikonfigurasi pada Doriki
- `-s 192.192.2.0/23` dan `-A INPUT -s 192.192.1.0/24` : Alamat asal paket, yaitu subnet A6 dan A7
- `-m time` : Menggunakan rule time
- `--timestart 07:00` Waktu mulai dengan waktu berakhir `--timestop 23:59`
- `--timestart 00:00` Waktu mulai dengan waktu berakhir `--timestop 06:59`
- `-j ACCEPT` : Paket diterima

Konfigurasi dibagi dua karena rule time hanya dapat menerima waktu dari 00:00 hingga 23:59.

Pengecekan dengan mengganti waktu di Elena dan Fukurou di luar jam yang diperbolehkan. Kemudian ping Doriki melalui Elena dan Fukurou.
- Melalui Elena
  - Waktu di setting menjadi jam 01:00 <br>
    <img width="537" alt="image" src="https://user-images.githubusercontent.com/68428942/145662874-85558edf-b10e-4fa6-a787-84b425074520.png">
  - Waktu di setting mnejadi jam 08:00 <br>
    <img width="537" alt="image" src="https://user-images.githubusercontent.com/68428942/145662881-61215bea-3c7c-409a-8ce1-1bada740975a.png">

- Melalui Fukurou
  - Waktu di setting menjadi jam 01:00 <br>
    <img width="537" alt="image" src="https://user-images.githubusercontent.com/68428942/145662898-f8c466ad-02f5-426d-a8d2-2286e7e7a279.png">
  - Waktu di setting mnejadi jam 08:00 <br>
    <img width="537" alt="image" src="https://user-images.githubusercontent.com/68428942/145662917-493a8f3f-c55a-446f-b2d5-85bf0c506818.png">
