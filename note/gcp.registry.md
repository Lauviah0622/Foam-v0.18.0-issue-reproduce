# gcp.registry




1. 要有權限


docker 上也要有權欠可以 push image 到 gcp 上

看這份設定
https://cloud.google.com/container-registry/docs/advanced-authentication


有四種可以給 docker 權限的方式

- gcloud credential helper
- Standalone credential helper
- Access token
- JSON key file


## gcloud credential helper
讓本機的 app 有使用 GCP 的權限




1. 要到 IAM 建立帳號
2. 然後再授予權限
3. 拿到 json 驗證檔案
4. 用 json 驗政黨驗證本機
gcloud credential helper 驗證
```
gcloud auth activate-service-account ACCOUNT --key-file=KEY-FILE
```

pg://cloudsql:5432?u=user&p=password&d=database


NC_DB="mysql2://host.docker.internal:3306?u=root&p=password&d=d1" \
    -e NC_AUTH_JWT_SECRET="569a1821-0a93-45e8-87ab-eb857f20a010"


ocker run -d -p 8080:8080 \
    -e NC_DB="pg://34.80.176.103:5432?u=postgres&p=EQgDdDF43UbEsk&d=Personal" \
    -e NC_AUTH_JWT_SECRET="subscript-remember-enjoyably-bolster" \
    nocodb/nocodb:latest

## 從 Cloud Run 連線到 SQL Server

https://cloud.google.com/sql/docs/postgres/connect-run?authuser=2



## 把 image 丟進 container registry

前提是要有 權限

1. 上 tag
```
docker tag nocodb-gcp asia.gcr.io/avian-sandbox-346513/nocodb-gcp
```

2. docket push

```
docker push asia.gcr.io/avian-sandbox-346513/nocodb-gcp
```

