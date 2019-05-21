# Wordpress Menggunakan MySQL Cluster dan Redis
  
  Implementasi MySQL Cluster dan NoSQL Redis menggunakan 4 node.
  
# Model Arsitektur
  
  Pada Desain MySQL Cluster dan Redis kali ini, saya menggunakan 4 node dengan pembagian sebagai berikut :
  
No | HostName |    IP    | Keterangan  |
---|----------|----------|-------------|
1  |clusterdb1|192.168.33.11|Sebagai Node Manager dan Redis|
2 |clusterdb2|192.168.33.12|Sebagai Server1 dan Node1 dan Redis|
3 |clusterdb3|192.168.33.13|Sebagai Server2 dan Node2 dan Redis|
4 |clusterdb4|192.168.33.14|Sebagai Load Balance(ProxySQL)|

# Installasi `apache`

  - Proses installasi mysql-cluster sama dengan tugas sebelumnya yaitu, (link tugas implementasi mysql-cluster)
  
# Installasi `wordpress`

  - Proses installasi wordpress sama dengan tugas sebelumnya yaitu, (link tugas ets)
  
# Installasi `Redis`

  - Proses installasi redis sama dengan tugas sebelumnya yaitu, (link tugas redis)
  
# Implementasi  Redis Cache pada wordpress

 - Install plugin `Rredis Object Cache`
 `Plugins > Add New > Redis Object Cache > Install Now > Activate`
 
 - Buka wp-config.php pada proxy atau clusterdb4
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
 
 - Konfigurasi wp-config.php
  NB : Status redis connected dengan 3 server yang telah kita konfigurasi sebelumnya.

- Monitoring dilakukan pada redis master dan slave 1, 2 :
`redis-cli monitor`

- Coba dengan membuat post baru pada wordpress

- Coba buka post yang sudah dibuat

# Referensi

  
 
