# prisma.usage

## migration
依照 prisma schema 建立 DB table


## introspection

從 DB 依照 table 來產生 prisma scheme

[[note/prisma.scheme.md]]



## prisma client 

```
npx prisma generate
```

可以產生 prisma/client 的 data model（記得安裝），每次改動 schema 都要記得重親執行一次


prisma/client 的 data model 會被儲存在 node_modules/.prisma/client 裡面
