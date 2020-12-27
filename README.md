# Jarkom_Modul5_Lapres_T09
Anggota Kelompok:
- Donny Kurnia Ramadhani (05311840000004)  
- Muhammad Zulfikar Fauzi (05311840000012)  

## Prerequisites
### A : Pembuatan Topologi
Untuk pembuatan topologi, seperti modul sebelumnya kita konfigurasikan di file Topologi.sh seperti yang diinginkan oleh soal. Berikut adalah isi dari file topologi.sh:
(masukin ss topologi)
### B : Subnetting (VLSM)
Untuk subnetting kita menggunakan teknik VLSM dimana pembagian IP digunakan secukupnya dan seefisien mungkin, kita menggunakan aplikasi Cisco Packet Tracer untuk mempermudah pembagian IP dan routing. Referensi selengkapnya bisa dilihat di Lapres modul sebelumnya pada link ini: (masukin link lapres routingsubnetting)

### C : Routing
Routing dilakukan sesuai yang telah diajarkan di Modul sebelumnya, untuk referensi Lapres bisa dilihat pada link ini: (masukin link lapres).
Berikut adalah contoh konfigurasi salah satu router (SURABAYA) yang sudah dilakukan routing: (masukin gambar routersurabaya)

### D : DHCP Relay dan DHCP Server
Untuk instalasi DHCP Relay dan DHCP Server kita gunakan isc-dhcp-relay pada semua router yang dilewati dan isc-dhcp-server pada Server. Referensi selengkapnya dapat dilihat pada Lapres modul sebelumnya pada link ini: (masukin link lapres)
Berikut adalah contoh konfigurasi pada Router Relay dan Server DHCP: (masukin ss dhcpserver sama router relay)

## Soal
### Nomor 1: Konfigurasi agar dapat mengakses ke luar tanpa menggunakan MASQUERADE di SURABAYA.

### Nomor 2: Konfigurasi agar men-drop semua akses SSH dari luar topologi (UML) ke server dengan IP DMZ di SURABAYA.

### Nomor 3: Konfigurasi agar DHCP dan DNS SERVER tidak dapat menerima koneksi ICMP lebih dari 3 dalam satu waktu.

### Nomor 4: Konfigurasi pada MALANG agar akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat.

### Nomor 5: Konfigurasi pada MALANG agar akses dari subnet GRESIK hanya diperbolehkan pada pukul 17.00 - 07.00 setiap harinya.

### Nomor 6: Konfigurasi pada SURABAYA agar setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada PROBOLINGGO port 80 dan MADIUN port 80.

### Nomor 7: Membuat log semua paket yang telah di-drop pada setiap UML yang memiliki aturan DROP. 
