# Implementasi MongoDB

- Download dan Install terlebih dahulu MongoDB Compass <a href="https://www.mongodb.com/cloud/atlas">MongoDB</a>
- Lakukan Registrasi di Website <a href="https://www.mongodb.com/cloud/atlas">MongoDB</a>
- Login, kemudian ikuti langkah-langkah sebagai berikut:
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Implementasi_MongoDB/Screenshot/setelah%20login.PNG)

- Buatlah user
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Implementasi_MongoDB/Screenshot/create%20user.PNG)

- Setting IP
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Implementasi_MongoDB/Screenshot/ip.PNG)
  
- Sambungkan ke Cluster dengan klik ```CONNECT```
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Implementasi_MongoDB/Screenshot/connect%20to%20cluster.PNG)

- Setelah disambungkan, buka MongoDB Compass yang sudah di install. Maka akan muncul tampilan seperti dibawah ini:
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Implementasi_MongoDB/Screenshot/Connect.PNG)
  
- Setelah itu, import file json menggunakan terminal di dalam file mongodb yang telah diinstall

- file json yang saya adalah <a href="https://www.kaggle.com/theriley106/grammyawardsinnumbers">Grammy Awards in Number</a>

  ```mongoimport --host clusterdb1-shard-00-00-e6qeg.mongodb.net:27017 --db gdp --type json --file     D:\NY_GDP_MKTP.json --jsonArray --       authenticationDatabase admin --ssl --username Afrian --password 1```
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Implementasi_MongoDB/Screenshot/ImportDataset.jpeg)
  
- cek mongodb compass, jika berhasil akan keluar output seperti ini:
  ![Ss](https://github.com/afrianmc/BDT2019/blob/master/Tugas_Implementasi_MongoDB/Screenshot/Cekdataset.jpeg)
  
Referensi:

- https://www.mongodb.com/cloud/atlas

- https://www.youtube.com/watch?v=tpz-6Trd1UI
