# Jarkom-Modul-3-D26-2023

Laporan Resmi Praktikum Jaringan Komputer Modul 3

* Fathan Abi Karami (5025211156)
* Alya Putri Salma (5025211174)

# Soal 0
Perjalanan selanjutnya akan menggunakan peta berikut:

![](./img/0_topologi.png)

dengan ketentuan sebagai berikut:

![](./img/0_tabel_1.png)
![](./img/0_tabel_2.png)

Setelah mengalahkan Demon King, perjalanan berlanjut. Kali ini, kalian diminta untuk melakukan register domain berupa riegel.canyon.yyy.com untuk worker Laravel dan granz.channel.yyy.com untuk worker PHP (0) mengarah pada worker yang memiliki IP [prefix IP].x.1.

## Pengerjaan

### Configure Network Adapter

Buat topologi seperti pada gambar. lalu configure network tiap node

Aura:
```txt
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.204.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.204.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.204.3.250
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 192.204.4.250
	netmask 255.255.255.0
```

Himmel:
```txt
auto eth0
iface eth0 inet static
	address 192.204.1.2
	netmask 255.255.255.0
	gateway 192.204.1.1
```

Heither:
```txt
auto eth0
iface eth0 inet static
	address 192.204.1.3
	netmask 255.255.255.0
	gateway 192.204.1.1
```

Denken:
```txt
auto eth0
iface eth0 inet static
	address 192.204.2.2
	netmask 255.255.255.0
	gateway 192.204.2.1
```

Eisen:
```txt
auto eth0
iface eth0 inet static
	address 192.204.2.3
	netmask 255.255.255.0
	gateway 192.204.2.1
```

Frieren:
```txt
auto eth0
iface eth0 inet static
	address 192.204.4.1
	netmask 255.255.255.0
	gateway 192.204.4.250
```

Flamme:
```txt
auto eth0
iface eth0 inet static
	address 192.204.4.2
	netmask 255.255.255.0
	gateway 192.204.4.250
```

Fern:
```txt
auto eth0
iface eth0 inet static
	address 192.204.4.3
	netmask 255.255.255.0
	gateway 192.204.4.250
```

Lawine:
```txt
auto eth0
iface eth0 inet static
	address 192.204.3.1
	netmask 255.255.255.0
	gateway 192.204.3.250
```

Linie:
```txt
auto eth0
iface eth0 inet static
	address 192.204.3.2
	netmask 255.255.255.0
	gateway 192.204.3.250
```

Lugner:
```txt
auto eth0
iface eth0 inet static
	address 192.204.3.3
	netmask 255.255.255.0
	gateway 192.204.3.250
```

### Configure Aura
pada router buat script start.sh di root untuk membuat iptables dan update

![](./img/0_aura_start.png)

cari IP DNS menngunakan
```bash
cat /etc/resolv.conf
```

didapat

```txt
nameserver 192.168.122.1
```

### configure DNS pada Heither

buat script start.sh di root untuk configure DNS pada heither dan jalankan apt-get update

![](./img/0_heither_start.png)

kemudian buat script configBind.sh untuk config DNS untuk granz.channel.d26.com dan riegel.canyon.d26.com. 

![](./img/0_heither_confBind.png)

pertama script akan menginstall package bind9. kemudian akan men-copy named.conf.local ke /etc/bind/ , yang berisikan:

![](./img/0_heither_namedconflocal.png)

kemudian copy named.conf.options ke /etc/bind/ , yang berisikan:

![](./img/0_heither_namedconfoptions1.png)
![](./img/0_heither_namedconfoptions2.png)

kemudian buat directory granz dan riegel di /etc/bind/

kemudian copy riegel.canyon.d26.com ke /etc/bind/riegel , yang berisikan konfigurasi dns riegel.canyon.d26.com:

![](./img/0_heither_riegel.png)

