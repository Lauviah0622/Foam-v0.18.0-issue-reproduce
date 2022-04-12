今天在 turborepo 看到他們的描述黨有一個 $schema
```json
{
  "$schema": "https://turborepo.org/schema.json",
  "pipeline": {
    "build": {
      "dependsOn": ["^build"]
    },
    "test": {
      "dependsOn": ["build"]
    },
    "deploy": {
      "dependsOn": ["test"]
    },
    "frontend#deploy": {
      "dependsOn": ["ui#test", "backend#deploy", "backend#health-check"]
    }
  }
}
```

這個東西代表這份 Json 的描述黨，也就是這份 json 應該要套用什麼樣的格式。可以制定哪些屬性是必要的，可以為屬性下 description，還有一定要用什麼格式（boolean, number 等等）之類的。


https://kenve.github.io/understanding-json-schema#schema-%E5%85%B3%E9%94%AE%E5%AD%97