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
   
# Import Dataset

  ## Dataset

  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/Dataset.PNG)
    
  Dalam kesempatan kali ini, saya menggunakan dataset dari <a href="https://www.kaggle.com">Kaggle</a> yaitu dataset <a           href="https://www.kaggle.com/koki25ando/salary">NBA Player Salary Dataset (2017 - 2018)</a>. Dataset diambil dari Referensi Basket.     Dataset ini sangat sederhana yang hanya mencakup informasi tentang nama pemain, tim, dan jumlah gaji. 
  
  ## Import Dataset
  
  - Masuk ke cassandra dengan sintaks:
  
  ```
    cqlsh 192.168.33.12
  ```
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/cqlsh192.168.33.12.PNG)

  - Buatlah keyspace/database pada cassandra sesuai dengan database yg akan dibuat.
  
  ```
    CREATE KEYSPACE healthdb1 WITH REPLICATION = { 'class' : 'NetworkTopologyStrategy', 'dc1' : 2 }
  ```
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/CreateKeyspace.PNG)
  
  - Buatlah tabel dalam keyspace/database yang sudah dibuat.
  
   ```
    CREATE TABLE healtdb1.salary2 (Id_no int PRIMARY KEY, Player text, Tm text, season17_18 int );
   ```
   ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/CreateTable.PNG)
   
  - Import dataset yang digunakan
  
  ```
    COPY healthdb1.salary2 (Id_no, Player, Tm, season17_18) FROM '/vagrant/NBA_season1718_salary.csv' WITH DELIMITER=',' AND HEADER=TRUE;
  ```
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/ImportDataset.PNG)
  
  ## CRUD
  
  - Masuk kedalam cassandra yang sudah dibuat.
  
  ```
    cqlsh healthdb1
  ```
  ![Ss]()
  
  - Create, Membuat data baru
 
  ```
    INSERT INTO healthdb1.salary2 (Id_no, Player, Tm, season17_18) VALUES (1000, 'Afrian', 'NBA', 1500000);
  ```
  
   Cek :
  ```
    SELECT * FROM salary2
  ```
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/Create.PNG)
  
  - Read, Cek hasil import dataset
  ```
    SELECT * FROM salary2
  ```
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/Import.PNG)
  
  - Update, mengedit data yang sudah ada
  ```
  UPDATE healthdb1.salary2 Tm='ATL' WHERE Id_no=1000;
  ```
  
   Cek :
  ```
    SELECT * FROM salary2
  ```
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/Update.PNG)
  
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/Update1.PNG)
  - Delete, menghapus data yang ada
  ```
    DELETE FROM healthdb1.salary2 WHERE Id_no=1000;
  ```
  
  Cek :
  ```
    SELECT * FROM salary2
  ```
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Cassandra/multinode/screenshoot/DELETE.PNG)
  
  
## Referensi
https://www.digitalocean.com/community/tutorials/how-to-run-a-multi-node-cluster-database-with-cassandra-on-ubuntu-14-04
http://tutorialwindow.com/how-to-import-data-from-excel-or-csv-files-to-cassandra-database
https://www.kaggle.com
