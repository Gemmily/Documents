### realm���ݿ�Ǩ��
---
###1.Realm
Realm��Realm�ƶ����ݿ�������ʵ���������Ǳ��صĻ�ͬ���ġ�
###2.��Realm
��Realmֻ��ͨ��ʵ����һ���µ�Realm������ִ�С������ö��󴫵ݸ����캯����
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
�й����ö����������ϸ��Ϣ�����[API����][5]�������һЩ�������ļ�������`schema`��������
+ `path`��ָ��[��һ��Realm·��][2]
+ `migration`�� [Ǩ��][3]
+  `sync`�� [ͬ������][4]�� ����Realm���������ͬ����Realm��
+  `inMemory`��Realm in-memory�򿪣� �Ҷ��󲻳־ã�һ��Realm���ر����ж������ʧ��
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
###3.Ĭ��Realm
ʹ��`Realm.defaultPath`ȫ�����Է��ʺ͸���Ĭ�ϵ�Realm·����
###4.����Realm
�ж��Realm�ڶ��λ�ó־û������õġ����磬������Realm�⣬��ϣ������һЩ������Ӧ�ó�����Realm�ļ��С�����ͨ���ڳ�ʼ��Realmʱָ��·��������ִ�д˲��������������Ӧ�ó����·������д���ĵ�Ŀ¼�С�
```javascript
// Open a realm at another path
Realm.open({
  path: 'anotherRealm.realm',
  schema: [CarSchema]
}).then(/* ... */);
```
###5.Schema�汾 {#index}
��Realmʱ���õ���һ��ѡ����`schemaVersion`���ԡ���ʡ��ʱ��`schemaVersion`����Ĭ��Ϊ0����ʹ�ð�����֮ǰ�淶��ͬ�Ķ����Schema��ʼ������Realmʱ����Ҫָ��`schemaVersion`�����`Schema`�����²���`schemaVersion`����֮ǰ�Ľṹ�����׳��쳣��
```javascript
const PersonSchema = {
  name: 'Person',
  properties: {
    name: 'string'
  }
};

// schemaVersionĬ����0
Realm.open({schema: [PersonSchema]});

const UpdatedPersonSchema = {
  /  // ��Ϊschema������ͬ, ������ǰ��"Person"������Realm�������
  name: 'Person',
  properties: {
    name: 'string',
    dog:  'Dog'     // new property
  }
};

// �⽫�׳��쳣����Ϊschema�Ѿ��ı�
// ��`schemaVersion`δָ��
Realm.open({schema: [UpdatedPersonSchema]});

// �⽫�ɹ�����Realm���µ��µ�schema
Realm.open({schema: [UpdatedPersonSchema], schemaVersion: 1});
```
������ǰ��Realmschema�汾������ʹ��`Realm.schemaVersion`������
```javascript
let currentVersion = Realm.schemaVersion(Realm.defaultPath);
```

### 6.Ǩ��
�����ݿ⹤��ʱ������ģ�ͽ��ܿ�����ʱ����仯��
���µĴ����Realm�Ѵ洢�ڴ����ϵľ����ݽ���ƥ��ʱ��ʹ���µ�schema�����е�Realmʱ�����׳��쳣����������Ǩ�ơ�

```javascript
let PersonSchema = {
  name: 'Person',
  properties: {
    firstName: 'string',
    lastName: 'string',
    age: 'int'
  }
}
//��������ģ�ͣ���name�����滻firstName��lastName��
let PersonSchema = {
  name: 'Person',
  properties: {
    name: 'string',
    age: 'int'
  }
}
```
###7.����Ǩ��
ͨ������[Schema�汾](#index)�������ѡ��migration function������migration �͹�����schema�汾��migration function�ṩ������ģ�ʹ���ǰ��schemaת��Ϊ�µ�schema����������߼�������Realmʱ��ֻ������ҪǨ��ʱ���ŻὫǨ�ƺ���Ӧ���ڽ�Realm���µ�������schema�汾��

���û���ṩǨ�ƺ����������µ��µ�schemaVersionʱ���κ��µ����Խ��Զ���Ӳ��Ҿɵ����Դ����ݿ���ɾ�����������Ҫ�������汾ʱ���¾ɵĻ����������ԣ���ô������Ǩ�ƺ�����ִ�д˲�����
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
Ǩ�Ƴɹ���ɺ�app����������һ������Realm�������ж���
###8.����Ǩ��
ʹ������Ǩ��ģʽ�����ܻ��ڶ���汾��Ǩ��ʱ�������⡣����û�����Ӧ�ó�����£������������İ汾�������ѱ����Ķ�Σ�����������£���Ҫ�༭�ɵ�Ǩ�ƴ�����ܽ����ݴӾ�schema���µ�����schema��
����ͨ��˳�����ж��Ǩ������������⣬ȷ�������ݿ�������ÿ����ǰ�汾�������й�����Ǩ�ƴ��롣��ѭ����ģʽ����Զ����Ҫ�޸ľɵ�Ǩ�ƴ��룬��������Ҫ�������оɵ�schema��Ǩ��ģ���Ա�����ʹ�á�
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
###9. [���API][1]
+ delete(object)
+ deleteAll()
+ deleteModel(name)
+ write(callback)

[1]: https://realm.io/docs/javascript/latest/api/Realm.html#delete
[2]: https://realm.io/docs/javascript/latest/#other-realms
[3]: https://realm.io/docs/javascript/latest/#migrations
[4]: https://realm.io/docs/javascript/latest/#sync
[5]: https://realm.io/docs/javascript/latest/api/Realm.html#~Configuration