# database_penyewaan_villa

### KELOMPOK 6
```
1.Hasbi Assidiki (312210448)
2.Mikael Rivaldo (312210378)
3.Akram Satya (312210461)
4.Yudha Eka Perdana (312210362)
```


Database Penyewaan Penginapan Villa

• Mengelola data Villa dan Tipenya

• Mengelola data Tarif kunjungan

• Mengelola data Pengunjung

• Transaksi Penyewaan dan Pembayaran

• Laporan Transaksi

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

