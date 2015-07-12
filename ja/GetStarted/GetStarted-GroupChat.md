# Getting Started - Group Chat

last update at 2015/7/8

---

- [グループAPIの利用方法](#HowToUseAPI)
	- [グループの作成](#HowToCreateGroup)
	- [メッセージの送信](#HowToSendMessage)
	- [メンバーの追加](#HowToAddMember)
- [ゲーム内チャットの利用](#HowToUseInGameChat)
	- [チャットイベントの監視](#ObserveEvent)
	- [ゲーム内チャットにメッセージの送信](#HowToSendMessageForInGame)

---

## <a name="HowToUseAPI"> グループAPIの利用方法 </a>

グループAPIを利用することで、グループの作成、グループに対してメッセージの送信、メンバーの追加等の機能を利用することが出来ます。独自にチャット画面を実装したり[ゲーム内チャットの利用](#HowToUseInGameChat)を考えているゲームはこのAPIの利用が必要になります。

### <a name="HowToCreateGroup"> グループの作成 </a>

グループを作成します。
グループにはマルチグループと、ペアグループの２種類が存在します。
マルチグループは2人以上のユーザーから作成することができます。マルチグループの場合は同じメンバーでも複数のグループを作成することが出来ます。
ペアグループはユーザーとの1:1のグループです。既に作成されているペアグループを再度作成することは出来ず、作成しようとすると既存のペアグループが返却されます。

Sample : マルチグループ

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreateMultiGroupButton:(id)sender
{
    NSArray *userIds = @[
                         @"xxxxxxxxxxxxxx",
                         @"yyyyyyyyyyyyyy",
                         @"zzzzzzzzzzzzzz"
                         ];
    [FASGroup createGroupWithUserIds:userIds
                          completion:^(FASGroup *group, NSError *error)
     {
         if (error)
         {
             // エラー
             return;
         }

         // 成功
         // 常に新しいグループが作成される。
     }];

}
```

Sample : ペアグループ

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreatePairGroupButton:(id)sender
{
    [FASGroup createPairWithUserId:@"xxxxxxxxxxxxxxxxxx"
                        completion:^(FASGroup *group, NSError *error)
     {
         if (error)
         {
             // エラー
             return;
         }

         // 成功
         // 既に作成されているペアグループだった場合は既存のグループが返却される。
     }];

}
```

### <a name="HowToSendMessage"> メッセージの送信 </a>

対象のグループIDに対してメッセージを送信します。
現在メッセージでは、テキストメッセージと画像メッセージがサポートされています。

Sample : テキストメッセージ

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddTextMessageButton:(id)sender
{
    [FASGroupMessage addMessageWithGroupId:@"xxxxxxxxxxxxxxx"
                                      text:@"text message"
                                completion:^(FASGroupMessage *message, NSError *error)
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

Sample : 画像メッセージ

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddTextMessageButton:(id)sender
{
    UIImage *image = [UIImage imageNamed:@"image"];
    [FASGroupMessage addMessageWithGroupId:@"xxxxxxxxxxxxxxx"
                                     image:image
                                completion:^(FASGroupMessage *message, NSError *error)
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

### <a name="HowToAddMember"> メンバーの追加 </a>

既存のマルチグループにメンバーを追加します。
ペアグループにメンバーを追加しようとするとエラーが返却されます。

Sample

```
#import <AppSteroid/FASGroupMember.h>

	…
	…

- (IBAction)pushedAddMemberButton:(id)sender
{
    [FASGroupMember addGroupMemberWithGroupId:@"xxxxxxxxxxxxxxx"
                                       userId:@"yyyyyyyyyyyyyyy"
                                   completion:^(FASGroupMember *member, NSError *error)
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

---

## <a name="HowToUseInGameChat"> ゲーム内チャットの利用 </a>
インゲームテキストチャットは、ゲーム中にリアルタイムでグループ間でテキストチャットを行う機能です。
テキストチャットはグループメッセージを介して行われます。

### 手順とサンプル

#### 事前準備
* AppSteroid の機能を利用するには、[GetStarted](./AppSteroidGetStarted.md) に説明する初期設定を行っておく必要があります。
* グループメッセージはプッシュ通知を介して行われますので [プッシュ通知の設定](GetStarted/GetStarted-PushNotification.md)を行っておく必要があります。

#### グループの作成
1. グループの作成
2. グループの作成の完了を処理する

```
#import <AppSteroid/FASGroup.h>

- (IBAction)pushedCreateGroupButton:(id)sender
{
	// 1. グループの作成
	[FASGroup createGroupWithOpponentUserIds:userIds
                                  completion:^(FASGroup *group, NSError *error)
	{
		// 2. グループの作成の完了を処理する
	}];
}
```

#### グループメッセージの受信
1. グループメッセージ作成時に発火するイベントを登録
2. グループメッセージ作成イベントを処理する
3. ビューから離れる時にイベントを破棄する

```
#import <AppSteroid/FASEvent.h>

@implementation InGameChatViewController
{
	FASObserver *_inGameObserver;
}

- (void)viewWillAppear:(BOOL)animated
{
    [super viewWillAppear:animated];

	// 1. グループメッセージ作成時に発火するイベントを登録
    _inGameObserver = [FASEvent observeEventWithPath:@"group/message/in_game"
                                              action:@"created"
                                        eventHandler:^(NSDictionary *params)
    {
		// 2. グループメッセージ作成イベントを処理する
		NSLog(@"%@", params);
    }];
    
    [self _registerForKeyboardNotifications];
}

- (void)viewWillDisappear:(BOOL)animated
{
    [super viewWillDisappear:animated];
    
    // 3. ビューから離れる時にイベントを破棄する
    [FASEvent unobserve:_inGameObserver];
}

```

#### グループメッセージの送信
1. グループメッセージの送信
2. メッセージ送信の完了を処理する

```
#import <AppSteroid/FASGroupMessage.h>

- (IBAction)pushedSendButton:(id)sender
{
	// 1. グループメッセージの送信
	[FASGroupMessage addMessageForInGameWithGroupId:@"xxxxxxgroup_idxxxxxxx"
                                               text:@"message"
                                         completion:^(FASGroupMessage *message, NSError *error)
    {
		// 2. メッセージ送信の完了を処理する
    }];
}

```