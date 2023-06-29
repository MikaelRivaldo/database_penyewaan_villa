# database_penyewaan_villa

### KELOMPOK 6
```
1.Hasbi Assidiki (312210448)
2.Mikael Rivaldo (312210378)
3.Akram Satya (312210461)
4.Yudha Eka Perdana (312210362)
```


## Untuk ERD Database Penyewaan Villa seperti gambar di bawah ini :

![ER-D Penyewaan Villa](https://github.com/MikaelRivaldo/database_penyewaan_villa/assets/115770247/d170407b-a07d-4955-b11d-828113f7f143)

`Penejelasan`

## Disini kami membuat erd tentang database penyewaan villa yang berisi 4 entitas yaitu : 

1.Villa

2.Pembayaran

3.Pengunjung

4.reservasi

Yang dimana setiap entitas mempunyai atribut seperti pada diagram diatas

## DDL Script
```sql
CREATE TABLE Villa (
  id_villa INT PRIMARY KEY,
  tempat VARCHAR(255),
  tipe VARCHAR(255),
  harga DECIMAL(10, 2)
);
```
```sql
CREATE TABLE Reservasi (
  id_reservasi INT PRIMARY KEY,
  id_pengunjung INT,
  id_villa INT,
  tgl_masuk DATE,
  tgl_keluar DATE,
  FOREIGN KEY (id_pengunjung) REFERENCES Pengunjung(id_pengunjung),
  FOREIGN KEY (id_villa) REFERENCES Villa(id_villa)
);
```
```sql
CREATE TABLE Pengunjung (
  id_pengunjung INT PRIMARY KEY,
  nama VARCHAR(255),
  alamat VARCHAR(255),
  email VARCHAR(255),
  no_hp VARCHAR(20)
);
```
```sql
CREATE TABLE Pembayaran (
  id_pembayaran INT PRIMARY KEY,
  id_reservasi INT,
  tipe VARCHAR(255),
  jumlah DECIMAL(10, 2),
  FOREIGN KEY (id_reservasi) REFERENCES Reservasi(id_reservasi)
);
```

### SQL CRUD Sricpt
```sql
insert into villa (id_villa,tempat,tipe,harga) values
    -> ('1','Puncak Bogor','3 kamar + kolam renang','5000000'),
    -> ('2','Cisarua-Bogor','2 kamar + kolam renang','4000000'),
    -> ('3','Cianjur','3 kamar tanpa kolam renang','3500000'),
    -> ('4','Bandung','2 kamar + kolam renang','4500000');
```
```sql
insert into pengunjung (id_pengunjung,nama,alamat,email,no_hp) values
    -> ('1','Hasbi Assidiki','Cibarusah','assidikihasbi23@gmail.com','089876542345'),
    -> ('2','Mikael Rivaldo','Cikarang','mikael89@gmail.com','087890654231'),
    -> ('3','Yudha Eka','Cikarang','yudha56@gmail.com','085689073456'),
    -> ('4','Akram Satya','Cikarang','akram85@gmail.com','087890985675');
```
```sql
insert into reservasi (id_reservasi,id_pengunjung,id_villa,tgl_masuk,tgl_keluar) values
    -> ('1','1','1','2023-06-24','2023-06-26'),
    -> ('2','2','2','2023-06-25','2023-06-27'),
    -> ('3','3','3','2023-06-26','2023-06-28'),
    -> ('4','4','4','2023-06-27','2023-06-29');
```
```sql
insert into pembayaran (id_pembayaran,id_reservasi,tipe,jumlah) values
    -> ('1','1','TUNAI','5000000'),
    -> ('2','2','NON TUNAI','4000000'),
    -> ('3','3','TUNAI','3500000'),
    -> ('4','4','NON TUNAI','4500000');
```
```sql
update villa set harga = '4000000' where id_villa = 2;
```
```sql
 insert into pengunjung (id_pengunjung,nama,alamat,email,no_hp) values
    -> ('5','Udin','Cicaheum','udin212@gmail.com','087678904354');
```
```sql
delete from pengunjung WHERE id_pengunjung = '5';
```
### SQL JOIN Script
``` sql
SELECT R.id_reservasi, R.id_pengunjung, V.tempat, V.tipe, V.harga
FROM Reservasi R
INNER JOIN Villa V ON R.id_villa = V.id_villa;
```
```sql
SELECT R.id_reservasi, P.nama, V.tempat, V.tipe, V.harga
FROM Reservasi R
INNER JOIN Pengunjung P ON R.id_pengunjung = P.id_pengunjung
INNER JOIN Villa V ON R.id_villa = V.id_villa;
```
```sql
SELECT R.id_reservasi, P.tipe, P.jumlah
FROM Reservasi R
LEFT JOIN Pembayaran P ON R.id_reservasi = P.id_reservasi;
```

# LAPORAN

Database Penyewaan Penginapan Villa  
• Mengelola data Villa dan Tipenya  
• Mengelola data Tarif kunjungan  
• Mengelola data Pengunjung  
• Transaksi Penyewaan dan Pembayaran  
• Laporan Transaksi  

Dari perintah diatas maka kelompok kami membuat ER-D dengan 4 entitas yaitu villa,pengunjung,reservasi,dan pembayar.
Setiap entitas yang kami pilih memiliki beberapa atribut,yaitu :
- Villa : Pada entitas villa ini kami berikan atribut untuk mengetahui lokasi villa,harga villa,dan tipe villa tersebut.Dan kami memilih 4 atribut yaitu : id_villa,tempat,tipe,harga.
- pengunjung : Pada entitas ini kami berikan atribut untuk mengetahui identitas pengunjung,oleh karenanya kami berikan 5 atribut yaitu : id_pengunjung,nama,alamat,email,no_hp.
- reservasi : Pada entitas ini akan diperlihatkan kapan pengunjung masuk dan keluar,dan pada entitas ini menghubungkan antara entitas villa dan pengunjung,oleh karenanya kami memilih 5 atribut yaitu : id_villla,id_pengunjung,id_reservasi,tgl_masuk,tgl_keluar.
- Pembayaran : Pada entitas akan diperlihatkan tipe pembayaran pengunjung yaitu antara tunai dan non tunai,dikarenakan pada entitas reservasi sudah dimasukan id_pengunjung dan id_villa maka disini saya hanya memasukan id_reservasi untuk menghubungkan dengan tabel villa dan pengunjung,dan kami memilih 4 atribut yaitu : id_reservasi,id_pembayaran,tipe,jumlah.

Dari ER-Diagram dan Script DDL diatas,kami akan mengimplementasikan pada langkah-langkah pembuatan database penyewaan villa
### 1. Memasukan values untuk setiap table
- Tabel villa
```sql
insert into villa (id_villa,tempat,tipe,harga) values
    -> ('1','Puncak Bogor','3 kamar + kolam renang','5000000'),
    -> ('2','Cisarua-Bogor','2 kamar + kolam renang','4000000'),
    -> ('3','Cianjur','3 kamar tanpa kolam renang','3500000'),
    -> ('4','Bandung','2 kamar + kolam renang','4500000');
```
  - Output  
  ![villa](https://github.com/HasbiAssidiki/Lab2py/assets/115614317/edb9bf0d-b53c-4418-b106-c50ce42b482b)   

- Tabel Pengunjung
```sql
insert into pengunjung (id_pengunjung,nama,alamat,email,no_hp) values
    -> ('1','Hasbi Assidiki','Cibarusah','assidikihasbi23@gmail.com','089876542345'),
    -> ('2','Mikael Rivaldo','Cikarang','mikael89@gmail.com','087890654231'),
    -> ('3','Yudha Eka','Cikarang','yudha56@gmail.com','085689073456'),
    -> ('4','Akram Satya','Cikarang','akram85@gmail.com','087890985675');
```
  - Output  
  ![pengunjung](https://github.com/HasbiAssidiki/Lab2py/assets/115614317/35153755-553b-41a4-96bf-343b7a45a919)  

- Tabel Reservasi
```sql
insert into reservasi (id_reservasi,id_pengunjung,id_villa,tgl_masuk,tgl_keluar) values
    -> ('1','1','1','2023-06-24','2023-06-26'),
    -> ('2','2','2','2023-06-25','2023-06-27'),
    -> ('3','3','3','2023-06-26','2023-06-28'),
    -> ('4','4','4','2023-06-27','2023-06-29');
```
  - Output  
  ![reservasi](https://github.com/HasbiAssidiki/Lab2py/assets/115614317/24ca240a-715d-46dc-b80d-447d42a835f0)  

- Tabel Pembayaran
```sql
insert into pembayaran (id_pembayaran,id_reservasi,tipe,jumlah) values
    -> ('1','1','TUNAI','5000000'),
    -> ('2','2','NON TUNAI','4000000'),
    -> ('3','3','TUNAI','3500000'),
    -> ('4','4','NON TUNAI','4500000');
```
  - Output  
  ![pembayaran](https://github.com/HasbiAssidiki/Lab2py/assets/115614317/9bd3d8bf-a8d1-4dc3-a2ce-e831bca7648d)  

### 2.Update + DELETE Table
- Menambahkan values
```sql
insert into pengunjung (id_pengunjung,nama,alamat,email,no_hp) values
    -> ('5','Udin','Cicaheum','udin212@gmail.com','087678904354');
```
  - Output  
![+pengunjung](https://github.com/HasbiAssidiki/Lab2py/assets/115614317/de256014-d4fd-437d-8df6-3c1f9e2ae6c1)   
- Mengganti values
```sql
update villa set harga = '4000000' where id_villa = 2;
```
  - Output  
![update villa](https://github.com/HasbiAssidiki/Lab2py/assets/115614317/5c9e4eea-6c18-49cc-a7e7-e9b795b75a2b)  
- Delete
```sql
delete from pengunjung WHERE id_pengunjung = '5
```

### 3. JOIN Table
- INNER JOIN antara tabel Reservasi, Pengunjung, dan Villa berdasarkan id_pengunjung dan id_villa:
```sql
SELECT R.id_reservasi, P.nama, V.tempat, V.tipe, V.harga
FROM Reservasi R
INNER JOIN Pengunjung P ON R.id_pengunjung = P.id_pengunjung
INNER JOIN Villa V ON R.id_villa = V.id_villa;
```
  - Output  
![INNER JOIN 2table](https://github.com/HasbiAssidiki/Lab2py/assets/115614317/b2f6016c-2d77-4fce-8983-dd0b6c5a3109)  
- LEFT JOIN antara tabel Reservasi dan Pembayaran berdasarkan id_reservasi:
```sql
SELECT R.id_reservasi, P.tipe, P.jumlah
FROM Reservasi R
LEFT JOIN Pembayaran P ON R.id_reservasi = P.id_reservasi;
```
  - Output  
![LEFT JOIN](https://github.com/HasbiAssidiki/Lab2py/assets/115614317/60ab56fe-2586-44ca-a5c3-ad070269b15c)   
- INNER JOIN antara tabel Reservasi, Villa, Pengunjung, dan Pembayaran berdasarkan id_reservasi, id_villa, dan id_pengunjung:
```sql
SELECT R.id_reservasi, V.tempat, P.nama, PB.tipe, PB.jumlah
FROM Reservasi R
INNER JOIN Villa V ON R.id_villa = V.id_villa
INNER JOIN Pengunjung P ON R.id_pengunjung = P.id_pengunjung
INNER JOIN Pembayaran PB ON R.id_reservasi = PB.id_reservasi;
```
  - Output  
![INNER JOIN 3table](https://github.com/HasbiAssidiki/Lab2py/assets/115614317/097d84ed-946e-4a1c-bc26-57085ae886c5)   
## FINISH
