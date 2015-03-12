# Getting Started - Key-Value Storage

last update at 2014/09/30

---

- [Overview](#HowToUseKeyValueStorage)
  - [Store Data](#HowToStoreData)
  - [Delete Data](#HowToDeleteData)
  - [Get Data](#HowToFetchData)

---


## <a name="HowToUseKeyValueStorage"> Overview </a>

Key-Value Storage can be used by using [FASStorage](../Specs/Spec-Storage.md/#FASStorage).
Data will be stored both on the Fresvii server, and in the local storage of the players device.  When the players device is offline, data will be stored only in the local storage. When the device is online, launching the app will trigger to sync the local data automatically with the Fresvii server data.


### <a name="HowToStoreData"> Store Data </a>
Store data by creating key-value data in `NSDictionary` type.
Data will be stored both on the Fresvii server, and in the local storage of the players device.

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
            // Error
            return;
        }

        // Success
    }];
}
```

### <a name="HowToDeleteData"> Delete Data </a>
Delete data by selecting the key of the data.
It will delete the data both form the Fresvii server, and the local storage of the players device.

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
            // Error
            return;
        }

        // Success
    }];
}
```

### <a name="HowToFetchData"> Get Data </a>
Get data value by selecting the key of the data.
It will preferentially get data from storage in the device. When the specific key could not be found in the device, it will search Fresvii server and return the result.

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
            // Error
            return;
        }

        // Success
        NSLog(@"Value : %@", response[key]);
    }];
}
```
