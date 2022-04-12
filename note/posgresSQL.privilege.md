# posgresSQL.privilege

列出一位用戶的所有權現

```
SELECT table_catalog, table_schema, table_name, privilege_type
FROM   information_schema.table_privileges 
WHERE  grantee = 'MY_USER'
```