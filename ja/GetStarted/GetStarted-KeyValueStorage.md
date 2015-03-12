# Getting Started - Key-Value Storage

last update at 2014/10/7

---

- [ストレージの利用](#HowToUseKeyValueStorage)
  - [データの保存方法](#HowToStoreData)
  - [データの削除方法](#HowToDeleteData)
  - [データの取得方法](#HowToFetchData)

---


## <a name="HowToUseKeyValueStorage"> ストレージの利用 </a>

AppSteroidが提供するKey-Valueストレージの利用方法を説明します。
[FASStorage](../Specs/Spec-Storage.md/#FASStorage)を利用することで利用可能になります。
データはFresviiサーバーと端末内のストレージの両方に保存され、オフライン時でもデータを保存することが出来ます。データの同期はオンライン時にアプリケーションを立ち上げた際に自動で行います。

### <a name="HowToStoreData"> データの保存方法 </a>
`NSDictionary`型でkey-valueデータを作成し、データを保存します。
Fresviiサーバーと端末内のストレージの両方にデータは保存されます。

Sample

```
#import <AppSteroid/FASStorage.h>

  …
  …


- (IBAction)pushedAddButton:(id)sender
{
    NSDictionary *data = @{@"key" : @"value"};
    [FASStorage addData:data
             completion:^(NSError *error)
    {
        if (error)
        {
            // エラー
            return;
        }

        // 成功
    }];
}
```

### <a name="HowToDeleteData"> データの削除方法 </a>
削除したいデータのキーを指定してデータを削除します。
Fresviiサーバーと端末内のストレージの両方からデータを削除します。

Sample

```
#import <AppSteroid/FASStorage.h>

  …
  …


- (IBAction)pushedDeleteButton:(id)sender
{
    [FASStorage deleteDataWithKey:@"key"
                       completion:^(NSError *error)
    {
        if (error)
        {
            // エラー
            return;
        }

        // 成功
    }];
}
```

### <a name="HowToFetchData"> データの取得方法 </a>
取得したいデータのキーを指定して値を取得します。
データの取得は端末内のストレージを優先的に取得してきます。端末内に対象のキーが無かった場合はFresviiサーバーへ検索を行い結果を返却します。

Sample

```
#import <AppSteroid/FASStorage.h>

  …
  …


- (IBAction)pushedFetchButton:(id)sender
{
    NSString *key = @"key";
    [FASStorage fetchDataWithKey:key
                      completion:^(id response, NSError *error)
    {
        if (error)
        {
            // エラー
            return;
        }

        // 成功
        NSLog(@"Value : %@", response[key]);
    }];
}
```
