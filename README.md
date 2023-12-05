# Jarkom-Modul-4-E18-2023

Anggota Kelompok ''E18'' 
| Nama                      | NRP        |
|---------------------------|------------|
| Hanun Shaka Puspa         | 5025211051 |
| Cholid Junoto             | 5025201038 |

## GNS3 - CIDR
Subnetting dan routing pada GNS3 dilakukan dengan metode CIDR dan dikerjakan oleh nrp 051.

### Topologi dan Subnet Kecil
Pemberian label pada subnet kecil adalah sebagai berikut.<br/>
<img src="./media/GNS Subnet CIDR.png" width="750px"/><br/>

### Subnetting CIDR
Dilakukan penggabungan subnet-subnet kecil dari subnet A hingga subnet I dengan langkah-langkah yang ada pada [CIDR Subnet Steps](./media/CIDR%20Subnet%20Steps.csv). Sehingga didapatkan netmask subnet terbesar /14 dan pembagian sebagai berikut.<br/>
<img src="./media/GNS Subnetted CIDR.png" width="750px"/><br/>
Kemudian dengan prefix ip `192.215`, NID subnet I1 akan menjadi `192.215.0.0/14`. Kemudian dilakukan pembagian NID pada subnet-subnet yang lebih kecil.<br/>
<img src="./media/CIDR NID Tree.png" width="750px"/><br/>
Hasil pembagian menjadi seperti berikut<br/>
<table>
  <thead>
    <tr>
      <th>Subnet</th>
      <th>Network ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A1</td>
      <td>192.215.192.0</td>
    </tr>
    <tr>
      <td>A2</td>
      <td>192.215.221.0</td>
    </tr>
    <tr>
      <td>A3</td>
      <td>192.215.48.0</td>
    </tr>
    <tr>
      <td>A4</td>
      <td>192.215.32.0</td>
    </tr>
    <tr>
      <td>A5</td>
      <td>192.215.37.0</td>
    </tr>
    <tr>
      <td>A6</td>
      <td>192.215.42.0</td>
    </tr>
    <tr>
      <td>A7</td>
      <td>192.215.64.0</td>
    </tr>
    <tr>
      <td>A8</td>
      <td>192.215.8.0</td>
    </tr>
    <tr>
      <td>A9</td>
      <td>192.215.5.0</td>
    </tr>
    <tr>
      <td>A10</td>
      <td>192.215.4.0</td>
    </tr>
    <tr>
      <td>A11</td>
      <td>192.215.0.0</td>
    </tr>
    <tr>
      <td>A12</td>
      <td>192.215.1.0</td>
    </tr>
    <tr>
      <td>A13</td>
      <td>192.215.16.0</td>
    </tr>
    <tr>
      <td>A14</td>
      <td>192.215.168.0</td>
    </tr>
    <tr>
      <td>A15</td>
      <td>192.215.144.0</td>
    </tr>
    <tr>
      <td>A16</td>
      <td>192.215.138.0</td>
    </tr>
    <tr>
      <td>A17</td>
      <td>192.215.131.0</td>
    </tr>
    <tr>
      <td>A18</td>
      <td>192.215.128.0</td>
    </tr>
    <tr>
      <td>A19</td>
      <td>192.215.132.0</td>
    </tr>
    <tr>
      <td>A20</td>
      <td>192.215.136.0</td>
    </tr>
    <tr>
      <td>A21</td>
      <td>192.215.160.0</td>
    </tr>
  </tbody>
</table>

### Konfigurasi NID Router
Pada GNS3, dilakukan konfigurasi untuk setiap router di dalam topologi secara manual.

#### Aura
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

#A14 Frieren
auto eth1
iface eth1 inet static
address 192.215.168.1
netmask 255.255.255.252

#A7 Eisen
auto eth2
iface eth2 inet static
address 192.215.64.1
netmask 255.255.255.252

#A2 Denken
auto eth3
iface eth3 inet static
address 192.215.221.1
netmask 255.255.255.252
```

#### Frieren
```
auto lo
iface lo inet loopback

#A14 Aura - Frieren
auto eth0
iface eth0 inet static
address 192.215.168.2
netmask 255.255.255.252
gateway 192.215.168.1

#A21 LakeKorridor
auto eth1
iface eth1 inet static
address 192.215.160.1
netmask 255.255.255.224

#A15 Flamme - Frieren
auto eth2
iface eth2 inet static
address 192.215.144.1
netmask 255.255.255.252
```

#### Eisen
```
auto lo
iface lo inet loopback

#A7 Aura - Eisen
auto eth0
iface eth0 inet static
address 192.215.64.2
netmask 255.255.255.252
gateway 192.215.64.1

#A13 Switch1
auto eth1
iface eth1 inet static
address 192.215.16.1
netmask 255.255.255.248

#A8 Linie
auto eth2
iface eth2 inet static
address 192.215.8.1
netmask 255.255.255.252

#A6 Lugner
auto eth3
iface eth3 inet static
address 192.215.42.1
netmask 255.255.255.252
 
