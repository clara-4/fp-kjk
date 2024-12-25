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
#### 1. Firewall Aktif
Firewall adalah komponen utama dalam menjaga keamanan jaringan dengan cara memantau dan mengontrol lalu lintas yang masuk dan keluar dari sistem. Firewall (melalui penggunaan iptables) diterapkan untuk membatasi dan mengontrol akses ke server dengan cara yang sangat ketat. Berikut adalah beberapa aturan yang diterapkan pada firewall:

Pembatasan Akses SSH (port 22): Aturan firewall diterapkan untuk menerima koneksi SSH hanya dari alamat IP tertentu ```192.243.1.2``` dan ```192.243.1.3```, serta menolak koneksi dari IP lainnya. Digunakan untuk mencegah akses tidak sah ke server melalui port SSH.

Pembatasan Koneksi HTTP (port 80): Untuk port HTTP, firewall membatasi jumlah koneksi baru (maksimum 10 koneksi) yang dapat diterima oleh server, untuk melindungi dari serangan DoS (Denial of Service). Koneksi lebih dari jumlah tersebut akan ditolak dengan memberikan reset TCP.

Pencegahan Serangan Port Scan: Aturan firewall juga diterapkan untuk mendeteksi dan memblokir teknik pemindaian port seperti XMAS scan, NULL scan, dan SYN flood. Hal tersebut memberikan pertahanan terhadap teknik pemetaan port yang digunakan oleh penyerang untuk menemukan celah di sistem.

SYN Flood Mitigation: Firewall mendeteksi serangan SYN flood yang sering digunakan dalam serangan DoS. Jika terlalu banyak koneksi SYN baru diterima dalam waktu singkat, firewall akan memblokirnya.

#### 2. ACL (Access Control List)
ACL adalah teknik yang digunakan untuk membatasi akses ke sumber daya tertentu dalam jaringan. ACL diterapkan pada level jaringan dan sistem untuk membatasi siapa yang dapat mengakses port atau layanan tertentu.

Kontrol Akses pada Port 22 (SSH): ACL digunakan untuk mengontrol siapa saja yang dapat mengakses port SSH pada server. Aturan firewall membatasi akses SSH hanya untuk alamat IP tertentu, sehingga hanya perangkat yang dikenal yang dapat masuk dan terhubung ke server. Hal tersebut digunakan untuk mengurangi risiko akses tidak sah.

Kontrol Akses Jaringan: Selain kontrol di tingkat aplikasi (seperti port 22 dan 80), ACL juga diterapkan untuk mengontrol akses ke subnet dan jaringan yang lebih besar dengan menentukan rute yang dapat diakses antar subnet (misalnya, ```route add -net 192.243.1.72 netmask 255.255.255.252 gw 192.243.1.78```).

#### 3. Segmentasi Jaringan
Segmentasi jaringan adalah proses membagi jaringan besar menjadi beberapa segmen atau subnet yang lebih kecil untuk meningkatkan kinerja dan keamanan. Dengan membagi jaringan, akses antara berbagai bagian jaringan dapat terkontrol dengan baik, membatasi potensi penyebaran ancaman, dan memastikan bahwa hanya pihak yang berwenang yang bisa mengakses sumber daya tertentu.

Subnetting pada Jaringan: Berbagai perangkat dikelompokkan ke dalam subnet yang terpisah. Misalnya, perangkat di jaringan 192.243.1.0/26 dipisahkan dari jaringan lain, dan ada pembagian lebih lanjut seperti di jaringan 192.243.0.0/24 untuk membatasi komunikasi antara jaringan yang berbeda.

Segmentasi berdasarkan Fungsi: Subnet yang berbeda juga digunakan untuk memisahkan berbagai jenis perangkat atau fungsi, seperti server (perpus-6), router (dptsi), dan perangkat lain di jaringan. Hal ini memastikan bahwa perangkat dengan fungsi yang berbeda tidak berkomunikasi langsung kecuali diperlukan.

Keamanan Berlapis: Segmentasi jaringan memperkenalkan keamanan berlapis, di mana perangkat atau jaringan yang lebih sensitif (misalnya, server) dapat ditempatkan di segmen terpisah dengan kontrol akses yang lebih ketat, sementara perangkat lain (seperti workstation atau perangkat pengguna) ditempatkan di subnet yang berbeda dengan pembatasan yang sesuai.

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
### Server
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
apt-get update
apt install apache2 -y
service apache2 start
apt install apache2-utils

# Aturan SSH: Terima hanya dari IP tertentu 
iptables -A INPUT -p tcp --dport 22 -s 192.243.1.2 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -s 192.243.1.3 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j REJECT

