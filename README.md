# fp-kjk

## Topologi
<img width="619" alt="image" src="https://github.com/user-attachments/assets/3f2db92d-cf01-43e5-8620-9ff8f40fbd12" />

## Deskripsi Topologi
Topologi jaringan ini dirancang untuk memenuhi kebutuhan konektivitas dan keamanan di lingkungan gedung pusat riset DPTSI, dengan standar keamanan ISO 27001:2022. Berikut adalah komponen dan deskripsi dari topologi yang ada:

### Komponen Utama:
#### Router Utama (Backbone) DPTSI
Router utama bertindak sebagai penghubung seluruh jaringan di gedung dan memastikan pengelolaan lalu lintas data yang efisien. Router ini dilengkapi dengan firewall sebagai lapisan keamanan utama untuk melindungi jaringan dari ancaman eksternal dan internal.

#### Server di Lantai 6 Perpustakaan
Server ini menyediakan layanan web yang hanya dapat diakses oleh jaringan internal. Lokasinya di lantai 6 perpustakaan memastikan akses yang mudah untuk pengelolaan dan pengamanan fisik.

#### Jaringan di Lantai 7 Tower 2
Lantai 7 terdiri dari 4 ruang kelas, masing-masing dengan kapasitas 40 mahasiswa. Setiap kelas dilengkapi dengan fasilitas Wi-Fi untuk mendukung proses pembelajaran dan aktivitas jaringan.

#### Jaringan di Lantai 9 Tower 2
Lantai 9 memiliki 2 laboratorium komputer:

Laboratorium 1: Terdiri dari 25 PC dengan koneksi Ethernet.
Laboratorium 2: Terdiri dari 25 PC dengan koneksi Ethernet.
Selain koneksi Ethernet, kedua laboratorium juga dilengkapi dengan konektivitas Wi-Fi untuk mendukung fleksibilitas pengguna.
Koneksi ke Awan (Internet)
Seluruh jaringan gedung terhubung ke jaringan eksternal (Internet) melalui NAT yang dikelola di router utama DPTSI.

### Keamanan Jaringan:
#### Firewall
Firewall yang terpasang di router utama DPTSI dirancang untuk memfilter lalu lintas data dan mencegah akses tidak sah ke jaringan internal, sesuai dengan prinsip pengelolaan risiko dalam ISO 27001:2022.

#### Akses Internal Terbatas
Server di lantai 6 hanya dapat diakses dari jaringan internal untuk menjaga kerahasiaan dan integritas data.

## Topologi Subnetting
<img width="539" alt="image" src="https://github.com/user-attachments/assets/5b283561-d867-4f7c-9cf2-98b0d18a8745" />

## Pembagian IP
<img width="737" alt="image" src="https://github.com/user-attachments/assets/404b60e5-f096-4884-8e5f-68ea26dcbeb2" />

## Konfigurasi

### dptsi (A1-A3)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

#perpus
auto eth1
iface eth1 inet static
    address 192.243.1.77
    netmask 255.255.255.252

#tw2
auto eth2
iface eth2 inet static
    address 192.243.1.65
    netmask 255.255.255.248
```

### perpus-6 (A1-A2)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.243.1.78
    netmask 255.255.255.252
    gateway 192.243.1.77

auto eth1
iface eth1 inet static
    address 192.243.1.73
    netmask 255.255.255.252
```

#### server (A2)
```
auto eth0
iface eth0 inet static
    address 192.243.1.74
    netmask 255.255.255.252
    gateway 192.243.1.73
```

### lantai9 (A3-A4)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.243.1.66
    netmask 255.255.255.248
    gateway 192.243.1.65

#lab
auto eth1
iface eth1 inet static
    address 192.243.1.1
    netmask 255.255.255.192
```

#### lab1 (A4)
```
auto eth0
iface eth0 inet static
    address 192.243.1.2
    netmask 255.255.255.192
    gateway 192.243.1.1
```

#### lab2 (A4)
```
auto eth0
iface eth0 inet static
    address 192.243.1.3
    netmask 255.255.255.192
    gateway 192.243.1.1
```

### lantai7 (A3-A5)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.243.1.67
    netmask 255.255.255.248
    gateway 192.243.1.65

#kelas
auto eth1
iface eth1 inet static
    address 192.243.0.1
    netmask 255.255.255.0
```

#### 701 (A5)
```
auto eth0
iface eth0 inet static
    address 192.243.0.2
    netmask 255.255.255.0
    gateway 192.243.0.1
```

#### 702 (A5)
```
auto eth0
iface eth0 inet static
    address 192.243.0.3
    netmask 255.255.255.0
    gateway 192.243.0.1
```

#### 703 (A5)
```
auto eth0
iface eth0 inet static
    address 192.243.0.4
    netmask 255.255.255.0
    gateway 192.243.0.1
```

#### 704 (A5)
```
auto eth0
iface eth0 inet static
    address 192.243.0.5
    netmask 255.255.255.0
    gateway 192.243.0.1
```

## Script Node Router

### dptsi (A1-A3)
```
route add -net 192.243.1.72 netmask 255.255.255.252 gw 192.243.1.78

#ke tw2
route add -net 192.243.1.0  netmask 255.255.255.192 gw 192.243.1.66
route add -net 192.243.0.0  netmask 255.255.255.0   gw 192.243.1.67
```

### perpus-6 
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.243.1.77
```

### lantai9 
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.243.1.65
```

### lantai7 
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.243.1.65
```