#A3 Switch0
auto eth4
iface eth4 inet static
address 192.215.48.1
netmask 255.255.255.248
```

#### Denken
```
auto lo
iface lo inet loopback
 
#A2 Aura
auto eth0
iface eth0 inet static
address 192.215.221.2
netmask 255.255.255.252
gateway 192.215.221.1

#A1 Switch2
auto eth1
iface eth1 inet static
address 192.215.192.1
netmask 255.255.255.0
```

#### Flamme
```
auto lo
iface lo inet loopback

#A15 Frieren
auto eth0
iface eth0 inet static
address 192.215.144.2
netmask 255.255.255.252
gateway 192.215.144.1

#A17 Fern
auto eth1
iface eth1 inet static
address 192.215.131.1
netmask 255.255.255.252

#A19 Switch5
auto eth2
iface eth2 inet static
address 192.215.132.1
netmask 255.255.252.0

#A16 Himmel
auto eth3
iface eth3 inet static
address 192.215.138.1
netmask 255.255.255.252
```

#### Fern
```
auto lo
iface lo inet loopback

#A17 Flamme
auto eth0
iface eth0 inet static
address 192.215.131.2
netmask 255.255.255.252
gateway 192.215.131.1

#A18 Switch4
auto eth1
iface eth1 inet static
address 192.215.128.1
netmask 255.255.248.0
```

#### Himmel
```
auto lo
iface lo inet loopback

#A16 Flamme
auto eth0
iface eth0 inet static
address 192.215.138.2
netmask 255.255.255.252
gateway 192.215.138.1

#A20 Switch6
auto eth1
iface eth1 inet static
address 192.215.136.1
netmask 255.255.255.248
```

#### Lugner
```
auto lo
iface lo inet loopback

#A6 Eisen
auto eth0
iface eth0 inet static
address 192.215.42.2
netmask 255.255.255.252
gateway 192.215.42.1

#A5 Switch9
auto eth1
iface eth1 inet static
address 192.215.37.1
netmask 255.255.252.0

#A4 Switch10
auto eth2
iface eth2 inet static
address 192.215.32.1
netmask 255.255.252.0
```

#### Linie
```
auto lo
iface lo inet loopback

#A8 Eisen
auto eth0
iface eth0 inet static
address 192.215.8.2
netmask 255.255.255.252
gateway 192.215.8.1

#A10 Lawine
auto eth1
iface eth1 inet static
address 192.215.4.1
netmask 255.255.255.252

#A9 Switch11
auto eth2
iface eth2 inet static
address 192.215.5.1
netmask 255.255.254.0
```

#### Lawine
```
auto lo
iface lo inet loopback

#A10 Linie
auto eth0
iface eth0 inet static
address 192.215.4.2
netmask 255.255.255.252
gateway 192.215.4.1

#A11 Switch7
auto eth1
iface eth1 inet static
address 192.215.0.1
netmask 255.255.255.192
```

#### Heiter
```
auto lo
iface lo inet loopback

#A11 Lawine
auto eth0
iface eth0 inet static
address 192.215.0.2
netmask 255.255.255.192
gateway 192.215.0.1

