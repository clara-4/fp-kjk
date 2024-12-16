# Final Project Keamanan Jaringan Komputer (D)
# Kelompok 2

| Nama                     | NRP        |
|--------------------------|------------|
| Atha Rahma               | 5027221030 |
| Jeany Aurellia Putri D   | 5027221008 |
| Clara Valentina          | 5027221016 |
| Angella Christie         | 5027221047 |
| Monika Damelia H         | 5027221011 |

# 1. Simulasi Jaringan

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

# 2. Analisis risiko Berdasarkan standar ISO 27001:2022.

### A. Fokus analisis risiko

1. Firewall Aktif
2. VLAN
3. ACL (Access Control List)
4. IDS/IPS menggunakan Snort

### B. Identifikasi Aset

| ID Aset | Lokasi     | Fungsi                             |
|---------|------------|------------------------------------|
| A1      | Gedung Riset Center DPTSI | Menghubungkan semua segmen jaringan |
| A2      | Perpustakaan lantai 6 | Menyediakan layanan web internal |
| A3      | Lantai 7 | Menyediakan koneksi Wi-Fi ke 4 kelas |
| A4      | Lantai 9	 | 	Menghubungkan lab 1 dan lab 2 |
| A5      | Router atau server IDS | Memantau dan mencegah serangan siber |

### C. Ancaman dan Kerentanan
**Ancaman Umum**

|Kode Ancaman	| Ancaman	| Deskripsi                           |
|---------------|------------|------------------------------------|
|T1 |	Akses Tidak Sah |	Akses tidak sah ke jaringan atau perangkat penting. |
|T2	| Serangan DDoS	| Trafik berlebih yang mengganggu layanan web server. |
|T3	| Serangan Lateral |	Penyebaran serangan antar VLAN tanpa batasan akses. |
|T4	| Port Scanning & Reconnaissance	| Pemindaian port untuk menemukan kerentanan pada server atau perangkat. |
|T5	| Malware dan Exploit	| Penyebaran malware ke jaringan internal (kelas, lab, server). |


**Kerentanan**

| Kode Kerentanan | Kerentanan     | Deskripsi                             |
|---------|------------|------------------------------------|
| V1	| Firewall Tidak Optimal	| Aturan firewall kurang ketat, memungkinkan akses berbahaya dari luar jaringan. |
| V2	| ACL Tidak Diterapkan |	Tidak ada pembatasan trafik antar VLAN, memungkinkan serangan lateral. |
| V3	| Segmentasi VLAN Kurang |	Jaringan tidak dipisahkan secara efektif, memudahkan serangan menyebar. |
|V4	    | Tidak Ada IDS/IPS	| Tidak ada sistem untuk mendeteksi atau mencegah serangan dalam jaringan. |
| V5	| Kebocoran Trafik Tidak Sah	| Trafik yang tidak sah dapat mengakses layanan kritis seperti server. |

### D. Analisis Risiko

| ID Risiko |	Aset Terdampak	| Ancaman	| Kerentanan	| Dampak	| Tingkat Risiko |	Kontrol Mitigasi |
|---------|------------|------------|-------|---------|------------|------------|
|R1	| Server (A2)	| Akses Tidak Sah (T1)|	Firewall Tidak Optimal |	Layanan web diretas dan data bocor.|	Tinggi|	Aktifkan Firewall, buka hanya port 80/443 yang perlu.|
|R2|	Server (A2)|	Serangan DDoS (T2)|	Firewall Tidak Optimal|	Layanan web terganggu (down).	| Tinggi|	Aturan firewall untuk membatasi trafik berlebihan.|
|R3	| Switch VLAN (A3, A4)|	Serangan Lateral (T3)|	ACL Tidak Diterapkan|	Penyebaran malware ke segmen lain.|	Tinggi| 	Terapkan ACL untuk membatasi akses antar VLAN.|
|R4 |	Switch VLAN (A3, A4)|	Port Scanning (T4)|	Firewall Tidak Optimal|	Informasi port digunakan untuk eksploitasi.|	Sedang	| Atur firewall untuk blokir trafik port scanning.|
|R5	| Semua Segmen|	Malware dan Exploit (T5)|	Tidak Ada IDS/IPS |	Kerusakan sistem dan pencurian data. |	Tinggi	| Terapkan IDS/IPS menggunakan Snort. |
|R6	|Trafik Antar VLAN	| Kebocoran Trafik (T1)	| Segmentasi VLAN Kurang|	Akses tidak sah antar jaringan.	| Sedang|	Terapkan segmentasi VLAN yang ketat.|