# Aturan HTTP: Batasi koneksi baru jika melebihi 10 khusus untuk port 80 dapat diakses oleh semua client
iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW -m connlimit --connlimit-above 10 -j REJECT --reject-with tcp-reset
iptables -A INPUT -p tcp --dport 80 -j ACCEPT

# Blokir NULL scan (tidak ada flag TCP yang diset)
iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP

# Blokir XMAS scan (semua flag TCP diset)
iptables -A INPUT -p tcp --tcp-flags ALL ALL -j DROP

# Blokir FIN scan (hanya flag FIN diset)
iptables -A INPUT -p tcp --tcp-flags ALL FIN -j DROP

# Deteksi dan blokir pemindaian port (SYN flood atau scanning)
iptables -A INPUT -p tcp --syn -m multiport --dports 1:65535 -m conntrack --ctstate NEW \
         -m recent --set --name PORTSCAN --rsource
iptables -A INPUT -p tcp --syn -m multiport --dports 1:65535 -m conntrack --ctstate NEW \
         -m recent --update --seconds 60 --hitcount 10 --name PORTSCAN --rsource \
         -j LOG --log-prefix "PORTSCAN DETECTED: "
iptables -A INPUT -m recent --rcheck --seconds 60 --hitcount 10 --name PORTSCAN --rsource \
         -j DROP
```
### lab1
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
apt-get update
apt install netcat
apt install apache2-utils
```
### 701
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
apt-get update
apt install netcat
apt install apache2-utils
```
## Configurasi Tambahan
### lab1
uji port
- port 80
`curl http://192.243.1.74:80`

- port 22
`echo "Hello from client!" | nc 192.243.1.74 22`

uji batas akses (limit akses per user)
```
for i in {1..20}; do curl -s -o /dev/null -w "%{http_code}\n" http://192.243.1.74/; sleep 0.01; done
```


### 701
uji port
- port 80 :
`curl http://192.243.1.74:80`

- port 22 :
`echo "Hello from client!" | nc 192.243.1.74 22`

uji batas akses (limit akses per user)
```
for i in {1..20}; do curl -s -o /dev/null -w "%{http_code}\n" http://192.243.1.74/; sleep 0.01; done
```

uji scan
```
nmap 192.243.1.74
```
### server
uji batas akses (limit akses per user)
```
tcpdump -i eth0 port 80
```


# 2. Analisis risiko Berdasarkan standar ISO 27001:2022.

### A. Fokus analisis risiko

1. Firewall Aktif
2. ACL (Access Control List)
3. Segmentasi jaringan

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

| **Kode Ancaman** | **Ancaman**             | **Deskripsi**                                                                                                                                                 |
|-------------------|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| A-01             | Unauthorized Access    | Ancaman akses tidak sah melalui port yang terbuka pada server (misalnya, SSH pada port 22).                                                                  |
| A-02             | Denial of Service (DoS) | Serangan yang mencoba membanjiri server dengan koneksi HTTP baru sehingga layanan menjadi tidak responsif.                                                   |
| A-03             | Port Scanning          | Upaya pemetaan port terbuka pada server untuk menemukan layanan yang dapat dieksploitasi.                                                                    |
| A-04             | XMAS Scan              | Serangan menggunakan paket dengan semua flag TCP diatur untuk mendeteksi port terbuka atau layanan yang rentan.                                              |
| A-05             | NULL Scan              | Serangan menggunakan paket tanpa flag TCP untuk melewati firewall yang kurang dikonfigurasi.                                                                |
| A-06             | SYN Flood              | Serangan yang memanfaatkan banyak koneksi SYN baru untuk membanjiri server dan mengganggu konektivitas.|

**Kerentanan**
| **Kode Kerentanan** | **Kerentanan**                   | **Deskripsi**                                                                                                                                       |
|----------------------|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| V-01                | Access Control Implementation   | Penerapan kontrol akses pada port 22 (SSH), yang hanya menerima koneksi dari alamat IP tertentu untuk mencegah akses tidak sah.                     |
| V-02                | Firewall Rules                  | Firewall dikonfigurasi untuk menolak koneksi pada port 22 selain dari IP yang diizinkan, serta menerapkan aturan pembatasan koneksi pada port 80.    |
| V-03                | Port Scanning Defense           | Firewall dikonfigurasi untuk mendeteksi dan memblokir aktivitas pemindaian port menggunakan teknik SYN flood atau scan lainnya.                      |
| V-04                | XMAS Scan Mitigation            | Firewall dikonfigurasi untuk memblokir paket dengan semua flag TCP diatur (XMAS scan).                                                              |
| V-05                | NULL Scan Mitigation            | Firewall dikonfigurasi untuk memblokir paket tanpa flag TCP yang disetel (NULL scan).                                                               |
| V-06                | SYN Flood Mitigation            | Firewall menggunakan aturan untuk mendeteksi dan memblokir koneksi SYN baru yang mencurigakan dalam jumlah besar.                                   |
| V-07                | Rate Limiting Implementation    | Pembatasan koneksi baru pada port 80 diterapkan untuk mencegah penyalahgunaan sumber daya dengan koneksi yang berlebihan.                           |

