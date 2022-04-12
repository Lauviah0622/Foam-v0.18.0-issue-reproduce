# posgresSQL.database

### 建立 database

```
CREATE DATABASE <dbname>
```

### 刪除 DB
```
DROP DATABASE <dbname>
```
要注意刪除 DB 名稱需要這個 DB 沒有被連線，

下面這個指令可以直接關閉所有與目標 DB 的連線，但是要注意自己不能和目標 DB 連線

```
SELECT pg_terminate_backend(pg_stat_activity.pid)
FROM pg_stat_activity
WHERE pg_stat_activity.datname = 'TARGET_DB' -- ← change this to your DB
  AND pid <> pg_backend_pid();
```



https://stackoverflow.com/questions/5408156/how-to-drop-a-postgresql-database-if-there-are-active-connections-to-it


如果是 14 版，可以使用

```
DROP DATABASE dev (FORCE)
```

https://stackoverflow.com/a/59021507/10766242

!!awesome

### 改 DB 名稱

```
ALTER DATABASE db RENAME TO newdb;
```

### 列出所有 DB

psql metacommand 版本

```
\l
```

