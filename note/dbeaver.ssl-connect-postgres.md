# dbeaver.ssl-connect-postgres



如果用 dbeaver 使用 ssl 連接 postsql 資料庫，會有這個問題

```
Could not read SSL key file /Users/feversocial/.ssh/pickle-dev-client-key.pem.
  extra data given to DerValue constructor
  extra data given to DerValue constructor
```


參考這篇的作法

https://github.com/dbeaver/dbeaver/issues/1835#issuecomment-312969213


因為 dbeaver 底層用 JDBC 來連接資料庫，在私鑰部分需要用 pk8 格式，所以如果是 PEM 格式的私鑰要轉成 pk8

> Although psql has no trouble, the JDBC driver has format restrictions. The private key must be PKCS8 and stored in DER format, whereas the certificate is fine in PEM format (because of course it is). If your key is in PEM format (i.e. starts with something like -----BEGIN PRIVATE KEY-----) you can convert it with openssl:

要用以下指令

```
openssl pkcs8 -topk8 -inform PEM -outform DER -in postgresql.key -out postgresql.pk8 -nocrypt
```

記得加上 -cocrypt，因為用有密碼的模式不知位什麼會失敗（很複雜）

此外還要記得把金鑰的權限設定為 600 以下

```
chmod 600 ~./postgresql/postgresql.pk8
```