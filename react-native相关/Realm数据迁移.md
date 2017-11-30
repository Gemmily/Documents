### realm数据库迁移
---
###1.Realm
Realm是Realm移动数据库容器的实例，可以是本地的或同步的。
###2.打开Realm
打开Realm只是通过实例化一个新的Realm对象来执行。将配置对象传递给构造函数。
```javascript
// Get the default Realm with support for our objects
Realm.open({schema: [Car, Person]})
  .then(realm => {
    // ...use the realm instance here
  })
  .catch(error => {
    // Handle the error here if something went wrong
  });
```
有关配置对象的完整详细信息请参阅[API配置][5]。对象的一些更常见的键，除了`schema`，包括：
+ `path`：指定[另一个Realm路径][2]
+ `migration`： [迁移][3]
+  `sync`： [同步对象][4]， 打开与Realm对象服务器同步的Realm。
+  `inMemory`：Realm in-memory打开， 且对象不持久，一旦Realm被关闭所有对象会消失。
```javascript
// Open a realm at another path
Realm.open({
  path: 'anotherRealm.realm',
  schema: [CarSchema]
}).then(/* ... */);
// migration
Realm.open({
  schema: [PersonSchema],
  schemaVersion: 1,
  migration: (oldRealm, newRealm) => {}
}).then(/* ... */);
```
###3.默认Realm
使用`Realm.defaultPath`全局属性访问和更改默认的Realm路径。
###4.其他Realm
有多个Realm在多个位置持久化是有用的。例如，除了主Realm外，还希望捆绑一些数据于应用程序在Realm文件中。可以通过在初始化Realm时指定路径参数来执行此操作。所有相对于应用程序的路径都可写入文档目录中。
```javascript
// Open a realm at another path
Realm.open({
  path: 'anotherRealm.realm',
  schema: [CarSchema]
}).then(/* ... */);
```
###5.Schema版本 {#index}
打开Realm时可用的另一个选项是`schemaVersion`属性。当省略时，`schemaVersion`属性默认为0。在使用包含与之前规范不同的对象的Schema初始化现有Realm时，需要指定`schemaVersion`。如果`Schema`被更新并且`schemaVersion`不是之前的结构，将抛出异常。
```javascript
const PersonSchema = {
  name: 'Person',
  properties: {
    name: 'string'
  }
};

// schemaVersion默认是0
Realm.open({schema: [PersonSchema]});

const UpdatedPersonSchema = {
  /  // 因为schema名称相同, 所以以前的"Person"对象在Realm将会更新
  name: 'Person',
  properties: {
    name: 'string',
    dog:  'Dog'     // new property
  }
};

// 这将抛出异常，因为schema已经改变
// 和`schemaVersion`未指定
Realm.open({schema: [UpdatedPersonSchema]});

// 这将成功并将Realm更新到新的schema
Realm.open({schema: [UpdatedPersonSchema], schemaVersion: 1});
```
检索当前的Realmschema版本，可以使用`Realm.schemaVersion`方法。
```javascript
let currentVersion = Realm.schemaVersion(Realm.defaultPath);
```

### 6.迁移
在数据库工作时，数据模型将很可能随时间而变化。
当新的代码和Realm已存储在磁盘上的旧数据将不匹配时，使用新的schema打开现有的Realm时，将抛出异常，除非运行迁移。

```javascript
let PersonSchema = {
  name: 'Person',
  properties: {
    firstName: 'string',
    lastName: 'string',
    age: 'int'
  }
}
//更新数据模型，用name属性替换firstName和lastName：
let PersonSchema = {
  name: 'Person',
  properties: {
    name: 'string',
    age: 'int'
  }
}
```
###7.进行迁移
通过更新[Schema版本](#index)并定义可选的migration function来定义migration 和关联的schema版本。migration function提供将数据模型从以前的schema转换为新的schema所需的所有逻辑。当打开Realm时，只有在需要迁移时，才会将迁移函数应用于将Realm更新到给定的schema版本。

如果没有提供迁移函数，当更新到新的schemaVersion时，任何新的属性将自动添加并且旧的属性从数据库中删除。如果您需要在升级版本时更新旧的或填充的新属性，那么可以在迁移函数中执行此操作。
```javascript
Realm.open({
  schema: [PersonSchema],
  schemaVersion: 1,
  migration: (oldRealm, newRealm) => {
    // only apply this change if upgrading to schemaVersion 1
    
    if (oldRealm.schemaVersion < 1) {
      const oldObjects = oldRealm.objects('Person');
      const newObjects = newRealm.objects('Person');

      // loop through all objects and set the name property in the new schema
      for (let i = 0; i < oldObjects.length; i++) {
        newObjects[i].name = oldObjects[i].firstName + ' ' + oldObjects[i].lastName;
      }
    }
  }
}).then(realm => {
  const fullName = realm.objects('Person')[0].name;
});
```
迁移成功完成后，app可以像往常一样访问Realm及其所有对象。
###8.现行迁移
使用上述迁移模式，可能会在多个版本上迁移时遇到问题。如果用户跳过应用程序更新，并且在跳过的版本中属性已被更改多次，在这种情况下，需要编辑旧的迁移代码才能将数据从旧schema更新到最新schema。
可以通过顺序运行多个迁移来避免此问题，确保将数据库升级到每个先前版本，并运行关联的迁移代码。遵循这种模式，永远不需要修改旧的迁移代码，尽管您需要保留所有旧的schema和迁移模块以备将来使用。
```javascript
const schemas = [
  { schema: schema1, schemaVersion: 1, migration: migrationFunction1 },
  { schema: schema2, schemaVersion: 2, migration: migrationFunction2 },
  ...
]

// the first schema to update to is the current schema version
// since the first schema in our array is at
// let nextSchemaIndex = Math.max(0, Realm.schemaVersion(Realm.defaultPath));

let nextSchemaIndex = Realm.schemaVersion(Realm.defaultPath);
while (nextSchemaIndex < schemas.length) {
  const migratedRealm = new Realm(schemas[nextSchemaIndex++]);
  migratedRealm.close();
}

// open the Realm with the latest schema
Realm.open(schemas[schemas.length-1]);
```
###9. [相关API][1]
+ delete(object)
+ deleteAll()
+ deleteModel(name)
+ write(callback)

[1]: https://realm.io/docs/javascript/latest/api/Realm.html#delete
[2]: https://realm.io/docs/javascript/latest/#other-realms
[3]: https://realm.io/docs/javascript/latest/#migrations
[4]: https://realm.io/docs/javascript/latest/#sync
[5]: https://realm.io/docs/javascript/latest/api/Realm.html#~Configuration