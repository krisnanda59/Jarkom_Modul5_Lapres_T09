# Jarkom_Modul5_Lapres_T09
Anggota Kelompok:
- Donny Kurnia Ramadhani (05311840000004)  
- Muhammad Zulfikar Fauzi (05311840000012)  

## Prerequisites
### A : Pembuatan Topologi
Untuk pembuatan topologi, seperti modul sebelumnya kita konfigurasikan di file Topologi.sh seperti yang diinginkan oleh soal. Berikut adalah isi dari file topologi.sh:
![topologi_sh](https://user-images.githubusercontent.com/61267430/103164636-700dee00-4840-11eb-948a-464089170703.PNG) 

### B : Subnetting (VLSM)
Untuk subnetting kita menggunakan teknik VLSM dimana pembagian IP digunakan secukupnya dan seefisien mungkin, kita menggunakan aplikasi Cisco Packet Tracer untuk mempermudah pembagian IP dan routing. Referensi selengkapnya bisa dilihat di Lapres modul sebelumnya pada link ini: https://github.com/naminai/Jarkom_Modul4_Lapres_T09

![image](https://user-images.githubusercontent.com/61267430/103167050-6db88d80-485a-11eb-8026-275088193bb9.png)

### C : Routing
Routing dilakukan sesuai yang telah diajarkan di Modul sebelumnya, untuk referensi Lapres bisa dilihat pada link ini: https://github.com/naminai/Jarkom_Modul4_Lapres_T09
Berikut adalah contoh konfigurasi salah satu router (SURABAYA) yang sudah dilakukan routing: 
![settingroutingsurabaya](https://user-images.githubusercontent.com/61267430/103164658-c0854b80-4840-11eb-88d5-6fb8df26c007.PNG)

### D : DHCP Relay dan DHCP Server
Untuk instalasi DHCP Relay dan DHCP Server kita gunakan isc-dhcp-relay pada semua router yang dilewati dan isc-dhcp-server pada Server. Referensi selengkapnya dapat dilihat pada Lapres modul sebelumnya pada link ini: https://github.com/naminai/Jarkom_Modul3_Lapres_T09
Berikut adalah contoh konfigurasi pada Router Relay dan Server DHCP:  
![relayserver](https://user-images.githubusercontent.com/61267430/103164678-f1658080-4840-11eb-91d8-1d5a3f5dcc97.PNG)  
![relay_batu](https://user-images.githubusercontent.com/61267430/103164679-f296ad80-4840-11eb-934a-c753e36c4f02.PNG)  
![relay_kediri](https://user-images.githubusercontent.com/61267430/103164680-f32f4400-4840-11eb-8f0b-f3ca4f48873e.PNG)  
![relay_surabaya](https://user-images.githubusercontent.com/61267430/103164682-f3c7da80-4840-11eb-8d53-c14168b35ec8.PNG)  

Kemudian kita lakukan setting konfigurasi dhcp pada client:  
![settingdhcp_klien](https://user-images.githubusercontent.com/61267430/103164706-3b4e6680-4841-11eb-9314-51062846cfa0.PNG)

## Soal
### Nomor 1: Konfigurasi agar dapat mengakses ke luar tanpa menggunakan MASQUERADE di SURABAYA.
Pertama kita setting konfigurasi berikut seperti pada baris pertama `iptables -t nat -A POSTROUTING -j SNAT --to-source 10.151.74.78 -s 192.168.0.0/16 ` pada SURABAYA:  
![iptables_surabaya](https://user-images.githubusercontent.com/61267430/103164774-f70f9600-4841-11eb-9231-e913de2f8d7e.PNG) 
Kita menggunakan `-t nat` NAT Table pada `-A POSTROUTING` POSTROUTING chain untuk `-j SNAT` mengubah source address yang awalnya berupa private IPv4 address yang memiliki 16-bit blok dari private IP addresses yaitu `-s 192.168.0.0/16` 192.168.0.0/16 menjadi `--to-source 10.151.74.78` IP eth0 SURABAYA yaitu 10.151.72.78 karena SURABAYA adalah satu-satunya router yang terhubung ke cloud melalui eth0.

Berikut hasil uji coba: 

![bisangeping_nomor1](https://user-images.githubusercontent.com/61267430/103166767-ecf89200-4857-11eb-8b58-cbf4f52267ba.PNG)  

### Nomor 2: Konfigurasi agar men-drop semua akses SSH dari luar topologi (UML) ke server dengan IP DMZ di SURABAYA.
Kita setting konfigurasi berikut seperti pada baris `iptables -A FORWARD -d 10.151.83.152/29 -i eth0 -p tcp -m tcp --dport 22 -j DROP` pada SURABAYA:   
![iptables_surabaya](https://user-images.githubusercontent.com/61267430/103164774-f70f9600-4841-11eb-9231-e913de2f8d7e.PNG)  

Kita menggunakan `-A FORWARD` FORWARD chain untuk menyaring paket dengan protokol TCP dari luar topologi menuju ke DHCP Server MOJOKERTO dan DNS Server MALANG (yang berada di satu subnet yang sama yaitu subnet 10.151.83.152/29), dimana akses SSH yang masuk ke DHCP Server MOJOKERTO dan DNS Server MALANG melalui interfaces eth0 dari DHCP Server MOJOKERTO dan DNS Server MALANG agar di DROP (dalam kasus ini sudah diimplementasikan logging sehingga jump ke LOGGING).

Berikut hasil uji coba:   

![image](https://user-images.githubusercontent.com/61267430/103166964-b7ed3f00-4859-11eb-9619-f0baeab8adb6.png) 

### Nomor 3: Konfigurasi agar DHCP dan DNS SERVER tidak dapat menerima koneksi ICMP lebih dari 3 dalam satu waktu.
Kita setting pada DHCP dan DNS Server (Mojokerto dan Malang) konfigurasi seperti di baris keempat `iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP` berikut ini:  
![iptables_malang](https://user-images.githubusercontent.com/61267430/103164868-44d8ce00-4843-11eb-93af-f2643066d4da.PNG)  
![iptables_mojokerto](https://user-images.githubusercontent.com/61267430/103164869-4609fb00-4843-11eb-9023-cf998259df32.PNG)  

Karena merupakan paket yang di DROP maka disini sudah diimplementasikan LOGGING sehingga jump ke LOGGING. Kita menggunakan INPUT chain untuk menyaring paket dengan protokol ICMP yang masuk agar dibatasi dengan `-m connlimit --connlimit-above 3`  sehingga hanya dibatasi maksimal 3 koneksi saja dan `--connlimit-mask 0` berasal darimana saja, sehingga selebihnya akan di DROP. 

Berikut hasil uji coba:

![nomor3](https://user-images.githubusercontent.com/61267430/103166778-0ac5f700-4858-11eb-9c3a-1ce95d07dc27.PNG)

### Nomor 4: Konfigurasi pada MALANG agar akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat.
Kita setting konfigurasi pada MALANG seperti pada baris 5, 6, dan 7 seperti berikut:  
![iptables_malang](https://user-images.githubusercontent.com/61267430/103164868-44d8ce00-4843-11eb-93af-f2643066d4da.PNG)  
```
iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 00:00 --timestop 06:59 --weekdays Mon,Tue,Wed,Thu,Fri -j REJECT
iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 17:01 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j REJECT
iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 00:00 --timestop 23:59 --weekdays Sat,Sun -j REJECT
```

Kita menggunakan INPUT chain untuk menyaring paket dari subnet 192.168.2.0/24 dan `timestart` dan `timestop` untuk jam dan `weekdays` untuk hari di luar ketentuan jam yang diberikan, sehingga akan di REJECT.

Berikut hasil uji coba:

![no4_bisa](https://user-images.githubusercontent.com/61267430/103166786-203b2100-4858-11eb-9d84-59adb344ffe8.PNG)    

![no4_gabisa](https://user-images.githubusercontent.com/61267430/103166788-20d3b780-4858-11eb-88b7-4e63f98ed0e7.PNG)    
  

### Nomor 5: Konfigurasi pada MALANG agar akses dari subnet GRESIK hanya diperbolehkan pada pukul 17.00 - 07.00 setiap harinya.
Kita setting konfigurasi pada MALANG seperti berikut:  
![iptables_malang](https://user-images.githubusercontent.com/61267430/103164868-44d8ce00-4843-11eb-93af-f2643066d4da.PNG)  
```
iptables -A INPUT -s 192.168.0.0/24 -m time --timestart 07:01 --timestop 16:59 -j REJECT
```   
Kita menggunakan INPUT chain untuk menyaring paket dari subnet 192.168.2.0/24 dan `timestart` dan `timestop` untuk ketentuan jam di luar ketentuan jam yang diberikan, sehingga akan di REJECT.

Berikut hasil uji coba: 

![no5_bisa](https://user-images.githubusercontent.com/61267430/103166796-33e68780-4858-11eb-89dd-3ff8fa6401e0.PNG)  

![no5_gabisa](https://user-images.githubusercontent.com/61267430/103166799-347f1e00-4858-11eb-9309-5ca252f3b8ca.PNG)  

### Nomor 6: Konfigurasi pada SURABAYA agar setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada PROBOLINGGO port 80 dan MADIUN port 80.
nope.

### Nomor 7: Membuat log semua paket yang telah di-drop pada setiap UML yang memiliki aturan DROP.  
![iptables_surabaya](https://user-images.githubusercontent.com/61267430/103164774-f70f9600-4841-11eb-9231-e913de2f8d7e.PNG)  
![iptables_malang](https://user-images.githubusercontent.com/61267430/103164868-44d8ce00-4843-11eb-93af-f2643066d4da.PNG)  
![iptables_mojokerto](https://user-images.githubusercontent.com/61267430/103164869-4609fb00-4843-11eb-9023-cf998259df32.PNG)  
```
iptables -N LOGGING
iptables -A LOGGING -j LOG --log-prefix "LOG:DROPPED " --log-level 6
iptables -A LOGGING -j DROP
```

Pertama kita membuat chain baru dengan `-N` dengan nama LOGGING kemudian kita menambahkan rule baru di LOGGING untuk me-log dengan prefix LOG:DROPPED untuk menandakan dia pernah masuk ke LOGGING dengan log-level 6 untuk warning. Terakhir, kita tambahkan rule untuk men-drop paket yang sudah di-log.

Berikut hasil uji coba:   

Pertama kita buka logging-nya di `/var/log/messages` yang merupakan default untuk logging:  

![cmd_log](https://user-images.githubusercontent.com/61267430/103166814-46f95780-4858-11eb-985c-a1b4bb71516a.PNG) 

Kemudian kita grep sesuai prefix kita sehingga terlihat seperti berikut:  

![no7_droppedpacket_malang](https://user-images.githubusercontent.com/61267430/103166753-bde22080-4857-11eb-9f4c-51628f5fcf20.PNG)  
