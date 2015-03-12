# Key-Value Storage Specifications

last update at 2014/10/7

---

## Introduction

JSON形式でデータを保存します。保存されたデータはiOSの端末とFresviiのサーバーに保存されます。
利用方法は[KeyValueStorageGetStarted](../GetStarted/GetStarted-KeyValueStorage.md)を参照してください。
また、[FASCustomMessage](NotificationSpec.md#FASCustomMessage)と連携して特定の値を持っているユーザーを絞り込んでプッシュ通知を送ることも可能です。詳しくは[PushNotificationGetStarted](../GetStarted/GetStarted-PushNotification.md)を参照してください。

---

## Classes

|Class|Description|
|------|-----|
|[FASStorage](#FASStorage)|AppSteroidが提供するKey-Value Storageの操作に関するクラス |

---

## APIs
### <a name="FASStorage"> FASStorage </a>
AppSteroidが提供するKey-Value Storageを利用するためのクラスです。

#### Class Methods

|Method|Description|
|------|-----|
|[fetchDataWithCompletion:](#FASStorage.fetchDataWithCompletion) |すべてのデータを取得します。 |
|[fetchDataWithKeyPrefix:completion:](#FASStorage.fetchDataWithKeyPrefixcompletion) |prefixに当てはまるキーのすべてのデータを取得します。 |
|[fetchDataWithKey:completion:](#FASStorage.fetchDataWithKeycompletion) |指定したキー名のデータを取得します。 |
|[fetchDataKeysWithCompletion:](#FASStorage.fetchDataKeysWithCompletion) |すべてのデータのキー名を取得します。 |
|[addData:completion:](#FASStorage.addDatacompletion) |NSDictionaryで指定したデータをFresviiサーバーに保存します。 |
|[deleteDataWithKey:completion:](#FASStorage.deleteDataWithKeycompletion) |指定したキー名のデータを削除します。 |

##### <a name="FASStorage.fetchDataWithCompletion"> fetchDataWithCompletion: </a>
すべてのデータを取得します。

\+ (void)fetchDataWithCompletion:(FASResponseCompletionHandler)completion;

* Parameters
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Response例

```
[
	{
		"created_at":"2014-04-06 11:57:48 +0000",
        "key":"key1",
        "updated_at":"2014-04-06 11:57:48 +0000",
        "value":"value1"
    },
    {
        "created_at":"2014-04-06 11:57:57 +0000",
        "key":"key2",
        "updated_at":"2014-04-06 11:57:57 +0000",
        "value":"value2"
    },
    {
        "created_at":"2014-04-06 12:10:55 +0000",
        "key":"foo",
        "updated_at":"2014-04-06 12:10:55 +0000",
        "value":"bar"
    }
]
```

Sample

```
#import <AppSteroid/FASStorage.h>

	…
	…

- (IBAction)pushedFetchAllButton:(id)sender
{
        [FASStorage fetchDataWithCompletion:^(id response, NSError *error)
        {
            // 処理が完了したら呼ばれます。
        }];
}
```

##### <a name="FASStorage.fetchDataWithKeyPrefixcompletion"> fetchDataWithKeyPrefix:completion: </a>
prefixに当てはまるキーのすべてのデータを取得します。

\+ (void)fetchDataWithKeyPrefix:(NSString *)prefix
                     completion:(FASResponseCompletionHandler)completion;

* Parameters
	* prefix
		* キーのプレフィックス。nilにすると全検索になります。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Response例

```
[
	{
        "created_at":"2014-04-06 12:10:55 +0000",
        "key":"foo",
        "updated_at":"2014-04-06 12:10:55 +0000",
        "value":"bar"
	}
]
```

Sample

```
#import <AppSteroid/FASStorage.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    NSString *prefix = @"f";
	[FASStorage fetchDataWithKeyPrefix:prefix
	                        completion:^(id response, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASStorage.fetchDataWithKeycompletion"> fetchDataWithKey:completion: </a>
指定したキー名のデータを取得します。

\+ (void)fetchDataWithKey:(NSString *)keyName
               completion:(FASResponseCompletionHandler)completion;

* Parameters
	* keyName
		* キーの名前。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Response例

```
{
	"created_at":"2014-04-06 11:57:48 +0000",
	"key":"key1",
    "updated_at":"2014-04-06 11:57:48 +0000",
    "value":"value1"
}
```

Sample

```
#import <AppSteroid/FASStorage.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    NSString *keyName = @"foo";
	[FASStorage fetchDataWithKey:keyName
                      completion:^(id response, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASStorage.fetchDataKeysWithCompletion"> fetchDataKeysWithCompletion: </a>
Fresviiに保存されているすべてのデータのキー名を取得します。

\+ (void)fetchDataKeysWithCompletion:(FASResponseCompletionHandler)completion;

* Parameters
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Response例

```
[
    "key1",
    "key2",
    "foo"
]
```

Sample

```
#import <AppSteroid/FASStorage.h>

	…
	…

- (IBAction)pushedFetchAllKeysButton:(id)sender
{
    [FASStorage fetchDataKeysWithCompletion:^(id response, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASStorage.addDatacompletion"> addData:completion: </a>
NSDictionaryで指定したデータをFresviiサーバーに保存します。

\+ (void)addData:(NSDictionary *)data
      completion:(void(^)(NSError *error))completion;

* Parameters
	* data
		* Key-Valueデータ。NSDictionaryの形式で設定します。
		   例) {"hoge": {"foo": "bar"}, "key": "value"}
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASStorage.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    NSDictionary *data = @{@"foo" : @"bar"};
    [FASStorage addData:data
             completion:^(NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASStorage.deleteDataWithKeycompletion"> deleteDataWithKey:completion: </a>
指定したキー名のデータを削除します。

\+ (void)deleteDataWithKey:(NSString *)keyName
                completion:(void(^)(NSError *error))completion;

* Parameters
	* keyName
		* キーの名前。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASStorage.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    NSString *keyName = @"foo";
    [FASStorage deleteDataWithKey:keyName
                       completion:^(NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```
