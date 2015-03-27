# Message Specifications

last update at 2015/2/26

---

## Introduction

メッセージに関する機能の仕様書です。
Fresviiコンソールから送信されるダイレクトメッセージの操作に関するクラスと特定の相手にプッシュ通知を送信する機能に関するクラスが記載されています。

---

## Classes

|Class|Description|
|------|-----|
|[FASDirectMessage](#FASDirectMessage)|Fresviiコンソールから送信されるダイレクトメッセージの操作に関するクラス |
|[FASCustomMessage](#FASCustomMessage)|特定の相手にプッシュ通知を送信する機能に関するクラス |

---

### <a name="FASDirectMessage"> FASDirectMessage </a>

#### Constants

|Constant|Description|
|------|-----|
|[FASDirectMessageCompletionHandler](#FASDirectMessage.FASDirectMessageCompletionHandler)|ダイレクトメッセージ受信処理を行った際に利用されるブロックオブジェクト |
|[FASDirectMessagesCompletionHandler](#FASDirectMessage.FASDirectMessagesCompletionHandler)|複数のダイレクトメッセージ取得処理を行った際に利用されるブロックオブジェクト |

##### <a name="FASDirectMessage.FASDirectMessageCompletionHandler"> FASDirectMessageCompletionHandler </a>
ダイレクトメッセージ受信処理を行った際に利用されるブロックオブジェクト

typedef void (^FASDirectMessageCompletionHandler)(FASDirectMessage *directMessage, NSError *error);

* Parameters
	* directMessage
		* [FASDirectMessage](#FASDirectMessage)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASDirectMessage.FASDirectMessagesCompletionHandler"> FASDirectMessagesCompletionHandler </a>
複数のダイレクトメッセージ取得処理を行った際に利用されるブロックオブジェクト

typedef void (^FASDirectMessagesCompletionHandler)(NSArray *directMessages, FASPagingMeta *meta, NSError *error);

* Parameters
	* directMessages
		* 複数の[FASDirectMessage](#FASDirectMessage)がNSArrayに格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[directMessageId](#FASDirectMessage.directMessageId)|ダイレクトメッセージID |
|[subject](#FASDirectMessage.subject)|タイトル |
|[text](#FASDirectMessage.text)|本文 |
|[createdAt](#FASDirectMessage.createdAt)|ダイレクトメッセージが作成された時刻 |

##### <a name="FASDirectMessage.directMessageId"> directMessageId </a>
ダイレクトメッセージID

@property (nonatomic, readonly) NSString *directMessageId;

##### <a name="FASDirectMessage.subject"> subject </a>
タイトル

@property (nonatomic, readonly) NSString *subject;

##### <a name="FASDirectMessage.text"> text </a>
本文

@property (nonatomic, readonly) NSString *text;

##### <a name="FASDirectMessage.createdAt"> createdAt </a>
ダイレクトメッセージが作成された時刻

@property (nonatomic, readonly) NSDate *createdAt;

#### Class Method

|Method|Description|
|------|-----|
|[fetchDirectMessagesWithPage:completion:](#FASDirectMessage.fetchDirectMessagesWithPage) |指定したページのダイレクトメッセージを一覧で取得します。 |
|[fetchDirectMessagesWithPage:onlyUnread:completion:](#FASDirectMessage.fetchDirectMessagesWithPage) |指定したページのダイレクトメッセージを一覧で取得します。`unread`を`YES`にした場合は未読メッセージのみを取得します。 |
|[fetchDirectMessageWithId:completion:](#FASDirectMessage.fetchDirectMessagesWithPage) |指定したidのダイレクトメッセージを取得します。 |

##### <a name="FASDirectMessage.fetchDirectMessagesWithPage"> fetchDirectMessagesWithPage:completion: </a>
指定したページのダイレクトメッセージを一覧で取得します。

\+ (void)fetchDirectMessagesWithPage:(NSUInteger)page
                          completion:(FASDirectMessagesCompletionHandler)completion;

* Parameters
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

##### <a name="FASDirectMessage.fetchDirectMessagesWithPage"> fetchDirectMessagesWithPage:onlyUnread:completion: </a>
指定したページのダイレクトメッセージを一覧で取得します。
`unread`を`YES`にした場合は未読メッセージのみを取得します。

\+ (void)fetchDirectMessagesWithPage:(NSUInteger)page
                          onlyUnread:(BOOL)unread
                          completion:(FASDirectMessagesCompletionHandler)completion;

* Parameters
	* page
		* ページ番号
	* unread
		* `YES`を指定した場合は未読メッセージのみ取得します。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

##### <a name="FASDirectMessage.fetchDirectMessagesWithPage"> fetchDirectMessageWithId:completion: </a>
指定したidのダイレクトメッセージを取得します。

\+ (void)fetchDirectMessageWithId:(NSString *)messageId
                       completion:(FASDirectMessageCompletionHandler)completion;

* Parameters
	* messageId
		* ダイレクトメッセージのID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

### <a name="FASCustomMessage"> FASCustomMessage </a>
特定の相手にプッシュ通知を送信する機能に関するクラス

#### Constants

|Constant|Description|
|------|-----|
|[FASCustomMessageCompletionHandler](#FASCustomMessage.FASCustomMessageCompletionHandler)|メッセージ送信処理を行った際に利用されるブロックオブジェクト |
|[FASCustomMessagesCompletionHandler](#FASCustomMessage.FASCustomMessagesCompletionHandler)|複数のメッセージ取得処理を行った際に利用されるブロックオブジェクト |

##### <a name="FASCustomMessage.FASCustomMessageCompletionHandler"> FASCustomMessageCompletionHandler </a>
メッセージ送信処理を行った際に利用されるブロックオブジェクト

typedef void (^FASCustomMessageCompletionHandler)(FASCustomMessage *message, NSError *error);

* Parameters
	* message
		* [FASCustomMessage](#FASCustomMessage)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASCustomMessage.FASCustomMessagesCompletionHandler"> FASCustomMessagesCompletionHandler </a>
複数のメッセージ取得処理を行った際に利用されるブロックオブジェクト

typedef void (^FASCustomMessagesCompletionHandler)(NSArray *messages, FASPagingMeta *meta, NSError *error);

* Parameters
	* message
		* [FASCustomMessage](#FASCustomMessage)が格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[messageId](#FASCustomMessage.messageId)|メッセージID |
|[action](#FASCustomMessage.action)|メッセージのアクション名 |
|[params](#FASCustomMessage.params)|メッセージのパラメータ |
|[createdAt](#FASCustomMessage.createdAt)|メッセージが作成された時刻 |

##### <a name="FASCustomMessage.messageId"> messageId </a>
メッセージID

@property (nonatomic, readonly) NSString *messageId;

##### <a name="FASCustomMessage.action"> action </a>

@property (nonatomic, readonly) NSString *action;

##### <a name="FASCustomMessage.params"> params </a>

@property (nonatomic, readonly) NSDictionary *params;

##### <a name="FASCustomMessage.createdAt"> createdAt </a>

@property (nonatomic, readonly) NSDate *createdAt;

#### Class Method

|Method|Description|
|------|-----|
|[sendMessageWithChannelName:action:completion:](#FASCustomMessage.sendMessageWithChannelNameactioncompletion) |チャンネル名とアクション名を指定してメッセージを送ります。 |
|[sendMessageWithChannelName:action:channelParams:params:subject:sound:apnsEnabled:gcmEnabled:completion:](#FASCustomMessage.sendMessageWithChannelNameactionchannelParamsparamssubjectsoundapnsEnabledgcmEnabledcompletion) |チャンネル名とアクション名、その他パラメータを指定してメッセージを送ります。 |
|[fetchMessagesWithPage:completion:](#FASCustomMessage.fetchMessagesWithPagecompletion) |送信されたメッセージ一覧を取得します。 |
|[fetchMessagesWithPage:createdAt:completion:](#FASCustomMessage.fetchMessagesWithPagecreatedAtcompletion) |指定日時以降に送信されたメッセージ一覧を取得します。 |

##### <a name="FASCustomMessage.sendMessageWithChannelNameactioncompletion"> sendMessageWithChannelName:action:completion: </a>
チャンネル名とアクション名を指定してiOS,Android両端末にメッセージを送ります。

\+ (void)sendMessageWithChannelName:(NSString *)channelName
                             action:(NSString *)action
                         completion:(FASCustomMessageCompletionHandler)completion;

* Parameters
	* channelName
		* チャンネル名
	* action
		* メッセージのアクション名
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

Sample

```
#import <AppSteroid/FASCustomMessage.h>

	…
	…

- (IBAction)pushedSendButton:(id)sender
{
    [FASCustomMessage sendMessageWithChannelName:@"level"
                                          action:@"created"
                                      completion:^(FASCustomMessage *message, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASCustomMessage.sendMessageWithChannelNameactionchannelParamsparamssubjectsoundapnsEnabledgcmEnabledcompletion"> sendMessageWithChannelName:action:channelParams:params:subject:sound:apnsEnabled:gcmEnabled:completion: </a>
チャンネル名とアクション名等を指定してメッセージを送ります。

\+ (void)sendMessageWithChannelName:(NSString *)channelName
                             action:(NSString *)action
                      channelParams:(id)channelParams
                             params:(id)params
                            subject:(NSString *)subject
                              sound:(NSString *)sound
                        apnsEnabled:(BOOL)apnsEnabled
                         gcmEnabled:(BOOL)gcmEnabled
                         completion:(FASCustomMessageCompletionHandler)completion;

* Parameters
	* channelName
		* チャンネル名
	* action
		* メッセージのアクション名
	* channelParams
		* チャンネルのクエリに指定したバインド変数の値をJSON形式になるように`NSDictionary`型か`NSArray`型で指定します。
	* params
		* プッシュメッセージのカスタムデータをJSON形式になるように`NSDictionary`型か`NSArray`型で指定します。
	* subject
		* プッシュメッセージの件名
	* sound
		* プッシュメッセージのサウンドファイル名。未指定の場合は無音になります。
	* apnsEnabled
		* iOS端末へのプッシュ配信を行うかどうかを指定します。`YES`を指定すると通知を行います。
	* gcmEnabled
		* Android端末へのプッシュ配信を行うかどうかを指定します。`YES`を指定すると通知を行います。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

Sample

```
#import <AppSteroid/FASCustomMessage.h>

	…
	…

- (IBAction)pushedSendButton:(id)sender
{
    [FASCustomMessage sendMessageWithChannelName:@"level"
                                          action:@"created"
                                   channelParams:channelParams
                                          params:params
                                         subject:_levelLabel.text
                                           sound:@"default"
                                     apnsEnabled:YES
                                      gcmEnabled:YES
                                      completion:^(FASCustomMessage *message, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASCustomMessage.fetchMessagesWithPagecompletion"> fetchMessagesWithPage:completion: </a>
送信されたメッセージ一覧を取得します。

\+ (void)fetchMessagesWithPage:(NSUInteger)page
                    completion:(FASCustomMessagesCompletionHandler)completion;

* Parameters
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

Sample

```
#import <AppSteroid/FASCustomMessage.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASCustomMessage fetchMessagesWithPage:1
                                 completion:^(NSArray *messages, FASPagingMeta *meta, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASCustomMessage.fetchMessagesWithPagecreatedAtcompletion"> fetchMessagesWithPage:createdAt:completion: </a>
指定日時以降に送信されたメッセージ一覧を取得します。

\+ (void)fetchMessagesWithPage:(NSUInteger)page
                     createdAt:(NSDate *)createdDate
                    completion:(FASCustomMessagesCompletionHandler)completion;

* Parameters
	* page
		* ページ番号
	* createdAt
		* メッセージ作成日時。指定日時以降に作成されたメッセージを取得します。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

Sample

```
#import <AppSteroid/FASCustomMessage.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    // 一時間前の通知一覧を取得する。
    NSDate *date = [[NSDate date] dateByAddingTimeInterval:-3600];
    [FASCustomMessage fetchMessagesWithPage:1
                                  createdAt:date
                                 completion:^(NSArray *messages, FASPagingMeta *meta, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```
