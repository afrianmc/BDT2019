#Tugas ETS

## 1. Pembagian Arsitektur dan IP

kali ini kita akan membuat 4 node yaitu 1 ndb-manager, 1 load balance(Proxy), 2 node dan 2 service API seperti pada tugas sebelumnya <a href="https://github.com/afrianmc/mysql-cluster">MySQL Proxy</a>

No | HostName |    IP    | Keterangan  |
---|----------|----------|-------------|
1  |clusterdb1|192.168.33.11|ndb-Manager|
2 |clusterdb2|192.168.33.12|Node 1 dan API 1|
3 |clusterdb3|192.168.33.13|Node 2 dan API 2|
4 |clusterdb4|192.168.33.14|Load Balance(ProxySQL)|


## 2. Instalasi Wordpress

- masuk ke proxy :

  (proxy)```vagrant ssh dbcluster4```

- install apache2

  (proxy)```sudo apt-get install apache2```
  
  (proxy)```sudo apt-get install php -y```
  
  (proxy)```sudo apt-get install php-mysql```
  
  (proxy)```sudo apt-get install -y php-gd php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-snmp php-soap php-tidy curl```

- install wordpress

  (proxy)```cd /tmp```
  
  (proxy)```wget -c http://wordpress.org/latest.tar.gz```
  
  (proxy)```tar -xzvf latest.tar.gz```
  
  (proxy)```sudo mv wordpress/* /var/www/html```
  
  (proxy)```sudo chown -R www-data:www-data /var/www/html```
  
  (proxy)```sudo chmod -R 755 /var/www/html```
  
  (proxy)```sudo service apache2 restart```
  

- masuk ke direktori /var/www/html/wp-admin/includes

- copy schema.php ke file vagrant untuk memudahkan dalam mengedit
  
  (proxy)```cp /var/www/html/wp-admin/includes/schema.php /vagrant```

- buka schema.php yang sudah dicopykan dan tambahkan "ENGINE=NDB" disetiap tabelnya

- copy kembali schema.php ke dalam direktori var/www/html/wp-admin/includes/

- buat direktori baru didalam direktori  /var/www/html/

  (proxy)```mkdir (nama direktori baru) ex: wordpress```

- masuk ke dalam direktori baru

- install 
  (proxy)```wget -c http://wordpress.org/latest.tar.gz```
  
  (proxy)```tar -xzvf latest.tar.gz```

- masuk ke dalam direktori wordpress

  (proxy)```cd /wordpress/wordpress```

  (proxy)```sudo nano wp-config```

- masukkan nama database, username, password dan hostname sesuai dengan yg telah dibuat
![Ss](https://github.com/afrianmc/BDT2019/blob/master/Screenshot/wp-config%20.png)

- buka wordpress pada browser
http://192.168.33.14/wordpress/wordpress

- maka akan muncul tampilan seperti :
![Ss](https://github.com/afrianmc/BDT2019/blob/master/Screenshot/installwordpress.png)

- ikuti langkah instalasi wordpress
![Ss](https://github.com/afrianmc/BDT2019/blob/master/Screenshot/login.png)


## 3. Cek Schema

schema yang telah dibuat pada wordpress, otomatis akan ada didalam dbcluster2, dan dbcluster3

![Ss](https://github.com/afrianmc/BDT2019/blob/master/Screenshot/ets%20tables.png)

- masuk ke cluster2

  (dbcluster2)```vagrant ssh dbcluster2```
  
  (dbcluster2)```mysql -u wordpress -p -h 192.168.33.14 -P 6033```
  
  (dbcluster2)```show databases;```
  
(maka akan muncul database yang telah dibuat ex:ets)

  (dbcluster2)```use ets;

## 4. Test Database

- cek status ndb pada salah satu node (cluster2)

(dbcluster2)```ndb_mgm```

(dbcluster2)```show```

![Ss](https://github.com/afrianmc/BDT2019/blob/master/Screenshot/show%20databases.png)

- matikan salah satu node cluster3

(dbcluster3)```sudo systemctl stop mysql```

cek dinode cluster2

(dbcluster2)```show```

![Ss](https://github.com/afrianmc/BDT2019/blob/master/Screenshot/cek%20salah%20satu%20node%20mati.png)

matikan kedua node

(dbcluster2 dan dbcluster3)```sudo systemctl stop mysql
