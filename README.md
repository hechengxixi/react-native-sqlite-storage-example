# react-native-sqlite-storage-example
    只针对Android，ios以后有机会再补充

## description
### document
    react-native-sqlite-storage README.md

### sqliteExample
    tutorial配套的例子

## tutorial
### 一、安装
    "react-native": "0.60.6",
    "react-native-sqlite-storage": "4.1.0"

### 二、配置
将一下代码加入 react-native.config.js（如果没有react-native.config.js则在项目根目录创建一个）
```js
module.exports = {
  dependencies: {
    "react-native-sqlite-storage": {
      platforms: {
        android: {
          sourceDir:
            "../node_modules/react-native-sqlite-storage/platforms/android-native",
          packageImportPath: "import io.liteglue.SQLitePluginPackage;",
          packageInstance: "new SQLitePluginPackage()"
        }
      }
    }
  }
};
```


### 三、 使用
```js
SQLite.DEBUG(true); // 开启debug console
SQLite.enablePromise(true); // 启用promise语法，默认为false
```


### 四、 创建数据库
```js
const database_name = "Test.db";
const database_version = "1.0";
const database_displayname = "SQLite Test Database";
const database_size = 200000;
let db;
SQLite.openDatabase(database_name, database_version, database_displayname, database_size).then((DB) => {
    db = DB;
    this.updateProgress("Database OPEN");
    // some transactions
}).catch((error) => {
    console.log(error);
});
```

### 五、导入已建的数据库文件
1. 使用DB Browser (SQLite) 创建一个数据库文件

![alt tag](https://raw.github.com/hechengxixi/react-native-sqlite-storage-example/master/instructions/1.png)

    sqlite数据库的size是通过page size * page count 来计算的
    
![alt tag](https://raw.github.com/hechengxixi/react-native-sqlite-storage-example/master/instructions/2.png)

2. 将.db文件修改为.sqlite3, 将文件放到下图目录

![alt tag](https://raw.github.com/hechengxixi/react-native-sqlite-storage-example/master/instructions/3.png)

3. 打开数据库
```js
const database_name = "testDB.sqlite3"; // 与数据库文件名相同
let db;
SQLite.openDatabase({name:database_name,createFromLocation:1}).then((DB) => {
    db = DB;
    this.updateProgress("Database OPEN");
    // some transactions
}).catch((error) => {
    console.log(error);
});
```