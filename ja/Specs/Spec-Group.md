# Group Specifications

last update at 2015/7/7

---

## Introduction

グループチャットに関する機能の仕様書です。
グループの作成、メンバーの追加、メッセージの送信などの機能が提供されています。
また、AppSteroidが提供するグループチャットのGUIを表示することも出来ます。ビューの表示方法は[GroupGetStarted](../GetStarted/GetStarted-GroupChat.md)を参照してください。

---

## Classes

|Class|Description|
|------|-----|
|[FASGroup](#FASGroup)|グループモデルクラス |
|[FASGroupMember](#FASGroupMember)|グループメンバーモデルクラス |
|[FASGroupMessage](#FASGroupMessage)|グループメッセージモデルクラス |
|[FASSticker](#FASSticker)|グループメッセージ用ステッカーモデルクラス |
|[FASStickerSet](#FASStickerSet)|グループメッセージ用ステッカーセットモデルクラス |

---

## APIs
### <a name="FASGroup"> FASGroup </a>
グループモデルクラス。グループ機能にアクセスするためのクラスメソッドも提供しています。

#### Constants

|Constant|Description|
|------|-----|
|[FASGroupCompletionHandler](#FASGroup.FASGroupCompletionHandler)|グループ作成、グループ情報の更新、グループ情報の取得処理を行った際に利用されるブロックオブジェクト。 |
|[FASGroupsCompletionHandler](#FASGroup.FASGroupsCompletionHandler)|複数のグループ取得処理を行った際に利用されるブロックオブジェクト。 |


##### <a name="FASGroup.FASGroupCompletionHandler"> (^FASGroupCompletionHandler)(FASGroup *group, NSError *error) </a>
グループ作成、グループ情報の更新、グループ情報の取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASGroupCompletionHandler)(FASGroup *group, NSError *error);

* Parameters
	* group
		* [FASGroup](#FASGroup)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASGroup.FASGroupsCompletionHandler"> (^FASGroupsCompletionHandler)(NSArray *groups, FASPagingMeta *meta, NSError *error) </a>
複数のグループ取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASGroupsCompletionHandler)(NSArray *groups, FASPagingMeta *meta, NSError *error);

* Parameters
	* groups
		* 複数の[FASGroup](#FASGroup)がNSArrayに格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[groupId](#FASGroup.groupId)|グループID |
|[lastReadMessageId](#FASGroup.lastReadMessageId)|最後に閲覧したメッセージのID |
|[name](#FASGroup.name)|グループ名 |
|[membersCount](#FASGroup.membersCount)|グループに参加しているメンバー数 |
|[subscribed](#FASGroup.subscribed)|購読状態 |
|[pair](#FASGroup.pair)|ペアグループかどうかの状態 |
|[createdAt](#FASGroup.createdAt)|グループ作成時刻 |
|[updatedAt](#FASGroup.updatedAt)|グループ更新時刻 |

##### <a name="FASGroup.groupId"> groupId </a>
グループID

@property (nonatomic, readonly) NSString *groupId;

##### <a name="FASGroup.lastReadMessageId"> lastReadMessageId </a>
最後に閲覧したメッセージのID

@property (nonatomic, readonly) NSString *lastReadMessageId;

##### <a name="FASGroup.name"> name </a>
グループ名

@property (nonatomic, readonly) NSString *name;

##### <a name="FASGroup.membersCount"> membersCount </a>
グループに参加しているメンバー数

@property (nonatomic, readonly) NSUInteger membersCount;

##### <a name="FASGroup.subscribed"> subscribed </a>
購読状態

@property (nonatomic, readonly) BOOL subscribed;

##### <a name="FASGroup.pair"> pair </a>
ペアグループかどうかの状態

@property (nonatomic, readonly) BOOL pair;

##### <a name="FASGroup.createdAt"> createdAt </a>
グループ作成時刻

@property (nonatomic, readonly) NSDate *createdAt;

##### <a name="FASGroup.updatedAt"> updatedAt </a>
グループ更新時刻

@property (nonatomic, readonly) NSDate *updatedAt;


#### Class Method

|Method|Description|
|------|-----|
|[createGroupWithCompletion:](#FASGroup.createGroupWithCompletion) |グループを作成します。 |
|[createGroupWithGroupName:completion:](#FASGroup.createGroupWithGroupNamecompletion) |グループ名を指定してグループを作成します。 |
|[createGroupWithUserIds:completion:](#FASGroup.createGroupWithOpponentUserIdscompletion) |__`Deprecated`[createGroupWithOpponentUserIds:completion:](#FASGroup.createGroupWithOpponentUserIdscompletion)を利用してください。__ ユーザーIDを配列で指定してグループを作成します。 |
|[createGroupWithOpponentUserIds:completion:](#FASGroup.createGroupWithOpponentUserIdscompletion) |ユーザーIDを配列で指定してグループを作成します。 |
|[createGroupWithGroupName:userIds:completion:](#FASGroup.createGroupWithGroupNameopponentUserIdscompletion) |__`Deprecated`[createGroupWithGroupName:opponentUserIds:completion:](#FASGroup.createGroupWithGroupNameOpponentUserIdscompletion)を利用してください。__ グループ名、グループメンバーを指定してグループを作成します。 |
|[createGroupWithGroupName:opponentUserIds:completion:](#FASGroup.createGroupWithGroupNameopponentUserIdscompletion) |グループ名、グループメンバーを指定してグループを作成します。 |
|[updateGroupWithGroupId:groupName:completion:](#FASGroup.updateGroupWithGroupIdgroupNamecompletion) |グループ名を変更します。 |
|[deleteGroupWithGroupId:completion:](#FASGroup.deleteGroupWithGroupIdcompletion) |グループを削除します。 |
|[fetchGroupsWithPage:completion:](#FASGroup.fetchGroupsWithPagecompletion) |グループを取得します。 |
|[subscribeGroupWithGroupId:completion:](#FASGroup.subscribeGroupWithGroupIdcompletion) |グループを購読状態にします。 |
|[unsubscribeGroupWithGroupId:completion:](#FASGroup.unsubscribeGroupWithGroupIdcompletion) |グループを未購読状態にします。 |
|[createPairWithUserId:completion:](#FASGroup.createPairWithOpponentUserIdcompletion) |__`Deprecated`[createPairWithOpponentUserId:completion:](#FASGroup.createPairWithOpponentUserIdcompletion)を利用してください。__ ペアグループを作成します。 |
|[createPairWithOpponentUserId:completion:](#FASGroup.createPairWithOpponentUserIdcompletion) |ペアグループを作成します。 |

##### <a name="FASGroup.createGroupWithCompletion"> createGroupWithCompletion: </a>
空のグループを作成します。

\+ (void)createGroupWithCompletion:(FASGroupCompletionHandler)completion;

* Parameters
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreationButton:(id)sender
{
    [FASGroup createGroupWithCompletion:^(FASGroup *group, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroup.createGroupWithGroupNamecompletion"> createGroupWithGroupName:completion: </a>
ユーザー名を指定してグループを作成します。

\+ (void)createGroupWithGroupName:(NSString *)groupName
                       completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupName
		* グループ名
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreationButton:(id)sender
{
    [FASGroup createGroupWithGroupName:@"GroupName"
                            completion:^(FASGroup *group, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroup.createGroupWithOpponentUserIdscompletion"> createGroupWithOpponentUserIds:completion: </a>
ユーザーIDを配列で指定してグループを作成します。

\+ (void)createGroupWithOpponentUserIds:(NSArray *)userIds
                             completion:(FASGroupCompletionHandler)completion;

* Parameters
	* userIds
		* ユーザーIDが格納された配列
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreationButton:(id)sender
{
    NSArray *userIds = @[
                        @"xxxxxxxxxxxxxxxxx",
                        @"yyyyyyyyyyyyyyyyy"
                        ];
    [FASGroup createGroupWithOpponentUserIds:userIds
                                  completion:^(FASGroup *group, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroup.createGroupWithGroupNameopponentUserIdscompletion"> createGroupWithGroupName:opponentUserIds:completion: </a>
グループ名とユーザーIDを配列で指定してグループを作成します。

\+ (void)createGroupWithGroupName:(NSString *)groupName
                  opponentUserIds:(NSArray *)userIds
                       completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupName
		* グループ名
	* userIds
		* ユーザーIDが格納された配列
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreationButton:(id)sender
{
    NSArray *userIds = @[
                        @"xxxxxxxxxxxxxxxxx",
                        @"yyyyyyyyyyyyyyyyy"
                        ];
    [FASGroup createGroupWithGroupName:@"GroupName"
                       opponentUserIds:userIds
                            completion:^(FASGroup *group, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroup.updateGroupWithGroupIdgroupNamecompletion"> updateGroupWithGroupId:groupName:completion: </a>
グループ名を変更します。

\+ (void)updateGroupWithGroupId:(NSString *)groupId
                      groupName:(NSString *)groupName
                     completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* groupName
		* グループ名
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedUpdateButton:(id)sender
{
    [FASGroup updateGroupWithGroupId:@"xxxxxxxxxxxxxxxxx"
                           groupName:@"NewGroupName"
                          completion:^(FASGroup *group, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroup.deleteGroupWithGroupIdcompletion"> deleteGroupWithGroupId:completion: </a>
グループを削除します。

\+ (void)deleteGroupWithGroupId:(NSString *)groupId
                     completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASGroup deleteGroupWithGroupId:@"xxxxxxxxxxxxxxxxx"
                          completion:^(NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroup.fetchGroupsWithPagecompletion"> fetchGroupsWithPage:completion: </a>
グループ一覧を取得します。

\+ (void)fetchGroupsWithPage:(NSUInteger)page
                  completion:(FASGroupCompletionHandler)completion;

* Parameters
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASGroup fetchGroupsWithPage:1
                       completion:^(NSArray *groups, FASPagingMeta *meta, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroup.subscribeGroupWithGroupIdcompletion"> subscribeGroupWithGroupId:completion: </a>
グループを購読状態にします。

\+ (void)subscribeGroupWithGroupId:(NSString *)groupId
                        completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedSubscribeButton:(id)sender
{
    [FASGroup subscribeGroupWithGroupId:@"xxxxxxxxxx"
                             completion:^(FASGroup *group, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroup.unsubscribeGroupWithGroupIdcompletion"> unsubscribeGroupWithGroupId:completion: </a>
グループを非購読状態にします。

\+ (void)unsubscribeGroupWithGroupId:(NSString *)groupId
                          completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedUnsubscribeButton:(id)sender
{
    [FASGroup unsubscribeGroupWithGroupId:@"xxxxxxxxxx"
                               completion:^(FASGroup *group, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroup.createPairWithOpponentUserIdcompletion"> createPairWithOpponentUserId:completion: </a>
ペアグループを作成します。既にペアグループが作成されている場合は既存のグループが返却されます。

\+ (void)createPairWithOpponentUserId:(NSString *)userId
                           completion:(FASGroupCompletionHandler)completion;

* Parameters
	* userId
		* ユーザーID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreatePairButton:(id)sender
{
    [FASGroup createPairWithOpponentUserId:@"xxxxxxxxxx"
                                completion:^(FASGroup *group, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

### <a name="FASGroupMember"> FASGroupMember </a>
グループメンバーモデルクラス。グループメンバー機能にアクセスするためのクラスメソッドも提供しています。

#### Constants

|Constant|Description|
|------|-----|
|[FASGroupMemberCompletionHandler](#FASGroupMember.FASGroupMemberCompletionHandler)|グループメンバー追加処理を行った際に利用されるブロックオブジェクト。 |
|[FASGroupMembersCompletionHandler](#FASGroupMember.FASGroupMembersCompletionHandler)|グループメンバー取得処理を行った際に利用されるブロックオブジェクト。 |


##### <a name="FASGroupMember.FASGroupMemberCompletionHandler"> (^FASGroupMemberCompletionHandler)(FASGroupMember *member, NSError *error) </a>
グループメンバー追加処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASGroupMemberCompletionHandler)(FASGroupMember *member, NSError *error);

* Parameters
	* member
		* [FASGroupMember](#FASGroupMember)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASGroupMember.FASGroupMembersCompletionHandler"> (^FASGroupMembersCompletionHandler)(NSArray *members, FASPagingMeta *meta, NSError *error) </a>
グループメンバー取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASGroupMembersCompletionHandler)(NSArray *members, FASPagingMeta *meta, NSError *error);

* Parameters
	* members
		* 複数の[FASGroupMember](#FASGroupMember)がNSArrayに格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[groupId](#FASGroupMember.groupId)|グループID |
|[user](#FASGroupMember.user)|グループに参加しているユーザー |

##### <a name="FASGroupMember.groupId"> groupId </a>
グループID

@property (nonatomic, readonly) NSString *groupId;

##### <a name="FASGroupMember.user"> user </a>
グループに参加しているユーザー。[FASUser](./Spec-User.md#FASUser)オブジェクト。

@property (nonatomic, readonly) FASUser *user;

#### Class Method

|Method|Description|
|------|-----|
|[addGroupMemberWithGroupId:userId:completion:](#FASGroupMember.addGroupMemberWithGroupIduserIdcompletion) |指定したグループにメンバーを追加します。 |
|[deleteGroupMemberWithGroupId:userId:completion:](#FASGroupMember.deleteGroupMemberWithGroupIduserIdcompletion) |指定したグループからメンバーを削除します。 |
|[fetchGroupMembersWithGroupId:page:completion:](#FASGroupMember.fetchGroupMembersWithGroupIdpagecompletion) |指定したグループのメンバー一覧を取得します。 |

##### <a name="FASGroupMember.addGroupMemberWithGroupIduserIdcompletion"> addGroupMemberWithGroupId:userId:completion: </a>
指定したグループにメンバーを追加します。

\+ (void)addGroupMemberWithGroupId:(NSString *)groupId
                            userId:(NSString *)userId
                        completion:(FASGroupMemberCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* userId
		* ユーザーID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroupMember.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    [FASGroupMember addGroupMemberWithGroupId:@"xxxxxxxxxxxxx"
                                       userId:@"yyyyyyyyyyyyyyy"
                                   completion:(FASGroupMember *member, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroupMember.deleteGroupMemberWithGroupIduserIdcompletion"> deleteGroupMemberWithGroupId:userId:completion: </a>
指定したグループからメンバーを削除します。

\+ (void)deleteGroupMemberWithGroupId:(NSString *)groupId
                               userId:(NSString *)userId
                           completion:(FASGroupMemberCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* userId
		* ユーザーID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroupMember.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASGroupMember deleteGroupMemberWithGroupId:@"xxxxxxxxxxxxx"
                                          userId:@"yyyyyyyyyyyyyyy"
                                      completion:(NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroupMember.fetchGroupMembersWithGroupIdpagecompletion"> fetchGroupMembersWithGroupId:page:completion: </a>
指定したグループのメンバー一覧を取得します。

\+ (void)fetchGroupMembersWithGroupId:(NSString *)groupId
                                 page:(NSUInteger)page
                           completion:(FASGroupMemberCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroupMember.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASGroupMember fetchGroupMembersWithGroupId:@"xxxxxxxxxxxxx"
                                            page:1
                                      completion:(NSArray *members, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

### <a name="FASGroupMessage"> FASGroupMessage </a>
グループメッセージモデルクラス。グループメッセージ機能にアクセスするためのクラスメソッドも提供しています。

#### Constants

|Constant|Description|
|------|-----|
|[FASGroupMessageCompletionHandler](#FASGroupMessage.FASGroupMessageCompletionHandler)|グループメッセージ追加処理、グループメッセージ一件取得処理を行った際に利用されるブロックオブジェクト。 |
|[FASGroupMessagesCompletionHandler](#FASGroupMessage.FASGroupMessagesCompletionHandler)|グループメセージ一覧取得処理を行った際に利用されるブロックオブジェクト。 |


##### <a name="FASGroupMessage.FASGroupMessageCompletionHandler"> (^FASGroupMessageCompletionHandler)(FASGroupMessage *message, NSError *error) </a>
グループメッセージ追加処理、グループメッセージ一件取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASGroupMessageCompletionHandler)(FASGroupMessage *message, NSError *error);

* Parameters
	* message
		* [FASGroupMessage](#FASGroupMessage)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASGroupMessage.FASGroupMessagesCompletionHandler"> (^FASGroupMessagesCompletionHandler)(NSArray *messages, FASPagingMeta *meta, NSError *error) </a>
グループメセージ一覧取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASGroupMessagesCompletionHandler)(NSArray *message, FASPagingMeta *meta, NSError *error);

* Parameters
	* messages
		* 複数の[FASGroupMessage](#FASGroupMessage)がNSArrayに格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[groupMessageId](#FASGroupMessage.groupMessageId)|グループメッセージID |
|[groupId](#FASGroupMessage.groupId)|グループID |
|[text](#FASGroupMessage.text)|テキストメッセージ |
|[imageUrl](#FASGroupMessage.imageUrl)|画像メッセージのURL |
|[imageThumbnailUrl](#FASGroupMessage.imageThumbnailUrl)|サムネイル化された画像メッセージのURL |
|[createdAt](#FASGroupMessage.createdAt)|グループメッセージ作成時刻 |
|[updatedAt](#FASGroupMessage.updatedAt)|グループメッセージ更新時刻 |
|[user](#FASGroupMessage.user)|メッセージを送信したユーザー |
|[video](#FASGroupMessage.video)|ビデオオブジェクト |
|[videoStatus](#FASGroupMessage.videoStatus)|ビデオの状態 |
|[image](#FASGroupMessage.image)|画像メッセージのデータ。送信時のみ格納されています。 |

##### <a name="FASGroupMessage.groupMessageId"> groupMessageId </a>
グループメッセージID

@property (nonatomic, readonly) NSString *groupMessageId;

##### <a name="FASGroupMessage.groupId"> groupId </a>
グループID

@property (nonatomic, readonly) NSString *groupId;

##### <a name="FASGroupMessage.text"> text </a>
テキストメッセージ

@property (nonatomic, readonly) NSString *text;

##### <a name="FASGroupMessage.imageUrl"> imageUrl </a>
画像メッセージのURL

@property (nonatomic, readonly) NSString *imageUrl;

##### <a name="FASGroupMessage.imageThumbnailUrl"> imageThumbnailUrl </a>
サムネイル化された画像メッセージのURL

@property (nonatomic, readonly) NSString *imageThumbnailUrl;

##### <a name="FASGroupMessage.createdAt"> createdAt </a>
グループメッセージ作成時刻

@property (nonatomic, readonly) NSDate *createdAt;

##### <a name="FASGroupMessage.updatedAt"> updatedAt </a>
グループメッセージ更新時刻

@property (nonatomic, readonly) NSDate *updatedAt;

##### <a name="FASGroupMessage.user"> user </a>
メッセージを送信したユーザー。[FASUser](./Spec-User.md#FASUser)オブジェクト。

@property (nonatomic, readonly) FASUser *user;

##### <a name="FASGroupMessage.video"> video </a>
[FASVideo](Spec-PlayMovie.md#FASVideo)オブジェクト。

@property (nonatomic, readonly) FASVideo *video;

##### <a name="FASGroupMessage.videoStatus"> videoStatus </a>
[FASVideoStatus](Spec-PlayMovie.md#FASVideo.FASVideoStatus)の値

@property (nonatomic, readonly) FASVideoStatus videoStatus;

##### <a name="FASGroupMessage.image"> image </a>
画像メッセージのデータ。送信時のみ格納されています。

@property (nonatomic, readonly) UIImage *image;

#### Class Method

|Method|Description|
|------|-----|
|[addMessageWithGroupId:text:completion:](#FASGroupMessage.addMessageWithGroupIdtextcompletion) |テキストメッセージを送信します。 |
|[addMessageWithGroupId:image:completion:](#FASGroupMessage.addMessageWithGroupIdimagecompletion) |画像メッセージを送信します。 |
|[addMessageWithGroupId:videoId:completion:](#FASGroupMessage.addMessageWithGroupIdimagecompletion) |ビデオメッセージをVideoIdを利用して送信します。 |
|[addMessageForInGameWithGroupId:text:completion:](#FASGroupMessage.addMessageForInGameWithGroupIdtextcompletion) |テキストメッセージを送信します。ゲーム中のチャット用に利用します。 |
|[deleteMessageWithGroupId:messageId:completion:](#FASGroupMessage.deleteMessageWithGroupIdmessageIdcompletion) |指定したグループIDとグループメッセージIDのメッセージを削除します。 |
|[fetchMessageWithGroupId:messageId:completion:](#FASGroupMessage.fetchMessageWithGroupIdmessageIdcompletion) |指定したグループIDとグループメッセージIDのメッセージを取得します。 |
|[fetchMessagesWithGroupId:page:completion:](#FASGroupMessage.fetchMessagesWithGroupIdpagecompletion) |指定したグループIDのメッセージ一覧を取得します。 |

##### <a name="FASGroupMessage.addMessageWithGroupIdtextcompletion"> addMessageWithGroupId:text:completion: </a>
テキストメッセージを送信します。

\+ (void)addMessageWithGroupId:(NSString *)groupId
                          text:(NSString *)text
                    completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* text
		* テキストメッセージ
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    [FASGroupMessage addMessageWithGroupId:@"xxxxxxxxxxxxx"
	                                  text:@"message"
                                completion:(FASGroupMessage *message, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroupMessage.addMessageWithGroupIdimagecompletion"> addMessageWithGroupId:image:completion: </a>
画像メッセージを送信します。

\+ (void)addMessageWithGroupId:(NSString *)groupId
                         image:(UIImage *)image
                    completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* image
		* 画像メッセージ
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    UIImage *image = [UIImage imageNamed:@"image"];
    [FASGroupMessage addMessageWithGroupId:@"xxxxxxxxxxxxx"
	                                 image:image
                                completion:(FASGroupMessage *message, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroupMessage.addMessageWithGroupIdvideoIdcompletion"> addMessageWithGroupId:videoId:completion: </a>
ビデオメッセージをVideoIdを利用して送信します。

\+ (void)addMessageWithGroupId:(NSString *)groupId
                       videoId:(NSString *)videoId
                    completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* videoId
		* ビデオID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    UIImage *image = [UIImage imageNamed:@"image"];
    [FASGroupMessage addMessageWithGroupId:@"xxxxxxxxxxxxx"
	                               videoId:@"yyyyyyyyyyyyy"
                                completion:(FASGroupMessage *message, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroupMessage.addMessageForInGameWithGroupIdtextcompletion"> addMessageForInGameWithGroupId:text:completion: </a>
テキストメッセージを送信します。ゲーム中のチャット用に利用します。

\+ (void)addMessageForInGameWithGroupId:(NSString *)groupId
                                   text:(NSString *)text
                             completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* text
		* テキストメッセージ
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    [FASGroupMessage addMessageForInGameWithGroupId:@"xxxxxxxxxxxxx"
                                               text:@"message"
                                         completion:(FASGroupMessage *message, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroupMessage.deleteMessageWithGroupIdmessageIdcompletion"> deleteMessageWithGroupId:messageId:completion: </a>
指定したグループIDとグループメッセージIDのメッセージを削除します。

\+ (void)deleteMessageWithGroupId:(NSString *)groupId
                        messageId:(NSString *)messageId
                       completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* messageId
		* グループメッセージID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASGroupMessage deleteMessageWithGroupId:@"xxxxxxxxxxxxx"
                                    messageId:@"yyyyyyyyyyyyyy"
                                   completion:(NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroupMessage.fetchMessageWithGroupIdmessageIdcompletion"> fetchMessageWithGroupId:messageId:completion: </a>
指定したグループIDとグループメッセージIDのメッセージを取得します。

\+ (void)fetchMessageWithGroupId:(NSString *)groupId
                       messageId:(NSString *)messageId
                      completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* messageId
		* グループメッセージID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASGroupMessage fetchMessageWithGroupId:@"xxxxxxxxxxxxx"
                                   messageId:@"yyyyyyyyyyyyyy"
                                  completion:(FASGroupMessage *message, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASGroupMessage.fetchMessagesWithGroupIdpagecompletion"> fetchMessagesWithGroupId:page:completion: </a>
指定したグループIDのメッセージ一覧を取得します。

\+ (void)fetchMessagesWithGroupId:(NSString *)groupId
                             page:(NSUInteger)page
                       completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASGroupMessage fetchMessagesWithGroupId:@"xxxxxxxxxxxxx"
                                         page:1
                                   completion:(NSArray *messages, FASPagingMeta *meta, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

### <a name="FASSticker"> FASSticker </a>
ステッカーモデルクラス。

#### Constants

|Constant|Description|
|------|-----|
|[FASStickerCompletionHandler](#FASSticker.FASStickerCompletionHandler)|ステッカー取得処理を行った際に利用されるブロックオブジェクト。 |


##### <a name="FASSticker.FASStickerCompletionHandler"> (^FASStickerCompletionHandler)(FASSticker *sticker, NSError *error) </a>
ステッカー取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASStickerCompletionHandler)(FASSticker *sticker, NSError *error);

* Parameters
	* sticker
		* [FASSticker](#FASSticker)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[stickerId](#FASSticker.stickerId)|ステッカーID |
|[stickerSetId](#FASSticker.stickerSetId)|ステッカーセットID |
|[stickerName](#FASSticker.stickerName)|ステッカー名 |
|[url](#FASSticker.url)|ステッカーのURL |

##### <a name="FASSticker.stickerId"> stickerId </a>
ステッカーID

@property (nonatomic, readonly) NSString *stickerId;

##### <a name="FASSticker.stickerSetId"> stickerSetId </a>
ステッカーセットID

@property (nonatomic, readonly) NSString *stickerSetId;

##### <a name="FASSticker.stickerName"> stickerName </a>
ステッカー名

@property (nonatomic, readonly) NSString *stickerName;

##### <a name="FASSticker.url"> url </a>
ステッカーのURL

@property (nonatomic, readonly) NSString *url;

#### Class Method

|Method|Description|
|------|-----|
|[fetchStickerWithId:completion:](#FASSticker.fetchStickerWithIdcompletion) |ステッカーを取得します。 |

##### <a name="FASSticker.fetchStickerWithIdcompletion"> fetchStickerWithId:completion: </a>
ステッカーを取得します。

\+ (void)fetchStickerWithId:(NSString *)stickerId
                completion:(FASStickerCompletionHandler)completion;

* Parameters
	* stickerId
		* ステッカーID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

### <a name="FASStickerSet"> FASStickerSet </a>
ステッカーセットモデルクラス。

#### Constants

|Constant|Description|
|------|-----|
|[FASStickerSetCompletionHandler](#FASStickerSet.FASStickerSetCompletionHandler)|ステッカーセット取得処理を行った際に利用されるブロックオブジェクト。 |
|[FASStickerSetsCompletionHandler](#FASStickerSet.FASStickerSetsCompletionHandler)|複数のステッカーセット取得処理を行った際に利用されるブロックオブジェクト。 |


##### <a name="FASStickerSet.FASStickerSetCompletionHandler"> (^FASStickerSetCompletionHandler)(FASStickerSet *stickerSet, NSError *error) </a>
ステッカーセット取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASStickerSetCompletionHandler)(FASStickerSet *stickerSet, NSError *error);

* Parameters
	* stickerSet
		* [FASStickerSet](#FASStickerSet)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。
		
##### <a name="FASStickerSet.FASStickerSetsCompletionHandler"> (^FASStickerSetsCompletionHandler)(NSArray *stickerSets, FASPagingMeta *meta, NSError *error) </a>
ステッカーセット取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASStickerSetsCompletionHandler)(NSArray *stickerSets, FASPagingMeta *meta, NSError *error);

* Parameters
	* stickerSet
		* [FASStickerSet](#FASStickerSet)が格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[stickerSetId](#FASStickerSet.stickerSetId)|ステッカーセットID |
|[stickerSetName](#FASStickerSet.stickerSetName)|ステッカーセット名 |
|[url](#FASStickerSet.url)|ステッカーセットの画像URL |
|[stickers](#FASStickerSet.stickers)|ステッカーセットに含まれる[FASSticker](#FASSticker)群が格納されています。 |
|[createdAt](#FASStickerSet.createdAt)|ステッカーセットが作成された日時 |
|[updatedAt](#FASStickerSet.updatedAt)|ステッカーセットが更新された日時 |

##### <a name="FASStickerSet.stickerSetId"> stickerSetId </a>
ステッカーセットID

@property (nonatomic, readonly) NSString *stickerSetId;

##### <a name="FASStickerSet.stickerSetName"> stickerSetName </a>
ステッカーセット名

@property (nonatomic, readonly) NSString *stickerSetName;

##### <a name="FASStickerSet.url"> url </a>
ステッカーセットの画像URL

@property (nonatomic, readonly) NSString *url;

##### <a name="FASStickerSet.stickers"> stickers </a>
ステッカーセットに含まれる[FASSticker](#FASSticker)群が格納されています。

@property (nonatomic, readonly) NSArray *stickers;

##### <a name="FASStickerSet.createdAt"> createdAt </a>
ステッカーセットが作成された日時

@property (nonatomic, readonly) NSString *url;

##### <a name="FASStickerSet.createdAt"> updatedAt </a>
ステッカーセットが更新された日

@property (nonatomic, readonly) NSDate *updatedAt;

#### Class Method

|Method|Description|
|------|-----|
|[fetchStickerSetsWithPage:completion:](#FASStickerSet.fetchStickerSetsWithPagecompletion) |ステッカーセットの一覧を取得します。 |
|[fetchStickerSetWithId:completion:](#FASStickerSet.fetchStickerSetWithIdcompletion) |ステッカーセットを取得します。 |

##### <a name="FASStickerSet.fetchStickerSetsWithPagecompletion"> fetchStickerSetsWithPage:completion: </a>
ステッカーセットの一覧を取得します。

\+ (void)fetchStickerSetsWithPage:(NSUInteger)page
                      completion:(FASStickerSetsCompletionHandler)completion;

* Parameters
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

##### <a name="FASStickerSet.fetchStickerSetWithIdcompletion"> fetchStickerSetWithId:completion: </a>
ステッカーセットを取得します。

\+ (void)fetchStickerSetWithId:(NSString *)stickerSetId
                   completion:(FASStickerSetCompletionHandler)completion;

* Parameters
	* stickerSetId
		* ステッカーセットID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。