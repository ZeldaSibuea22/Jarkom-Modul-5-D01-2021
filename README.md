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
