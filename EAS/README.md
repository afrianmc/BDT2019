# Wordpress Menggunakan MySQL Cluster dan Redis
  
  Implementasi MySQL Cluster dan NoSQL Redis menggunakan 4 node.
  
# Model Arsitektur
  
  Pada Desain MySQL Cluster dan Redis kali ini, saya menggunakan 4 node dengan pembagian sebagai berikut :
  
No | HostName |    IP    | Keterangan  |
---|----------|----------|-------------|
1  |db-cluster1|192.168.33.11|Sebagai Node Manager dan Redis|
2 |db-cluster2|192.168.33.12|Sebagai Server1 dan Node1 dan Redis|
3 |db-cluster3|192.168.33.13|Sebagai Server2 dan Node2 dan Redis|
4 |db-cluster4|192.168.33.14|Sebagai Load Balance(ProxySQL)|

# Installasi `apache`

  - Proses installasi mysql-cluster sama dengan tugas sebelumnya yaitu, <a href="https://github.com/afrianmc/mysql-cluster">mysql-cluster</a>
  
# Installasi `wordpress`

  - Proses installasi wordpress sama dengan tugas sebelumnya yaitu, <a href="https://github.com/afrianmc/BDT2019/tree/master/ETS">ETS</a>
  
# Installasi `Redis`

  - Proses installasi redis sama dengan tugas sebelumnya yaitu, <a href="https://github.com/afrianmc/BDT2019/tree/master/bdt-redis">Redis</a>
  
# Implementasi  Redis Cache pada wordpress

 - Install plugin `Rredis Object Cache`
 `Plugins > Add New > Redis Object Cache > Install Now > Activate`
 ![Ss](https://github.com/afrianmc/BDT2019/blob/master/EAS/ss/Screenshot%20from%202019-05-20%2021-19-49.png)
 
 - Buka wp-config.php pada proxy 
 `sudo nano wp-config.php`
 
 - Tambahkan konfigurasi :
 ` define( 'WP_REDIS_CLIENT', 'predis' );
define( 'WP_REDIS_SENTINEL', 'mymaster' );
define( 'WP_REDIS_SERVERS', [
    'tcp://192.168.33.11:26379?database=15&alias=master',
    'tcp://192.168.33.12:26379?database=15&alias=slave1',
    'tcp://192.168.33.13:26379?database=15&alias=slave2',
] );

define('WP_CACHE_KEY_SALT', 'example.com'); #WP_CACHE_KEY_SALT mengatur untuk semua key chace
define('WP_CACHE', true);  #WP_CACHE membuat cache persistent dengan plugin redis object chace`

# Monitoring Redis Cache

 - Mengecek koneksi redis
 ` Settings > Redis > Enable Object Cache`
 ![Ss](https://github.com/afrianmc/BDT2019/blob/master/EAS/ss/Screenshot%20from%202019-05-22%2001-08-33.png)
 
 - Konfigurasi wp-config.php
  NB : Status redis connected dengan 3 server yang telah kita konfigurasi sebelumnya.

- Monitoring dilakukan pada redis master dan slave 1, 2 :
`redis-cli monitor`
![Ss](https://github.com/afrianmc/BDT2019/blob/master/EAS/ss/Screenshot%20from%202019-05-22%2001-11-06.png)

- Coba dengan membuat post baru pada wordpress
![Ss](https://github.com/afrianmc/BDT2019/blob/master/EAS/ss/Screenshot%20from%202019-05-22%2001-11-54.png)

- Coba buka post yang sudah dibuat
![Ss](https://github.com/afrianmc/BDT2019/blob/master/EAS/ss/Screenshot%20from%202019-05-22%2001-12-48.png)

# Referensi
https://medium.com/@amila922/redis-sentinel-high-availability-everything-you-need-to-know-from-dev-to-prod-complete-guide-deb198e70ea6
https://www.digitalocean.com/community/tutorials/how-to-configure-redis-caching-to-speed-up-wordpress-on-ubuntu-14-04
https://www.cloudways.com/blog/install-redis-cache-wordpress/
 
