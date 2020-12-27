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

### C : Routing
Routing dilakukan sesuai yang telah diajarkan di Modul sebelumnya, untuk referensi Lapres bisa dilihat pada link ini: (masukin link lapres).
Berikut adalah contoh konfigurasi salah satu router (SURABAYA) yang sudah dilakukan routing: 
![settingroutingsurabaya](https://user-images.githubusercontent.com/61267430/103164658-c0854b80-4840-11eb-88d5-6fb8df26c007.PNG)

### D : DHCP Relay dan DHCP Server
Untuk instalasi DHCP Relay dan DHCP Server kita gunakan isc-dhcp-relay pada semua router yang dilewati dan isc-dhcp-server pada Server. Referensi selengkapnya dapat dilihat pada Lapres modul sebelumnya pada link ini: (masukin link lapres)
Berikut adalah contoh konfigurasi pada Router Relay dan Server DHCP: 
![relayserver](https://user-images.githubusercontent.com/61267430/103164678-f1658080-4840-11eb-91d8-1d5a3f5dcc97.PNG)  
![relay_batu](https://user-images.githubusercontent.com/61267430/103164679-f296ad80-4840-11eb-934a-c753e36c4f02.PNG)  
![relay_kediri](https://user-images.githubusercontent.com/61267430/103164680-f32f4400-4840-11eb-8f0b-f3ca4f48873e.PNG)  
![relay_surabaya](https://user-images.githubusercontent.com/61267430/103164682-f3c7da80-4840-11eb-8d53-c14168b35ec8.PNG)  

Kemudian kita lakukan setting konfigurasi dhcp pada client:  
![settingdhcp_klien](https://user-images.githubusercontent.com/61267430/103164706-3b4e6680-4841-11eb-9314-51062846cfa0.PNG)

## Soal
### Nomor 1: Konfigurasi agar dapat mengakses ke luar tanpa menggunakan MASQUERADE di SURABAYA.
Pertama kita setting konfigurasi berikut pada SURABAYA:  
![iptables_surabaya](https://user-images.githubusercontent.com/61267430/103164774-f70f9600-4841-11eb-9231-e913de2f8d7e.PNG)

### Nomor 2: Konfigurasi agar men-drop semua akses SSH dari luar topologi (UML) ke server dengan IP DMZ di SURABAYA.
Kita setting konfigurasi berikut pada SURABAYA:   
![iptables_surabaya](https://user-images.githubusercontent.com/61267430/103164774-f70f9600-4841-11eb-9231-e913de2f8d7e.PNG)  

### Nomor 3: Konfigurasi agar DHCP dan DNS SERVER tidak dapat menerima koneksi ICMP lebih dari 3 dalam satu waktu.
Kita setting pada DHCP dan DNS Server (Mojokerto dan Malang) konfigurasi berikut ini:  
![iptables_malang](https://user-images.githubusercontent.com/61267430/103164868-44d8ce00-4843-11eb-93af-f2643066d4da.PNG)  
![iptables_mojokerto](https://user-images.githubusercontent.com/61267430/103164869-4609fb00-4843-11eb-9023-cf998259df32.PNG)  

### Nomor 4: Konfigurasi pada MALANG agar akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat.
Kita setting konfigurasi pada MALANG seperti berikut:  
![iptables_malang](https://user-images.githubusercontent.com/61267430/103164868-44d8ce00-4843-11eb-93af-f2643066d4da.PNG)  

### Nomor 5: Konfigurasi pada MALANG agar akses dari subnet GRESIK hanya diperbolehkan pada pukul 17.00 - 07.00 setiap harinya.
Kita setting konfigurasi pada MALANG seperti berikut:  
![iptables_malang](https://user-images.githubusercontent.com/61267430/103164868-44d8ce00-4843-11eb-93af-f2643066d4da.PNG)  

### Nomor 6: Konfigurasi pada SURABAYA agar setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada PROBOLINGGO port 80 dan MADIUN port 80.

### Nomor 7: Membuat log semua paket yang telah di-drop pada setiap UML yang memiliki aturan DROP. 
