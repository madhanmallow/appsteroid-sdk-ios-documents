# Notification Specifications

last update at 2014/10/7

---

## Introduction

プッシュ通知の設定や、通知イベントを取り扱うための機能に関する仕様書です。
デバイストークンをFresviiサーバーに設定するAPIや、特定のプッシュ通知を監視して通知を受けるようにする機能などが提供されています。
また、[FASCustomMessage](#FASCustomMessage)では、[FASStorage](Spec-Storage.md#FASStorage)と連携して、特定のユーザーにプッシュ通知を送ることが出来ます。
詳しくは[PushNotificationGetStarted](../GetStarted/GetStarted-PushNotification.md)を参照してください。

---

## Classes

|Class|Description|
|------|-----|
|[FASNotification](#FASNotification)|PushNotificationを取り扱うためのクラス |
|[FASEvent](#FASEvent)|PushNotificationを監視して通知を受け取るためのクラス |
|[FASObserver](#FASObserver)|[FASEvent](#FASEvent)で監視登録した際に作成されるクラス |

---

## APIs
### <a name="FASNotification"> FASNotification </a>
PushNotificationを取り扱うためのクラスです。

#### Constants
|Constant|Description|
|------|-----|
|[FASCertificateType](#FASNotification_FASCertificateType)|APNs証明書の種類 |

##### <a name="FASNotification_FASCertificateType"> FASCertificateType </a>
APNs証明書の種類。

```obj-c
typedef NS_ENUM(NSInteger, FASCertificateType)
{
    FASCertificateTypeDevelopment = 0,
    FASCertificateTypeProduction  = 1
};
```

* Development: 開発用証明書
* Production: 本番用証明書

#### Class Methods

|Method|Description|
|------|-----|
|[addDeviceToken:completion:](#FASNotification.addDeviceTokencompletion) |指定したデバイストークンを登録します。 |
|[addDeviceToken:certificateType:completion:](#FASNotification_addDeviceTokencertificateTypecompletion) |証明書の種類を指定でデバイストークンを登録します。 |
|[deleteDeviceToken:completion:](#FASNotification.deleteDeviceTokencompletion) |指定したデバイストークンを削除します。 |
|[fetchNotificationMessageWithId:completion:](#FASNotification.fetchNotificationMessageWithIdcompletion) |PushNotificateionの詳細情報を取得してきます。 |
|[handleDidReceiveRemoteNotification:](#FASNotification.handleDidReceiveRemoteNotification) |AppSteroidに関するPushNotificateionを取り扱います。|
|[allowsToHandlePushNotification:](#FASNotification.allowsToHandlePushNotification) |AppSteroidのPushNotificationからアプリを起動した際、自動でその通知に関する機能を取り扱うかどうかを設定します。 |
|[isAllowedToHandlePushNotification](#FASNotification.isAllowedToHandlePushNotification) |AppSteroidに関するPushNotificationを取り扱うかどうか返却します。 |

##### <a name="FASNotification.addDeviceTokencompletion"> addDeviceToken:completion: </a>
指定したデバイストークンを登録します。

\+ (void)addDeviceToken:(NSData *)deviceToken
             completion:(FASCompletionHandler)completion;

* Parameters
	* deviceToken
		* PushNotificationを受け取るために必要なデバイストークン。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (void)application:(UIApplication *)application
didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
	[FASNotification addDeviceToken:deviceToken
	                     completion:^(NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASNotification_addDeviceTokencertificateTypecompletion"> addDeviceToken:certificateType:completion: </a>
証明書の種類を指定でデバイストークンを登録します。証明書の種類については [開発モードについて](./DevelopmentMode.md) も合わせてご確認ください。

\+ (void)addDeviceToken:(NSData *)deviceToken
				certificateType:(FASCertificateType)certificateType
             completion:(FASCompletionHandler)completion;

* Parameters
	* deviceToken
		* PushNotificationを受け取るために必要なデバイストークン。
	* certificateType
		* ビルド環境でのAPNs証明書の種類
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (void)application:(UIApplication *)application
didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
	[FASNotification addDeviceToken:deviceToken
	                     completion:^(NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASNotification.deleteDeviceTokencompletion"> deleteDeviceToken: </a>
指定したデバイストークンを削除します。

\+ (void)deleteDeviceToken:(NSData *)deviceToken
                completion:(FASCompletionHandler)completion;

* Parameters
	* deviceToken
		* PushNotificationを受け取るために必要なデバイストークン。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASNotification deleteDeviceToken:deviceToken
                            completion:^(NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASNotification.fetchNotificationMessageWithIdcompletion"> fetchNotificationMessageWithId:completion: </a>
Fresviiサーバー経由のPushNotificateionのuserInfoに格納されているidの値から詳細情報を取得してきます。

\+ (void)fetchNotificationMessageWithId:(NSString *)messageId
                             completion:(FASResponseCompletionHandler)completion;

* Parameters
	* messageId
		* userInfoに格納されているidの値を設定します。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (void)fetchNotificationMessageWithMessageId:(NSString *)messageId
{
    [FASNotification fetchNotificationMessageWithId:messageId
                                         completion:^(id response, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASNotification.handleDidReceiveRemoteNotification"> handleDidReceiveRemoteNotification: </a>
Fresviiサーバー経由のPushNotificateionをハンドリングします。
特に、[FASEvent](#FASEvent)を利用する際はこのメソッドの実装は必須になります。

\+ (void)handleDidReceiveRemoteNotification:(NSDictionary *)userInfo;

* Parameters
	* userInfo
		* PushNotificateionを受信するためのメソッド`application:didReceiveRemoteNotification:`または、`application:didReceiveRemoteNotification:fetchCompletionHandler:`で受け取れるパラメータをそのまま利用します。

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (void)application:(UIApplication *)application
didReceiveRemoteNotification:(NSDictionary *)userInfo
{
    [FASNotification handleDidReceiveRemoteNotification:userInfo];
}
```

##### <a name="FASNotification.allowsToHandlePushNotification"> allowsToHandlePushNotification: </a>
AppSteroidのPushNotificationをバックグラウンドで受信して起動した際に、自動でその通知に関する機能を取り扱うかどうかを設定します。デフォルトでは`YES`になっています。

\+ (void)allowsToHandlePushNotification:(BOOL)boolean;

* Parameters
	* boolean
		* 通知に関する機能を取り扱うかどうかの設定

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
	…
	…
    [FASNotification allowsToHandlePushNotification:YES];
    …
    …
}
```

##### <a name="FASNotification.isAllowedToHandlePushNotification"> isAllowedToHandlePushNotification </a>
AppSteroidに関するPushNotificationを取り扱うかどうか返却します。

\+ (BOOL)isAllowedToHandlePushNotification;

### <a name="FASEvent"> FASEvent </a>
AppSteroidのPushNotificationを監視し、指定したpathとactionに通知を行うためのクラスです。

#### Constants

|Constant|Description|
|------|-----|
|[FASEventHandler](#FASEvent.FASEventHandler) |指定されているpathとactionに対応するPushNotificationを受け取ったときに実行されるブロックオブジェクトです。 |

##### <a name="FASEvent.FASEventHandler"> FASEventHandler </a>
指定されているpathとactionに対応するPushNotificationを受け取ったときに実行されるブロックオブジェクトです。


typedef void (^FASEventHandler)(NSDictionary *params);

* Parameters
	* params
		* 通知に関する詳細が`NSDictionary`型で格納されています。

#### Class Method

|Method|Description|
|------|-----|
|[observeEventWithDelegate:path:action:](#FASEvent.observeEventWithDelegatepathaction) |デリゲートメソッド経由で通知を受け取るために監視登録します。 |
|[observeEventWithPath:action:eventHandler:](#FASEvent.observeEventWithPathactioneventHandler) |ブロックオブジェクト経由で通知を受け取るために監視登録します。 |
|[unobserve:](#FASEvent.unobserve)|監視を解除します。 |

##### <a name="FASEvent.observeEventWithDelegatepathaction"> observeEventWithDelegate:path:action: </a>
デリゲートメソッド経由で通知を受け取るために監視登録します。

\+ (FASObserver \*)observeEventWithDelegate:(id<FASEventDelegate>)delegate
                                       path:(NSString \*)path
                                     action:(NSString \*)action

* Parameters
	* delegate
		* [FASEventDelegate](#FASEventDelegate)で定義されているデリゲートメソッドを受け取るためのクラスを指定します。
	* path
		* PushNotificationが送られる切っ掛けとなった機能の名前を指定します。`userInfo`の`resource`と対応しています。
	* action
		* PushNotificationが送られる切っ掛けとなった機能の動作の名前を指定します。`userInfo`の`action`と対応しています。

* Return Value
	* [FASObserver](#FASObserver)オブジェクト。[unobserve:](#FASEvent.unobserve)する際に利用します。

Sample

```
#import <AppSteroid/FASEvent.h>

	…
	…

@implementation FASEventViewController
{
    FASObserver *_observer;
}

- (void)viewDidLoad
{
	…
	…

	_observer = [FASEvent observeEventWithDelegate:self
	                                          path:@"user/friendship/request"
	                                        action:@"created"];
}

- (void)created:(NSDictionary *)params
{
	// 指定したpathとactionのPushNotificationを受け取ったら実行されます。
}
```

##### <a name="FASEvent.observeEventWithPathactioneventHandler"> observeEventWithPath:action:eventHandler: </a>
ブロックオブジェクト経由で通知を受け取るために監視登録します。

\+ (FASObserver \*)observeEventWithPath:(NSString \*)path
                                 action:(NSString \*)action
                           eventHandler:(FASEventHandler)handler

* Parameters
	* path
		* PushNotificationが送られる切っ掛けとなった機能の名前を指定します。`userInfo`の`resource`と対応しています。
	* action
		* PushNotificationが送られる切っ掛けとなった機能の動作の名前を指定します。`userInfo`の`action`と対応しています。
	* handler
		* PushNotificationが通知を受け取ったときに実行されるブロックオブジェクトです。

* Return Value
	* [FASObserver](#FASObserver)オブジェクト。[unobserve:](#FASEvent.unobserve)する際に利用します。


Sample

```
#import <AppSteroid/FASEvent.h>

	…
	…

@implementation FASEventViewController
{
    FASObserver *_observer;
}

- (void)viewDidLoad
{
	…
	…

	_observer = [FASEvent observeEventWithPath:@"user/friendship/request"
                                        action:@"created"
                                  eventHandler:^(NSDictionary *params)
    {
        // 指定したpathとactionのPushNotificationを受け取ったら実行されます。
    }];
}
```
##### <a name="FASEvent.unobserve"> unobserve: </a>
イベント監視を解除します。

\+ (void)unobserve:(FASObserver \*)observer

* Parameters
	* observer
		* 監視登録したときに返ってきたオブジェクトを指定します。

Sample

```
#import <AppSteroid/FASEvent.h>

	…
	…

@implementation FASEventViewController
{
    FASObserver *_observer;
}

- (void)dealloc
{
	[FASEvent unobserve:_observer];
}
```

#### <a name="FASEventDelegate"> FASEventDelegate </a>
PushNotificationを受け取った際に呼ばれるデリゲートメソッド。
`observeEventWithDelegate:path:action:`で監視登録を行った際にこのデリゲートメソッドを利用出来ます。

|Method|Description|
|------|-----|
|[created:](#FASEventDelegate.created) |`action`で`created`が指定された際に呼ばれるメソッドです。 |
|[updated:](#FASEventDelegate.updated) |`action`で`updated`が指定された際に呼ばれるメソッドです。 |
|[joined:](#FASEventDelegate.joined) |`action`で`joined`が指定された際に呼ばれるメソッドです。 |
|[accepted:](#FASEventDelegate.accepted) |`action`で`accepted`が指定された際に呼ばれるメソッドです。 |

##### <a name="FASEventDelegate.created"> created: </a>
PushNotificationのパラメータ`userInfo`の`action`で`created`が指定された際に呼ばれるメソッドです。

\- (void)created:(NSDictionary *)params

* Parameters
	* params
		* PushNotificationを受け取った時に得られるuserInfoが格納されています。

##### <a name="FASEventDelegate.updated"> updated: </a>
PushNotificationのパラメータ`userInfo`の`action`で`updated`が指定された際に呼ばれるメソッドです。

\- (void)updated:(NSDictionary *)params

* Parameters
	* params
		* PushNotificationを受け取った時に得られるuserInfoが格納されています。

##### <a name="FASEventDelegate.joined"> joined: </a>
PushNotificationのパラメータ`userInfo`の`action`で`joined`が指定された際に呼ばれるメソッドです。

\- (void)joined:(NSDictionary *)params

* Parameters
	* params
		* PushNotificationを受け取った時に得られるuserInfoが格納されています。

##### <a name="FASEventDelegate.accepted"> accepted: </a>
PushNotificationのパラメータ`userInfo`の`action`で`accepted`が指定された際に呼ばれるメソッドです。

\- (void)accepted:(NSDictionary *)params

* Parameters
	* params
		* PushNotificationを受け取った時に得られるuserInfoが格納されています。

### <a name="FASObserver"> FASObserver </a>
[FASEvent](#FASEvent)で監視登録した際に作成されるクラスです。監視を解除するときに利用します。
