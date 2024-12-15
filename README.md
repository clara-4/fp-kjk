# fp-kjk

## Topologi
<img width="619" alt="image" src="https://github.com/user-attachments/assets/3f2db92d-cf01-43e5-8620-9ff8f40fbd12" />

## Topologi Subnetting
<img width="539" alt="image" src="https://github.com/user-attachments/assets/5b283561-d867-4f7c-9cf2-98b0d18a8745" />

## Pembagian IP
<img width="737" alt="image" src="https://github.com/user-attachments/assets/404b60e5-f096-4884-8e5f-68ea26dcbeb2" />

## Konfigurasi

### dptsi (A1-A3)
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
    address 192.243.1.77
    netmask 255.255.255.252

auto eth2
iface eth2 inet static
    address 192.243.1.65
    netmask 255.255.255.248

### perpus-6 (A1-A2)
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

#### server (A2)
auto eth0
iface eth0 inet static
    address 192.243.1.74
    netmask 255.255.255.252
    gateway 192.243.1.73

### lantai9 (A3-A4)
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.243.1.66
    netmask 255.255.255.248
    gateway 192.243.1.65

auto eth1
iface eth1 inet static
    address 192.243.1.1
    netmask 255.255.255.192

#### lab1 (A4)
auto eth0
iface eth0 inet static
    address 192.243.1.2
    netmask 255.255.255.192
    gateway 192.243.1.1

#### lab2 (A4)
auto eth0
iface eth0 inet static
    address 192.243.1.3
    netmask 255.255.255.192
    gateway 192.243.1.1

### lantai7 (A3-A5)
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.243.1.67
    netmask 255.255.255.248
    gateway 192.243.1.65

auto eth1
iface eth1 inet static
    address 192.243.0.1
    netmask 255.255.255.0

#### 701 (A5)
auto eth0
iface eth0 inet static
    address 192.243.0.2
    netmask 255.255.255.0
    gateway 192.243.0.1

#### 702 (A5)
auto eth0
iface eth0 inet static
    address 192.243.0.3
    netmask 255.255.255.0
    gateway 192.243.0.1

#### 703 (A5)
auto eth0
iface eth0 inet static
    address 192.243.0.4
    netmask 255.255.255.0
    gateway 192.243.0.1

#### 704 (A5)
auto eth0
iface eth0 inet static
    address 192.243.0.5
    netmask 255.255.255.0
    gateway 192.243.0.1

## Script Node Router

### dptsi (A1-A3)
route add -net 192.243.1.76 netmask 255.255.255.252 gw 192.243.1.77
route add -net 192.243.1.64 netmask 255.255.255.248 gw 192.243.1.65

### perpus-6 
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.243.1.78

### lantai9 
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.243.1.66

### lantai7 
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.243.1.67

