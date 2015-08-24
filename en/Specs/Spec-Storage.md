# Key-Value Storage Specifications

last update at 2014/09/30

---

## Introduction

Data will be stored in JSON format. Save data will be stored on both AppSteroid server and iOS device.
Check [KeyValueStorageGetStarted](../GetStarted/GetStarted-KeyValueStorage.md) to see. how to use.

---

## Classes

|Class|Description|
|------|-----|
|[FASStorage](#FASStorage)|Class to operate Key-Value Storage provided by AppSteroid. |

---

## APIs
### <a name="FASStorage"> FASStorage </a>
Class to operate Key-Value Storage provided by AppSteroid.

#### Class Methods

|Method|Description|
|------|-----|
|[fetchDataWithCompletion:](#FASStorage.fetchDataWithCompletion) |Get all data |
|[fetchDataWithKeyPrefix:completion:](#FASStorage.fetchDataWithKeyPrefixcompletion) |Get all data with included key prefix. |
|[fetchDataWithKey:completion:](#FASStorage.fetchDataWithKeycompletion) |Get all data with a specified key name. |
|[fetchDataKeysWithCompletion:](#FASStorage.fetchDataKeysWithCompletion) |Get key name for all data. |
|[addData:completion:](#FASStorage.addDatacompletion) |Save data specified in NSDictionary on AppSteroid server. |
|[deleteDataWithKey:completion:](#FASStorage.deleteDataWithKeycompletion) |Delete all data with a specified key name. |

##### <a name="FASStorage.fetchDataWithCompletion"> fetchDataWithCompletion: </a>
Get all data

\+ (void)fetchDataWithCompletion:(FASResponseCompletionHandler)completion;

* Parameters
	* completion
		* Block object to be executed when the process is completed.

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
            // It will be called when the process is completed.
        }];
}
```

##### <a name="FASStorage.fetchDataWithKeyPrefixcompletion"> fetchDataWithKeyPrefix:completion: </a>
Get all data with included key prefix.

\+ (void)fetchDataWithKeyPrefix:(NSString *)prefix
                     completion:(FASResponseCompletionHandler)completion;

* Parameters
	* prefix
		* Key prefix. It will full search when it is nil.
	* completion
		* Block object to be executed when the process is completed.

Response example

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
        // It will be called when the process is completed
    }];
}
```

##### <a name="FASStorage.fetchDataWithKeycompletion"> fetchDataWithKey:completion: </a>
Get all data with a specified key name

\+ (void)fetchDataWithKey:(NSString *)keyName
               completion:(FASResponseCompletionHandler)completion;

* Parameters
	* keyName
		* Key name
	* completion
		* Block object to be executed when the process is completed.

Response

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
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASStorage.fetchDataKeysWithCompletion"> fetchDataKeysWithCompletion: </a>
Get key name for all data stored on AppSteroid.

\+ (void)fetchDataKeysWithCompletion:(FASResponseCompletionHandler)completion;

* Parameters
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASStorage.addDatacompletion"> addData:completion: </a>
Save data specified in NSDictionary on AppSteroid server.

\+ (void)addData:(NSDictionary *)data
      completion:(void(^)(NSError *error))completion;

* Parameters
	* data
		* Key-Value data. Set with NSDictionary format.
		   Example) {"hoge": {"foo": "bar"}, "key": "value"}
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASStorage.deleteDataWithKeycompletion"> deleteDataWithKey:completion: </a>
Delete all data with a specified key name.

\+ (void)deleteDataWithKey:(NSString *)keyName
                completion:(void(^)(NSError *error))completion;

* Parameters
	* keyName
		* Key name
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed.
    }];
}
```
