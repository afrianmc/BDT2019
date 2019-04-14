# Instalasi Cassandra Single Node

Sebelumnya, buat konfigurasi Vagrant file sebagai berikut :

![ss]

## Install Java Oracle

1.  install properties-common menambahkan add repository:
  ```
  sudo apt-get update                               # apt-get update digunakan untuk mengupdate package yang sudah ada
  sudo apt-get install software-properties-common   # install lib for add apt 
  ```

2. Menambahkan repository baru untuk java:
  ```
  sudo add-apt-repository ppa:webupd8team/java    # add repository java
  sudo apt-get update                             # apt-get update untuk repository java yang baru agar repository yang baru ikut         terupdate
  ```
  Output:
  ![Ss]
  
3. Install Java:
  ```
  sudo apt-get install oracle-java8-set-default
  ```
  Untuk mengecek versi java dengan menggunakan sintaks:
  ```
  java -version
  ```
  Output:
  ![Ss]
  
## Install Cassandra

1. Install cassandra repository ke /etc/apt/sources.list.d/cassandra.sources.list
  ```
  echo "deb http://www.apache.org/dist/cassandra/debian 39x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
  ```
   
2. Jalankan CURL command untuk menambahkan repository keys lalu update repository
  ```
  curl https://www.apache.org/dist/cassandra/KEYS | sudo apt-key add -
  sudo apt-get update                                                   # update repository
  ```
  Output:
  ![Ss]
  
3. Install Cassandra
  ```
  sudo apt-get install cassandra
  ```
  
  Lakukan verifikasi dengan sintaks:
  ```
  nodetool status
  ```
  Output:
  ![Ss]
  
  Kemudiaan cek running Cassandra:
  ```
  sudo service cassandra status
  ```
  Output:
  ![Ss]
  
4. Connect dengan cqlsh
  ```
  cqlsh
  ```
  Output:
  ![Ss]
  
## Referensi
https://www.digitalocean.com/community/tutorials/how-to-install-cassandra-and-run-a-single-node-cluster-on-ubuntu-14-04


