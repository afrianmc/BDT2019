# Wordpress Menggunakan MySQL Cluster dan Redis
  
  Implementasi MySQL Cluster dan NoSQL Redis menggunakan 4 node.
  
# Model Arsitektur
  
  Pada Desain MySQL Cluster dan Redis kali ini, saya menggunakan 4 node dengan pembagian sebagai berikut :
  
  | No. | IP Address | Hostname | Deskripsi |
  |-----|-------------|----------|-----------|
  | 1. | 192.168.33.11 | dbcluster1 | Sebagai Manager dan Redis |
  
  | 2. | 192.168.33.12 | dbcluster2 | Sebagai Server1 dan Node1 dan Redis |
  
  | 3. | 192.168.33.13 | dbcluster3 | Sebagai Server2 dan Node2 dan Redis |
  
  | 4. | 192.168.33.14 | dbcluster4 | Sebagai Load Balancer (ProxySQL) |
  
# Installasi 
  
 
