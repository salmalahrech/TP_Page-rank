# TP_Page-rank
TP GCP
Commande de création du BUCKET
```
gcloud storage buckets create gs://my_bucket_map_reduce --project=alpine-keep-363216  --location=europe-west1 --uniform-bucket-level-access
```

Copier les données du gs://public_lddm_data/page_links_en.nt.bz2 vers mon bucket
```
gsutil gs://public_lddm_data/page_links_en.nt.bz2  gs://my_bucket_map_reduce
```
Importer le code PIG : Dataproc.py et celui de Pyspark 
Commande de création du cluster avec 1 master et 2 workers et puis on va varier le nombre de workers par la suite 
```
gcloud dataproc clusters create cluster-a35a --enable-component-gateway --region europe-west1 --zone europe-west1-c --master-machine-type n1-standard-4 --master-boot-disk-size 500 --num-workers 2 --worker-machine-type n1-standard-4 --worker-boot-disk-size 500 --image-version 2.0-debian10 --project alpine-keep-363216
```
Commande pour lancer le job avec pig:
```
 gcloud dataproc jobs submit pig --region europe-west1 --cluster cluster-a35a -f gs://my_bucket_map_reduce/dataproc.py
```
commande pour lancer le job avec pyspark
```
gcloud dataproc jobs submit pyspark --region europe-west1 --cluster cluster-a35a gs://my_bucket_map_reduce/pagerank-notype.py  -- gs://my_bucket_map_reduce/page_links_en.nt.bz2  3
```
## Resultat de la durée d'éxecution :

              PIG           |   Pyspark
              ------------- | -------------
    2 noeuds |  49 min 37 s | 44 min 15 s         
    3 noeuds |  39 min 47 s | 39 min 42 s
    4 noeuds |  35 min 14 s | 35 min 45 s
    5 noeuds |  35 min 28 s | 38 min 53 s
       
