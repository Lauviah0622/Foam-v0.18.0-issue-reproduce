# posgresSQL.login


## 利用 ssl 登入

```
psql "sslmode=verify-ca sslrootcert=/Users/feversocial/.ssh/pickle-dev-server-ca.cert sslcert=/Users/feversocial/.ssh/pickle-dev-client-cert.cert sslkey=/Users/feversocial/.ssh/pickle-dev-client-key.pem  hostaddr=34.81.228.116 user=postgres"

```


> 在 mac OS 上，似乎不能用家路徑 `~`

> 在 mac OS 上，需要設定檔案的權限小於 600


預設會用 user 的名稱來登入指定的 DB，如果不希望這麼做，可以直接指定


```
psql "sslmode=verify-ca sslrootcert=/Users/feversocial/.ssh/pickle-dev-server-ca.cert sslcert=/Users/feversocial/.ssh/pickle-dev-client-cert.cert sslkey=/Users/feversocial/.ssh/pickle-dev-client-key.pem  hostaddr=34.81.228.116 user=postgres dbname=dbname"

```


