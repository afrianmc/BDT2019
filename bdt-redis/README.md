# Implementasi Redis Cluster

## Arsitektur
Dibawah ini merupakan pembagian Arsitektur dan IP Redis-cluster yang kita gunakan:

No | HostName |    IP    | Keterangan  |
---|----------|----------|-------------|
1  |master    |192.168.33.10 |Master|
2 |slaveredis1|192.168.33.11|Slave 1|
3 |slaveredis2|192.168.33.12|Slave 2|

## Instalasi
- Install package redis yang dibutuhkan pada masing-masing node: 
```
sudo apt-get update 
sudo apt-get install build-essential tcl
sudo apt-get install libjemalloc-dev
```
- Kemudian install redis pada masing-masing node:
```
curl -O http://download.redis.io/redis-stable.tar.gz
tar xzvf redis-stable.tar.gz
cd redis-stable
make
make test
sudo make install
```

## Konfigurasi
- Lakukan konfigurasi untuk firewall di masing-masing node:
```
sudo ufw allow 6379 #Port Redis
sudo ufw allow 26379 #Sentinel
sudo ufw allow from 192.168.33.10 #Master
sudo ufw allow from 192.168.33.11 #Slave1
sudo ufw allow from 192.168.33.12 #Slave2
```
- Setelah melakukan instalasi maka akan terdapat file ```redis.conf``` dan ```sentinel.conf```. Lakukanlah konfigurasi pada file tersebut pada masing-masing node

- Selanjutnya ubahlah konfigurasi file redis.conf seperti berikut:
```
# Untuk Master
protected-mode no
port 6379
dir .
logfile "/home/redis-stable/redig.log" #output log
```
```
# Untuk Slave1 dan Slave2
protected-mode no
port 6379
dir .
slaveof 192.168.33.10 6379
logfile "/home/redis-stable/redig.log" #output log
```
Pada file redis.conf yang slave terdapat ```slaveof 192.168.33.10 6379``` yang mana berarti slave ini dari master 192.168.33.10 (node1).

- kemudian ubahlah konfigurasi file sentinel.conf seperti berikut pada masing-masing node:
```
protected-mode no
port 26379
logfile "/home/redis-stable/sentinel.log"
sentinel monitor mymaster 192.168.33.10 6379 2
sentinel down-after-milliseconds mymaster 5000
sentinel failover-timeout mymaster 10000
```

## Menjalankan Redis
- Untuk menjalankan redis kita perlu menjalankan folder ```src``` :
```
src/redis-server redis.conf &
src/redis-server sentinel.conf --sentinel &
```
- Kemudian untuk melakukan cek status redis dengan sintaks:
```
ps -ef | grep redis
```
maka akan muncul gambar seperti berikut:


- Selanjutnya lakukan ping ke masing-masing node dengan sintak seperti berikut:
```
redis-cli -h [ip address] ping #masukkan ip address masing-masing node
```
![ss]
redis telah berhasil jalan tanpa adanya error

- Mengecek log dari master dengan sintaks seperti berikut:
```
cat redis.conf
```
- Maka akan muncul gambar seperti berikut:

![ss]


- Mengecek info replikasi dari masing-masing node dengan sintaks:
```
redis-cli
```
Master

![ss]

Slave1

![ss]

slave2

![ss]

masing-masing node telah terreplikasi dengan baik 

## Testing
- Pada kasus ini saya akan mematikan master redis dengan sintaks:
```
redis-cli -p 6379 DEBUG sleep 30
```
![ss]

- jika master berhasil dimatikan, maka salah satu slave akan menjadi master.

![ss]
![ss]

pada kasus ini slave2 menjadi master dan redis tetap berjalan setelah master dimatikan.

## Referensi
https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-redis-on-ubuntu-16-04




