# Lapres Modul 4


## Cisco (Classless VLSM)

### Menentukan Subnet
untuk menentukan banyak subnet yang diperlukan, dilakukan pembagian seperti gambar berikut.

![VLSM Subnet](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/VLSM_1.png)

### Pembagian IP
setelah subnet dibagi, maka dilakukan pembagian IP berdasarkan kebutuhan masing-masing subnet. dapat dilihat pada tabel berikut.
| Subnet | IP | Netmask | Netmask | NID |
|---|---|---|---|---|
| A1 |	13 |	/28 |	255.255.255.240 |	192.168.0.16/28 |
| A2 |	721 |	/22 |	255.255.252.0 |	192.168.16.0/22 |
| A3 |	521 |	/22 |	255.255.252.0 |	192.168.12.0/22 |
| A4 |	501 |	/23 |	255.255.254.0 |	192.168.2.0/23 |
| A5 |	2 |	/30 |	255.255.255.252 |	192.168.0.12/30 |
| A6 |	2 |	/30 |	255.255.255.252 |	192.168.0.8/30 |
| A7 |	251 |	/24 |	255.255.255.0 |	192.168.1.0/24 |
| A8 |	701 |	/22 |	255.255.252.0 |	192.168.8.0/22 |
| A9 |	2021 |	/21 |	255.255.248.0 |	192.168.24.0/21 |
| A10 |	2 |	/30 |	255.255.255.252 |	192.168.0.4/30 |
| A11 |	2 |	/30 |	255.255.255.252 |	192.168.0.0/30 |
| A12 |	1001 |	/22 |	255.255.252.0 |	192.168.4.0/22 |
| A13 |	101 |	/25 |	255.255.255.128 |	192.168.0.128/25 |
| **Total** |	5839 |	/19 | | |

selain itu dilakukan hal yang sama untuk server **Malang** dan **Mojokerto** seperti pada tabel berikut.
| Server | Netmask | Netmask | NID |
|---|---|---|---|
| Malang |	30 |	255.255.255.252 |	10.151.73.72/30 |
| Mojokerto |	30 |	255.255.255.252 |	10.151.73.76/30 |

### Pohon Pembagian IP
IP yang diberikan ke masing-masing subnet ditentukan dari pohon pembagian berikut. root menggunakan **192.168.0.0** dengan netmask /19. dari situ kemudian dilakukan pembagian seperti pada gambar di bawah.

![VLSM Tree](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/VLSM_2.png)

pohon yang besar merupakan pembagian IP untuk subnet A1 - A13, dan pohon kecil adalah untuk server.

### Topologi CPT
berikut adalah tampilan topologi sistem yang sudah dibangun pada CPT.

![VLSM Cisco](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/VLSM_3.png)

#### Pengaturan Router
pada router, kita atur konfigurasi interface sesuai sambungannya. contohnya dapat dilihat pada gambar di bawah, yaitu pada router **Madiun**. dari router ini, terdapat dua sambungan yaitu menuju *A1* dan *A4*. dari router **Madiun**, yang menuju ke *A1* adalah `Fa0/1`, maka pada interface `Fa0/1` diset seperti berikut.

![VLSM Cisco](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/VLSM_4.png)

keterangan :
- `IPv4 Address` adalah NID *A1* + 1 = 192.168.0.17
- `Subnet Mask` adalah netmask dari *A1* = 255.255.255.240

contoh lain adalah pada `Fa0/0` router **Madiun** yang mengarah ke *A4*. berikut konfigurasi interfacenya.

![VLSM Cisco](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/VLSM_5.png)

keterangan :
- `IPv4 Address` adalah NID *A4* + 1 = 192.168.2.1
- `Subnet Mask` adalah netmask dari *A4* = 255.255.254.0

konfigurasi interface dilakukan untuk semua router lainnya berdasarkan hubungan masing-masing dengan subnet yang berdekatan.

#### Pengaturan Client
pada klien, yaitu PC-PT, kita atur konfigurasi pada `IP Configuration`. sebagai contoh, berikut klien **Bojonegoro** pada subnet *A1* yang terhubung dnegan router **Madiun**.

