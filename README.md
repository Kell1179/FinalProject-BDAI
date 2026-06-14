# FinalProject-BDAI
Repositori ini merupakan tugas besar mata kuliah Big Data dan AI yang menerapkan 4 model berbeda untuk mendeteksi money-laundering dan dihubungkan melalui clustering PySpark. Adapun dataset yang digunakan adalah : [IBM Transactions for Anti-Money Laundering](https://www.kaggle.com/datasets/ealtman2019/ibm-transactions-for-anti-money-laundering-aml?select=HI-Medium_Trans.csv)  

**Note**: XGBoost dan CatBoost tidak dilakukan pada cluster karena tidak didukung oleh PySpark, sehingga dhasil prediksi machine learning diambil dari notebook XGBoost dan CatBoost yang terpisah.

## Kelompok 6 :
1. Mirekel Ilham Akbar - 103012330486 (Merge Notebook dan setup PySpark)
2. Ilham Fadhillah Sanni - 103012300263 (Model Random Forest)
3. Bimantara Ardi Winata - 103012300282 (Model CatBoost)
4. Ezra Hafizh Raditya - 103012330244 (Model XGBoost)
5. Kayla Zahra Nafaiza - 103012300219 (Model SVM)  

___

## Arsitektur
```
┌─────────────────────────────────────────────────────┐
│  spark://<MASTER_IP>:7077                           │
│                                                     │
│  [Master Node]  ←──── Jupyter Notebook (driver)     │
│       │                                             │
│  ┌────┴────┐                                        │
│  │Worker 1 │  RAM: 8GB  │  Dataset: lokal           │
│  │Worker 2 │  RAM: 8GB  │  Dataset: lokal           │
└──┴─────────┴────────────────────────────────────────┘
```

## Pre-requisite setiap node (Worker/Master)
1. Python
2. JDK17
3. Apache Spark
4. Jupyter notebook (master)
**Note : Pastikan versi python dan JDK yang digunakan worker dan master sama untuk menghindari inkompabilitas**  

## Python Libraries
Pastikan setiap worker memiliki library berikut :
1. PySpark
2. XGBoost
3. CatBoost
4. Scikit-learn
5. Matplotlib
6. Seaborn
7. Pandas
8. Numpy
9. PyArrow  

Library tersebut dapat diinstal melalui cmd dengan menggunakan command berikut :  
```
pip install pyspark xgboost catboost scikit-learn matplotlib seaborn pandas numpy pyarrow
```

___

## Setup Environment
| Variable | Value |
|---|---|
| `JAVA_HOME` | `C:\Program Files\Java\jdk-17` (sesuaikan dengan direktori JDK terinstal) |
| `SPARK_HOME` | `C:\spark` (sesuaikan dengan direktori spark terinstal)|
| `HADOOP_HOME` | `C:\spark` (sesuaikan dengan direktori spark terinstal)|
| `PATH` | Tambahkan `%SPARK_HOME%\bin` dan `%JAVA_HOME%\bin` |



## Langkah - langkah menjalankan program Unified
1. Clone repository ini dengan menjalankan git clone ```<url>``` pada cmd
2. Letakkan CSV (atau parquet jika sudah konversi) pada path direktori yang sama pada setiap worker dan master
3. Pada notebook unified, sesuaikan IP Master dan Path CSV serta parquet
   ```
   MASTER_IP   = "<IP Master>"  # ← IP master node (sesuaikan)
   DRIVER_IP   = "<IP Master>"  # ← IP yang dipakai driver untuk bind
   ```
   ```
   CSV_PATH     = "<PATH CSV>"   # ← Sesuaikan
   PARQUET_PATH = "<PATH Parquet>" # ← Sesuaikan
   ```
   Pada windows, IP dapat dicek melalui cmd dengan menjalankan ```ipconfig```
4. Pada master, buka direktori tempat PySpark diinstal dan jalankan spark master melalui cmd dengan command berikut :
   ```
   .\bin\spark-class.cmd org.apache.spark.deploy.master.Master --host <IP Master> --port 7077 --webui-port 8080
   ```
5.  Cek spark master pada ```<IP Master>:7077``` dan ```<IP Master>:8080```. Pastikan keduanya berjalan
6.  Pada setiap worker, buka direktori tempat PySpark diinstal dan jalankan spark worker melalui cmd dengan command berikut :
   ```
   .\bin\spark-class.cmd org.apache.spark.deploy.worker.Worker spark://<IP Master>:7077 --host <IP Worker> --port 7078 --webui-port 8081
   ```
7. Pada master, buka cmd pada direktori tempat notebook diletakkan dan jalankan jupyter notebook
8. Jalankan notebook (Cell konversi CSV -> .parquet cukup dijalankan sekali saja)



## Langkah - langkah menjalankan program XGBoost / CatBoost
1. Clone repository ini dengan menjalankan git clone ```<url>``` pada cmd
2. Pada PC mana saja, buka cmd pada direktori tempat notebook diletakkan dan jalankan jupyter notebook
3. Pilih notebook XGboost / CatBoost dan jalankan pada jupyter notebook

