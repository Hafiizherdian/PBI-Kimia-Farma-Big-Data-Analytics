# PBI-Kimia-Farma-Big-Data-Analytics
Program Project Based Internship kolaborasi Rakamin Academy dan Kimia Farma Big Data Analytics merupakan program pengembangan diri dan akselerasi karier yang diperuntukkan untuk mendalami posisi Big Data Analytics di perusahaan Kimia Farma.

| Tools |  |
| ------ | ------ |
| GCP | https://console.cloud.google.com/ |
| Looker Studio | https://lookerstudio.google.com/ |

Dataset
- [kf_final_transaction.csv](https://drive.google.com/file/d/1iDOBdKZ4-kkLhpklQWWrsFvACtI7MCz3/view)
- [kf_inventory.csv](https://drive.google.com/file/d/1ihtG2t0V1AO0IAGkGwQaqtba6AxDEKDI/view)
- [kf_kantor_cabang.csv](https://drive.google.com/file/d/1vzaasqIeXqqe_jI99dNLaa8nxnoe9OWW/view)
- [kf_product.csv](https://drive.google.com/file/d/1739wO7BwtVStHCA4Dcj9xGhlc_blBNbT/view)

---

## Objectives
1. Importing Dataset to BigQuery
2. Buat tabel analisa
3. Create Dashboard Performance Analytics Kimia Farma Business Year 2020-2023

---
### 1. Importing Dataset to BigQuery

  Mengimport keempat dataset yang akan digunakan untuk tabel pada BigQuery.


### 2. Buat tabel analisa

  Membuat tabel analisa berdasarkan hasil aggregasi dari ke-empat tabel yang sudah diimport sebelumnya.
  ![sample data](https://github.com/Hafiizherdian/PBI-Kimia-Farma-Big-Data-Analytics/assets/152409368/89c49eea-8f39-4e06-8693-5a7b5e5cc645)
    


### 3. Create Dashboard Performance Analytics Kimia Farma Business Year 2020-2023
    
  Membuat sebuah dashboard analisis kinerja Kimia Farma tahun 2020-2023 di Google Looker Studio berdasarkan tabel analisa yang telah dibuat

![Kimia_farma_pages-to-jpg-0001](https://github.com/Hafiizherdian/PBI-Kimia-Farma-Big-Data-Analytics/assets/152409368/96ba5bc3-2c07-4322-b1f3-04a97b1e23fb)
![Kimia_farma_pages-to-jpg-0002](https://github.com/Hafiizherdian/PBI-Kimia-Farma-Big-Data-Analytics/assets/152409368/a0efc3d8-bf3e-456c-bed3-eaff9bf0a9da)

GCP BigQuery https://console.cloud.google.com/bigquery?sq=328311511300:bc9dd7edf21447c0a91470b1d83b25d1

Dashboard Performance Analytics https://lookerstudio.google.com/s/tqsjxqcfy4Q

<details><summary><b>Show Query Tabel Analisa</b></summary>

    select transaksi.transaction_id, transaksi.date,KC.branch_id, KC.branch_name, KC.kota, KC.provinsi, KC.rating, transaksi.customer_name, inventory.product_id, inventory.product_name, product.price, transaksi.discount_percentage, transaksi.price - (transaksi.price * transaksi.discount_percentage) as nett_sales, transaksi.price * inventory.opname_stock as nett_profit, transaksi.rating rating_transaksi, KC.branch_id as total_transaksi,
    CASE
            when product.price <= 50000 THEN 0.1
            when product.price > 50000 AND product.price <= 100000 THEN 0.15
            when product.price > 100000 AND product.price <= 300000 THEN 0.2
            when product.price > 300000 AND product.price <= 500000 THEN 0.25
            when product.price > 500000 THEN 0.3
        end as persentase_gross_laba
        from kimia_farma.kf_final_transaction transaksi
        
    left join 
    kimia_farma.kf_kantor_cabang KC on transaksi.branch_id = KC.branch_id
        
    left join 
    kimia_farma.kf_inventory inventory on transaksi.product_id = inventory.product_id
        
    right join 
    kimia_farma.kf_product product on transaksi.price = product.price
    limit 1035000;

    
    