![VLSM Cisco](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/VLSM_6.png)

keterangan :
- `IPv4 Address` adalah NID *A1* + 2 (diberikan +2 karena +1 sudah digunakan untuk router **Madiun**) = 192.168.0.18
- `Subnet Mask` adalah netmask dari *A1* = 255.255.255.240
- `Default Gateway` adalah NID dari router **Madiun** = 192.168.0.17

konfigurasi IP dilakukan untuk klien-klien lainnya berdasarkan hubungan masing-masing dengan router yang berdekatan.

#### Pengaturan Server
pada server, dilakukan konfigurasi interface sesuai sambungannya. contohnya adalah pada server **Mojokerto** yang terhubung dengan router **Surabaya**. berikut konfigurasi pada **Surabaya** sambungan `Eth1/0` yang mengarah ke **Mojokerto**.

![VLSM Cisco](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/VLSM_7.png)

keterangan :
- `IPv4 Address` adalah NID *Mojokerto* + 1 = 10.151.73.77
- `Subnet Mask` adalah netmask dari *Mojokerto* = 255.255.255.252

dan berikut konfigurasi **Mojokerto** sambungan `Fa0` yang terhubung ke **Surabaya**.

![VLSM Cisco](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/VLSM_8.png)

keterangan :
- `IPv4 Address` adalah NID *Mojokerto* + 2 (diberikan +2 karena +1 sudah digunakan untuk router **Surabaya**) = 10.151.73.78
- `Subnet Mask` adalah netmask dari *Mojokerto* = 255.255.255.252

#### Routing
selanjutnya dilakukan routing untuk mengenalkan subnet pada router.

## UML (Classless CIDR)


**Jawaban**


![no11](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr11.png)


**Revisi**


Dari topologi bagi menjadi beberapa bagian subnet dan diberi label A1 hingga terakhir


![no1](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr1.png)


Pada setiap subnet gabung dengan subnet yang berdekatan dimulai dari subnet yang paling jauh dan diberi netmask satu tingkat lebih besar dari netmask yang paling besar di antara keduanya


Subnet yang paling jauh adalah subnet A1 maka A1 digabung dengan subnet di dekatnya yaitu A2

![no2](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr2.png)

Subnet A1 dan subnet A2 digabung menjadi subnet B1, didapatkan netmask /21


Hal yang sama dilakukan pada subnet yang lain sampai didapatkan satu subnet terbesar yang dimana subnet tersebut adalah topologi secara keseluruhan 


![no3](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr3.png)

- subnet B1 digabung dengan subnet A2 menjadi subnet C1, didapatkan netmask /20

- subnet A5 dan subnet A6 digabung menjadi subnet C2, didapatkan netmask /22

- subnet A12 dan subnet A13 digabung menjadi subnet C3, didapatkan netmask /20


![no4](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr4.png)

- subnet A4 dan subnet C2 digabung menjadi subnet D1, didapatkan netmask /21

- subnet A11 dan subnet C3 digabung menjadi subnet D2, didapatkan netmask /19

- subnet A10 dan subnet A9 digabung menjadi subnet D3, didapatkan netmask /21


![no5](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr5.png)

- subnet C1 dan subnet D1 digabung menjadi subnet E1, didapatkan netmask /19

- subnet D2 dan subnet D3 digabung menjadi subnet E2, didapatkan netmask /18


![no6](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr6.png)

- subnet A7 dan subnet E1 digabung menjadi subnet F1, didapatkan netmask /18

- subnet A8 dan subnet E2 digabung menjadi subnet F2, didapatkan netmask /17


![no7](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr7.png)


- subnet F1 dan subnet F2 digabung menjadi subnet G1, didapatkan netmask /16


Dari pembagian subnet di atas dapat didapatkan pembagian IP dengan menggunakan susunan tree sebagai berikut


![no10](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr10.png)


Dari perhitungan didapatkan hasil nid, netmask, dan broadcast address sebagai berikut


![no8](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr8.png)

![no9](https://github.com/wardahnab/Jarkom_Modul4_Lapres_A08/blob/main/Gambar/cidr9.png)
