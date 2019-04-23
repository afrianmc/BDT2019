# Installasi Cassandra Multi Node

Sebelumnya, buat konfigurasi Vagrant file dan lakukan installasi java dan cassandra seperti pada tugas sebelumnya <a href="https://github.com/afrianmc/BDT2019/tree/master/Tugas_Cassandra/singlenode">Installasi Single Node</a>

## Menghapus data default

  Sebelum membuat multi-node, kita harus menghapus data di masing-masing node. Sebelumnya kita harus mematikan cassandra terlebih dahulu:
  ```
  sudo service cassandra stop
  sudo rm -rf /var/lib/cassandra/data/system/*
  ```
  
## Konfigurasi Cassandra

  Ubah konfigurasi cassandra.yaml file yang terletak pada direktori etc/cassandra.yaml :
  ```
  sudo nano /etc/cassandra/cassandra.yaml
  ```
  
  kemudian ubah beberapa konfigurasi sebagai berikut:
  ```
  .....
  cluster_name: 'TestCluster' #Nama Cluster anda, harus sama pada masing-masing node
  .....
  seed_provider:
      - class_name: org.apache.cassandra.locator.SimpleSeedProvider
        parameters:
          #ip node 1,ip node 2, dan seterusnya jika ada
          - seeds: "192.168.33.11,192.168.33.12"
  .....
  listen_address: 192.168.33.11 #ip masing-masing node tempat cassandra berjalan, 192.168.33.11 ini adalah node 1
  .....
  rpc_address: 192.168.33.11 #ip masing-masing node tempat cassandra berjalan, 192.168.33.11 ini adalah node 1
  .....
  endpoint_snitch: GossipingPropertyFileSnitch
  ```
  
  Jalankan kembali cassandra:
  ```
  sudo service cassandra start
  sudo nodetool status
  ```
  Outout:
  
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/nodetoll1.PNG)
  
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/nodetool2.PNG)
  
  Cek cqlsh
  ```
  cqlsh <ip-node> 9042
  ```
  Output:
  
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/cqlsh1.png)

  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/cqlsh2.png)
   
## Import Dataset

## Dataset

  ![Ss]()
    
  Dalam kesempatan kali ini, saya menggunakan dataset dari <a href="https://www.kaggle.com">Kaggle</a> yaitu dataset <a           href="https://www.kaggle.com/koki25ando/salary">NBA Player Salary Dataset (2017 - 2018)</a>. Dataset diambil dari Referensi Basket.     Dataset ini sangat sederhana yang hanya mencakup informasi tentang nama pemain, tim, dan jumlah gaji. 

  
## Referensi
https://www.digitalocean.com/community/tutorials/how-to-run-a-multi-node-cluster-database-with-cassandra-on-ubuntu-14-04
