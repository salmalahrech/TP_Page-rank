# TP_Page-rank
TP GCP
Commande de création du BUCKET
```
gcloud storage buckets create gs://my_bucket_map_reduce --project=alpine-keep-363216  --location=europe-west1 --uniform-bucket-level-access
```

Copier les données du gs://public_lddm_data/page_links_en.nt.bz2 vers mon bucket
gsutil gs://public_lddm_data/page_links_en.nt.bz2  gs://my_bucket_map_reduce
![image](https://user-images.githubusercontent.com/35890810/195428435-2e277d44-9ebb-4128-a9f2-8af51d736dbd.png)

Commande de création du cluster avec 2 workers 

