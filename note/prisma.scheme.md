# prisma.scheme

## 功能


prisma scheme 可以用來建立 prisma client library

## prisma 的命名慣例
目的是更方便的在 JS / TS 裡面作使用

https://www.prisma.io/docs/reference/api-reference/prisma-schema-reference#naming-conventions-1

-  table 命名小寫
-  camel case


## connection

```
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```
url 格式
```
postgresql://postgres:JmV58mt9XiFJDz5M@34.81.228.116:5432/test?schema=public&sslmode=require&sslcert=/Users/feversocial/.ssh/pickle-dev-server-ca.cert&sslidentity=/Users/feversocial/.ssh/pickle-client-identity.p12&sslpassword=JmV58mt9XiFJDz5M
```

記得這邊的 sslidentity 要用 `PKCS12` 的格式（ssl 憑證可以有很多不同的格式），可以透過下面的指令來轉換

```
openssl pkcs12 -export -out client-identity.p12 -inkey client-key.pem -in client-cert.pem
```



## modle

### @map
因為 prisma client 會依照 schema 來產生 ORM api。而產生的命名就是依據 schema，但是有時候 DB 的 column 會用大寫開頭，或者是 kabob case 等不符合 JS 慣例的命名。這時候就可以用 @map 來把名稱映射到真實的 DB column

```prisma
model MyUser {
  userId    Int     @id @default(autoincrement()) @map("user_id")
  firstName String? @map("first_name")
  lastName  String  @unique @map("last_name")

  @@map("my_user")
}
```

`@map` 用來 mapping column，`@@map` 用來 mapping table