kemudian copy granz.channel.d26.com ke /etc/bind/granz , yang berisikan konfigurasi dns granz.channel.d26.com:

![](./img/0_heither_granz.png)

kemudian restart service bind9

# Soal 1
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.

Kemudian, karena masih banyak spell yang harus dikumpulkan, bantulah para petualang untuk memenuhi kriteria berikut:
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.

## Pengerjaan
pada tiap node client, configure network menjadi:

Revolte:
```txt
auto eth0
iface eth0 inet dhcp
```

Richter:
```txt
auto eth0
iface eth0 inet dhcp
```

Sein:
```txt
auto eth0
iface eth0 inet dhcp
```

Stark:
```txt
auto eth0
iface eth0 inet dhcp
```

# Soal 2, 3, 4, 5
* Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80. 
* Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168. 
* Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut 
* Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit

## Pengerjaan
### Config DHCP Server (Himmel)
buat script configDhcp.sh untuk mengkonfigurasi DHCP Server di Himmel. Script berisikan:

![](./img/2_himmel_configDhcp.png)

pertama script akan menginstall package isc-dhcp-server. kemudian akan men-copy isc-dhcp-server yang berisikan config interface dhcp server ke /etc/default/ , yang berisikan:

![](./img/2_himmel_iscdhcpserver.png)

isc-dhcp-server meng-config INTERFACESv4 = eht0. kemudian akan men-copy dhcpd.conf yang berisikan config dhcp , ke /etc/dhcp/. 

![](./img/2_himmel_dhcpdconf1.png)
![](./img/2_himmel_dhcpdconf2.png)
![](./img/2_himmel_dhcpdconf3.png)

pada dhcp.conf terdapat config untuk subnet 192.204.3.0 yang mengatur client yang melalui switch3 dan subnet 192.204.4.0 yang mengatur client yang melalui switch4. range ip diatur pada range. DNS diatur pada option domain-name-servers. Lama waktu DHCP server meminjamkan alamat IP kepada Client diatur pada default-lease-time (dalam satuan second). waktu maksimal dialokasikan untuk peminjaman alamat IP diatur pada max-lease-time (dalam satuan second). sesuaikan default-lease-time tiap subnet dengan ketentuan di soal. kemudian restart service isc-dhcp-server.

### Configure DHCP-Relay (Aura)
Atur node Aura sebagai DHCP Relay. pada node Aura buat script configDhcpRelay.sh yang berisikan:

![](./img/2_aura_configDhcpRelay.png)

pertama install package isc-dhcp-relay. kemudain copy isc-dhcp-relay yang berisikan konfigurasi dhcp relay ke /etc/default/ :

![](./img/2_aura_iscdhcprelay.png)

SERVERS di set ke IP DHCP Server (Himmel). INTERFACES di set ke eth1 eth2 eth3 eth4. kemudian copy sysctl.conf ke /etc/.

![](./img/2_aura_sysctlconf.png)

kemudian restart service isc-dhcp-relay.

saat dijalankankan: 

![](./img/2_aura_configdhcprelay_run.png)

set forward ke 192.204.1.2 (IP DHCP Server himmel)

set Listen DHCP Relay ke eth1 eth2 eth3 eht4

skip option dhcp relay daemon

## Testing
### DHCP 
Revolte:

![](./img/2_revolte_test_dhcp.png)

Richter:

![](./img/2_richter_test_dhcp.png)

Sein:

![](./img/2_sein_test_dhcp.png)

Stark:

![](./img/2_stark_test_dhcp.png)


### DNS
ping google.com, granz.channel.d26.com, riegel.canyon.d26.com:

![](./img/2_revolte_ping.png)

# Soal 6
# Soal 7
# Soal 8
# Soal 9
# Soal 10
# Soal 11
# Soal 12
# Soal 13
# Soal 14
# Soal 15
# Soal 16
# Soal 17
# Soal 18
# Soal 19
# Soal 20
