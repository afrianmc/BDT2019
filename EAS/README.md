# Wordpress Menggunakan MySQL Cluster dan Redis
  
  Implementasi MySQL Cluster dan NoSQL Redis menggunakan 4 node.
  
# Model Arsitektur
  
  Pada Desain MySQL Cluster dan Redis kali ini, saya menggunakan 4 node dengan pembagian sebagai berikut :
  
No | HostName |    IP    | Keterangan  |
---|----------|----------|-------------|
1  |clusterdb1|192.168.33.11|ndb-Manager|
2 |clusterdb2|192.168.33.12|Node 1 dan API 1|
3 |clusterdb3|192.168.33.13|Node 2 dan API 2|
4 |clusterdb4|192.168.33.14|Load Balance(ProxySQL)|

# Installasi 
  
 
