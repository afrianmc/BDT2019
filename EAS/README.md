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

# Installasi `apache` dan `wordpress`

  - Proses installasi mysql-cluster sama dengan tugas sebelumnya yaitu, (link tugas implementasi mysql-cluster)
  - Proses installasi wordpress sama dengan tugas sebelumnya yaitu, (link tugas ets)
  
# Installasi `Redis`

  
 