### D. Analisis Risiko

| ID Risiko |	Aset Terdampak	| Ancaman	| Kerentanan	| Dampak	| Tingkat Risiko |	Kontrol Mitigasi |
|---------|------------|------------|-------|---------|------------|------------|
|R1	| Server (A2)	| Akses Tidak Sah (T1)|	Firewall Tidak Optimal |	Data pada layanan web internal rentan bocor.|	Tinggi|	**Batasi Akses ke Server dari IP Tertentu**: Konfigurasi firewall agar hanya IP tertentu yang dapat mengakses server.|
|R2|	Server (A2)|	Serangan DDoS (T2)|	Firewall Tidak Optimal|	Gangguan layanan web server.	| Tinggi|	**Batasi Akses Satu IP**: Atur firewall untuk hanya mengizinkan satu koneksi aktif per IP untuk mencegah penyalahgunaan.|
|R3	| Server (A2)|	Port Scanning (T4)|	Firewall Tidak Optimal|	Informasi port digunakan untuk eksploitasi.|	Tinggi| 	**Blokir IP jika terdeteksi nmap atau port scanning**: Konfigurasikan firewall untuk mendeteksi pola scanning dan memblokir IP tersebut.|

# 3. Implementasi Teknik Keamanan Jaringan Komputer berdasarkan Analisis Resiko

### Batasi Akses ke Server dari IP Tertentu
- Hanya izinkan IP tertentu yang memiliki akses ke server melalui pengaturan firewall.

![Screenshot 2024-12-23 194338](https://github.com/user-attachments/assets/127025a4-91f9-4c8a-b82d-5f0f4f1a223a)

### Blokir Akses Satu IP
- Konfigurasi firewall atau server untuk hanya mengizinkan satu koneksi aktif dari satu IP. Hal ini gapat mengurangi resiko penggunaan berlebihan oleh IP tertentu yang berpotensi melakukan serangan seperti DDoS.

![Screenshot 2024-12-23 194717](https://github.com/user-attachments/assets/2ab24ee0-bd60-472f-a799-5fb7cb5c2da3)

![image](https://github.com/user-attachments/assets/2b71fe44-f7b3-4149-9db4-a22b039cd222)

![image](https://github.com/user-attachments/assets/65e8160b-ea59-4826-bb6d-5274e9051509)


### Blokir IP jika Terdeteksi NMAP atau Port Scanning 
- Tambahkan aturan deteksi scanning di firewall. Jika terdeteksi pola scanning dari alat seperti nmap, IP tersebut langsung diblokir secara otomatis dalam periode tertentu

# 4. Bentuk Serangan untuk Uji Coba Teknik Keamanan Jaringan Komputer 

### Batasi Akses ke Server dari IP Tertentu
- Pada client 704, tidak dapat melakukan nc pada server khususnya port 22 karena IP 704 sudah di block oleh server.

![Screenshot 2024-12-23 194535](https://github.com/user-attachments/assets/73059c17-bba1-4aba-ae1e-81e300c6eb26)

- Sedangkan pada client Lab1 berhasil melakukan nc dan dapat mengirimkan pesan dari client ke server.

![Screenshot 2024-12-23 194437](https://github.com/user-attachments/assets/6ae972ec-c0ed-461a-8a92-01c23ea3cafd)

![Screenshot 2024-12-23 194339](https://github.com/user-attachments/assets/9dd02de2-3b7d-4368-9782-0008e2bec3ba)

- Melakukan curl IP server pada port 80 di kedua client

![Screenshot 2024-12-23 194817](https://github.com/user-attachments/assets/c0f7b3cf-3332-4601-bc60-b7cc84952e75)

![Screenshot 2024-12-23 194849](https://github.com/user-attachments/assets/de19f47b-bb1a-487b-87a0-b9cc31856e53)
 

### Blokir Akses Satu IP

- Statistik untuk hasil penangkapan paket jaringan pada client 704 dan Lab 1

![Screenshot 2024-12-23 194717](https://github.com/user-attachments/assets/9382b5e5-b1e0-4b0c-9ac9-cfc88574d6ec)

![Screenshot 2024-12-23 194755](https://github.com/user-attachments/assets/a67076ab-0259-4342-b087-3cccf42f2a69)

### Blokir IP jika Terdeteksi NMAP atau Port Scanning 

- Melakukan NMAP untuk scanning IP server dan memastikan server client terblokir setelah melakukan NMAP

![Screenshot 2024-12-23 195117](https://github.com/user-attachments/assets/abbe8e91-8040-4a91-a389-a2f715c2504e)
