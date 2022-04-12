# posgresSQL.command

## metacommand

```
$ \c [ dbname　 [ username ] [ host ] [ port ] | conninfo ] # \con　nect [dbname] 與該 database 連線
$ \encoding [ encoding ]
$ \du           # 列出所有 roles
$ \du+          # 列出所有 roles & 詳細資料
$ \l            # 列出所有 database

# 資料表相關
$ \z [pattern] # 列出所有 table

# 設定環境變數
$ \set foo bar # 將 foo 設為 bar
$ \echo :foo   # 取得 foo 的變數值

# 其他
$ \h create table # 查詢用法
$ \! pwd          # 取得當前資料夾名稱
$ \q              # \quit，離開

# 帳號相關
$ \password [ username ]
```

建立 DB

```
createdb <database-name> -O pjchender -E utf8
```

列出所有 DB

```
\l
```

連結 DB

```
\connect <dbname>
\c <dbname>

ex: 
\c template0
```


### tips

[[note/posgresSQL.command.tips.md]]
