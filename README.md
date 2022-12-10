# Jarkom Modul 5 F02 2022

### Anggota:

1. [Andymas Narendra Bagaskara](https://github.com/zaibir123) (05111940000192)
2. [Jayanti Totti Andhina](https://github.com/JayantiTA) (5025201037)
3. [Gaudhiwaa Hendrasto](https://github.com/gaudhiwaa) (5025201066)

### (A) Membuat topologi jaringan sesuai dengan rancangan yang diberikan Loid:

![](./media/image19.png)

Keterangan : Eden adalah DNS Server

WISE adalah DHCP Server

Garden dan SSS adalah Web Server

Jumlah Host pada Forger adalah 62 host

Jumlah Host pada Desmond adalah 700 host

Jumlah Host pada Blackbell adalah 255 host

Jumlah Host pada Briar adalah 200 host

### (B) Membuat topologi tersebut menggunakan teknik VLSM setelah melakukan subnetting.

![](./media/image43.png)

| Subnet | Jumlah IP | Netmask |
|--------|-----------|---------|
| A1     | 3         | /29     |
| A2     | 63        | /25     |
| A3     | 701       | /22     |
| A4     | 2         | /30     |
| A5     | 2         | /30     |
| A6     | 256       | /23     |
| A7     | 201       | /24     |
| A8     | 3         | /29     |
| Total  | 1231      | /21     |

Tree:

![](./media/image8.png)

### (C) Melakukan Routing agar setiap perangkat pada jaringan tersebut dapat terhubung.

**Konfigurasi Network Interfaces**

Strix:

![](./media/image20.png)

Westalis:

![](./media/image6.png)

Ostania:

![](./media/image32.png)

Forger, Desmond, Blackbell, Briar:

![](./media/image1.png)

Eden:

![](./media/image41.png)

Wise:

![](./media/image22.png)

Garden:

![](./media/image29.png)

SSS:

![](./media/image24.png)

**Routing**

Strix:

![](./media/image30.png)

Westalis:

![](./media/image45.png)

Ostania:

![](./media/image28.png)

### (D) Memberikan ip pada subnet Forger, Desmond, Blackbell, dan Briar secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

**Eden** sebagai DNS Server:

![](./media/image40.png)

**Wise** sebagai DHCP Server:

![](./media/image18.png)

![](./media/image17.png)

**Ostania** dan **Westalis** sebagai DHCP Relay:

![](./media/image10.png)

**Garden** dan **SSS** sebagai Web Server:

![](./media/image42.png)

#### 1.  Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Strix menggunakan iptables, tetapi Loid tidak ingin menggunakan MASQUERADE.

Script pada **Strix:**

![](./media/image11.png)

#### 2.  Kalian diminta untuk melakukan drop semua TCP dan UDP dari luar Topologi kalian pada server yang merupakan DHCP Server demi menjaga keamanan.

Script pada **Strix:**

![](./media/image14.png)

**Testing:**

Client:

![](./media/image33.png)

#### 3.  Loid meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 2 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

Script pada **Eden** dan **Wise:**

![](./media/image35.png)

**Testing:**

Menuju Eden:

Client1:

![](./media/image9.png)

Client2:

![](./media/image37.png)

Client3:

![](./media/image5.png)

Menuju Wise:

Client1:

![](./media/image34.png)

Client2:

![](./media/image26.png)

Client3:

![](./media/image36.png)

#### 4.  Akses menuju Web Server hanya diperbolehkan disaat jam kerja yaitu Senin sampai Jumat pada pukul 07.00 - 16.00.

Script pada **Garden**:

![](./media/image15.png)

Script pada **SSS**:

![](./media/image3.png)

**Testing:**

Sesuai jam kerja:

Menuju Garden:

![](./media/image44.png)

Menuju SSS:

![](./media/image23.png)

Di luar jam kerja:

Menuju Garden:

![](./media/image21.png)

Menuju SSS:

![](./media/image31.png)

#### 5.  Karena kita memiliki 2 Web Server, Loid ingin Ostania diatur sehingga setiap request dari client yang mengakses Garden dengan port 80 akan didistribusikan secara bergantian pada SSS dan Garden secara berurutan dan request dari client yang mengakses SSS dengan port 443 akan didistribusikan secara bergantian pada Garden dan SSS secara berurutan.

![](./media/image7.png)

**Testing:**

Blackbell menuju Graden dengan port 80

![](./media/image39.png)

![](./media/image4.png)

Briar menuju Garden dengan port 80

![](./media/image12.png)

![](./media/image13.png)

Blackbell menuju SSS dengan port 443

![](./media/image27.png)

![](./media/image25.png)

Briar menuju SSS dengan port 443

![](./media/image2.png)

![](./media/image38.png)

#### 6.  Karena Loid ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.

Script pada **Strix**:

![](./media/image16.png)