#A12 Switch8
auto eth1
iface eth1 inet static
address 192.215.1.1
netmask 255.255.252.0
```

#### LakeKorridor
```
#A21 Frieren
auto eth0
iface eth0 inet static
address 192.215.160.2
netmask 255.255.255.224
gateway 192.215.160.1
```

#### LaubHills
```
#A18 Fern
auto eth0
iface eth0 inet static
address 192.215.128.2
netmask 255.255.248.0
gateway 192.215.128.1
```

#### AppetitRegion
```
#A18 Fern
auto eth0
iface eth0 inet static
address 192.215.128.3
netmask 255.255.248.0
gateway 192.215.128.1
```

#### RohrRoad
```
#A19 Flamme
auto eth0
iface eth0 inet static
address 192.215.132.2
netmask 255.255.252.0
gateway 192.215.132.1
```

#### SchwerMountains
```
#A20 Himmel
auto eth0
iface eth0 inet static
address 192.215.136.2
netmask 255.255.255.248
gateway 192.215.136.1
```

#### Richter
```
#A13 Eisen
auto eth0
iface eth0 inet static
address 192.215.16.2
netmask 255.255.252.248
gateway 192.215.16.1
```

#### Revolte
```
#A13 Eisen
auto eth0
iface eth0 inet static
address 192.215.16.3
netmask 255.255.252.248
gateway 192.215.16.1
```

#### BredtRegion
```
#A11 Lawine
auto eth0
iface eth0 inet static
address 192.215.0.2
netmask 255.255.255.192
gateway 192.215.0.1
```

#### Sein
```
#A12 Heiter
auto eth0
iface eth0 inet static
address 192.215.1.2
netmask 255.255.252.0
gateway 192.215.1.1
```

#### RiegelCanyon
```
#A12 Heiter
auto eth0
iface eth0 inet static
address 192.215.1.3
netmask 255.255.252.0
gateway 192.215.1.1
```

#### GranzChannel
```
#A9 Linie
auto eth0
iface eth0 inet static
address 192.215.5.2
netmask 255.255.254.0
gateway 192.215.5.1
```

#### GrobeForest
```
#A5 Lugner
auto eth0
iface eth0 inet static
address 192.215.37.2
netmask 255.255.252.0
gateway 192.215.37.1
```

#### TurkRegion
```
#A4 Lugner
auto eth0
iface eth0 inet static
address 192.215.32.2
netmask 255.255.252.0
gateway 192.215.32.1
```

#### Stark
```
#A3 Eisen
auto eth0
iface eth0 inet static
address 192.215.48.2
netmask 255.255.255.248
gateway 192.215.48.1
```

#### WilleRegion
```
#A1 Denken
auto eth0
iface eth0 inet static
address 192.215.192.2
netmask 255.255.255.0
gateway 192.215.192.1
```

#### RoyalCapital
```
#A1 Denken
auto eth0
iface eth0 inet static
address 192.215.192.3
netmask 255.255.255.0
gateway 192.215.192.1
```

### Routing CIDR pada GNS3
Untuk melakukan routing di GNS3, dipanggil command berikut pada router.
```
route add -net <NID subnet> netmask <netmask> gw <IP gateway>
```
Routing dilakukan pada setiap router yang ada pada topologi GNS3. Command tersebut mendaftarkan NID subnet ke router di atasnya dengan gateway NID router yang menghubungkan subnet tersebut dengan router di atasnya.

#### Aura
```
route add -net 192.215.160.0 netmask 255.255.255.224 gw 192.215.168.2
route add -net 192.215.144.0 netmask 255.255.255.252 gw 192.215.168.2
route add -net 192.215.138.0 netmask 255.255.255.252 gw 192.215.168.2
route add -net 192.215.131.0 netmask 255.255.255.252 gw 192.215.168.2
route add -net 192.215.128.0 netmask 255.255.248.0 gw 192.215.168.2
route add -net 192.215.132.0 netmask 255.255.252.0 gw 192.215.168.2
route add -net 192.215.136.0 netmask 255.255.255.248 gw 192.215.168.2

route add -net 192.215.192.0 netmask 255.255.255.0 gw 192.215.221.2

route add -net 192.215.48.0 netmask 255.255.255.248 gw 192.215.64.2
route add -net 192.215.32.0 netmask 255.255.252.0 gw 192.215.64.2
route add -net 192.215.37.0 netmask 255.255.255.0 gw 192.215.64.2
route add -net 192.215.42.0 netmask 255.255.255.252 gw 192.215.64.2
route add -net 192.215.8.0 netmask 255.255.255.252 gw 192.215.64.2
route add -net 192.215.5.0 netmask 255.255.254.0 gw 192.215.64.2
route add -net 192.215.4.0 netmask 255.255.255.252 gw 192.215.64.2
route add -net 192.215.0.0 netmask 255.255.255.192 gw 192.215.64.2
route add -net 192.215.1.0 netmask 255.255.252.0 gw 192.215.64.2
route add -net 192.215.16.0 netmask 255.255.255.248 gw 192.215.64.2
```

#### Frieren
```
route add -net 192.215.138.0 netmask 255.255.255.252 gw 192.215.144.2
route add -net 192.215.131.0 netmask 255.255.255.252 gw 192.215.144.2
route add -net 192.215.128.0 netmask 255.255.248.0 gw 192.215.144.2
route add -net 192.215.132.0 netmask 255.255.252.0 gw 192.215.144.2
route add -net 192.215.136.0 netmask 255.255.255.248 gw 192.215.144.2
```

#### Eisen
```
route add -net 192.215.32.0 netmask 255.255.252.0 gw 192.215.42.2
route add -net 192.215.37.0 netmask 255.255.252.0 gw 192.215.42.2

route add -net 192.215.5.0 netmask 255.255.254.0 gw 192.215.8.2
route add -net 192.215.4.0 netmask 255.255.255.252 gw 192.215.8.2
route add -net 192.215.0.0 netmask 255.255.255.192 gw 192.215.8.2
route add -net 192.215.1.0 netmask 255.255.252.0 gw 192.215.8.2
```

#### Denken
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.215.221.1
```

#### Fern
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.215.144.2
```

#### Flamme
```
route add -net 192.215.128.0 netmask 255.255.248.0 gw 192.215.131.2
route add -net 192.215.136.0 netmask 255.255.255.248 gw 192.215.138.2
```

#### Himmel
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.215.144.2
```

#### Linie
```
route add -net 192.215.0.0 netmask 255.255.255.192 gw 192.215.4.2
route add -net 192.215.1.0 netmask 255.255.252.0 gw 192.215.4.2
```

#### Lugner
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.215.64.2
```

#### Lawine
```
route add -net 192.215.1.0 netmask 255.255.252.0 gw 192.215.0.2
```

#### Heiter
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.215.4.2
```

## CPT - VLSM

## Kendala Pengerjaan
Sulit mencari resource belajar untuk melakukan subnetting dan routing pada GNS3. Masih tidak yakin akan efisiensi pembagian NID pada GNS3 - CIDR.
