# posgresSQL.role

```
$ \du           # 列出所有 roles
$ \du+          # 列出所有 roles & 詳細資料
$ \l            # 列出所有 database，這個也會列出哪個 role 擁有 db
```

## 角色

- 角色擁有資料庫物件，包含資料表、資料庫、函數
- 角色可以分配自己擁有的權限給其他角色
- 角色可以把自己的「身分（或者說權限）」指定給其他角色

自己的理解是，角色同時有成員 & 群組的概念

### 查詢角色資料

角色資料會被放在 `pg_roles` 這張表裡面，我們可以透過這張表來知道有哪些角色還有有哪些角色屬性。

```
 rolname          | rolsuper | rolinherit | rolcreaterole | rolcreatedb | rolcanlogin | rolreplication | rolconnlimit | rolpassword | rolvaliduntil | rolbypassrls | rolconfig |  oid
```

所以我們可以用這個指令來 SELECT pg_roles 的所有 role

```
SELECT * FROM pg_roles;
```

也可以看特定 role 的所有 attribute

```sql
SELECT * FROM pg_roles WHERE rolname = 'test2';
```

記得字串要用 `' '` 包住

### 操作角色

#### 建立

```SQL
CREATE ROLE name LOGIN
```

```sql
CREATE USER name
```

`CREATE USER ` 會建立預設帶有 LOGIN attribute 的 role，如果不希望可以登入（目前不太清楚這可以幹嘛，可能是繼承用），可以使用單純的 `CRATE ROLE name`

沒有 login 的角色在 `\du` 指令會特別註記　`Cannot Login`

| List of roles Role name | Attributes   | Member of |
| ----------------------- | ------------ | --------- |
| test                    |              | {}        |
| test2                   |              | {}        |
| test3                   | Cannot login | {}        |

內建的角色名稱
```
          rolname
---------------------------
 cloudsqladmin
 pg_monitor
 pg_read_all_settings
 pg_read_all_stats
 pg_stat_scan_tables
pg_read_server_files
 pg_write_server_files
 pg_execute_server_program
 pg_signal_backend
 cloudsqlsuperuser
 cloudsqlagent
 cloudsqlimportexport
 cloudsqlreplica
 cloudsqliamuser
 cloudsqliamserviceaccount
```

PG 開頭的 role 應該是 preset，可以讓我們作 member of 方便管理，不用再自行定義。

#### 刪除
```sql
DROP ROLE name; 
```

基本的刪除角色指令，但是如果角色擁有資料庫物件，而且有權限就不能刪除

所以需要
1. 先把需要保存的物件分配其他使用者，或者是刪除
2. 在把角色上用有的物件刪除
3. 刪除角色

```
REASSIGN OWNED BY doomed_role TO successor_role;
DROP OWNED BY doomed_role;
-- repeat the above commands in each database of the cluster
DROP ROLE doomed_role;
```


#### membership

postgresSQL 的角色是可以賦予給其他角色的，有點像是繼承的概念

賦予 A 角色 B角色的 權限
```
GRANT b TO a
```
撤銷 A 角色 B 角色的 權限

```
REVOKE b FROM a
```

SET ROLE => 暫時成為某個 group role


#### Default Roles

#### 更改名稱

https://www.postgresqltutorial.com/postgresql-administration/postgresql-alter-role/

```
ALTER ROLE role_name TO new_name;
```

## attribute

|             |                                                                           |                                                                           |
| ----------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| SUPERUSER   | 所有權限除了 LOGIN                                                        | 要用 SUPERUSER 才能建立 SUPER USER，也只有 SUPER USER 可以修改 SUPER USER |
| CREATEROLE  | 能夠建立角色，修改角色（alter），刪除角色（drop), grant, revoke |                                                                           |
| CREATEDB    | 能夠建立 DB                                                               |                                                                           |
| REPLICATION | streaming replication ？不太懂                                            |                                                                           |
| 指定密碼 | CREATE ROLE name PASSWOOD 'string'                                            |                                                                           |
| INHERIT | 能夠繼承                                            |                                                                           |
| NOINHERIT | 不能繼承
                                            |                                                                           |


### 設定角色預設設定


```sql
ALTER ROLE myname SET enable_indexscan TO off;
```

這樣下次登入就會自動採用這樣的設定


### privilege

這代表哪個角色「擁有」 object

作角色

建立 DB, 建立 ROLE 這些東西是 role 的 attribute 要用這個
ALTER ROLE role_name [WITH] option;

https://www.postgresqltutorial.com/postgresql-administration/postgresql-alter-role/

GRANT, REVOKE 這個是操作 DB 的權限，要用
https://docs.postgresql.tw/the-sql-language/ddl/privileges

怎麼看所有的權限，不過
https://tableplus.com/blog/2018/08/postgresql-how-to-list-all-privileges.html


## 密碼

> 如果有開啟密碼，但沒有設定 role 的密碼的話，這樣登入的時候會永遠失敗。
### 設定密碼

在建立帳戶的時候設定密碼
```
CREATE ROLE name PASSWORD 'string';
```
更改帳戶的設定來設定 / 修改密碼

```
ALTER ROLE name PASSWORD 'string';
```

