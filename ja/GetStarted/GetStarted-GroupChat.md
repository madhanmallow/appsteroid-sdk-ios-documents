# Getting Started - Group Chat

last update at 2014/10/7

---

- [グループチャット画面の表示](#HowToDisplayView)
	- [簡単に表示する](#EasyWay)
	- [パラメータを指定して表示する](#SettingParameters)
	- [レイアウトの変更](#Layout)
- [グループAPIの利用方法](#HowToUseAPI)
	- [グループの作成](#HowToCreateGroup)
	- [メッセージの送信](#HowToSendMessage)
	- [メンバーの追加](#HowToAddMember)
- [ゲーム内チャットの利用](#HowToUseInGameChat)
	- [チャットイベントの監視](#ObserveEvent)
	- [ゲーム内チャットにメッセージの送信](#HowToSendMessageForInGame)

---

## <a name="HowToDisplayGroupChatView"> グループチャット画面の表示 </a>

AppSteroidが提供するグループチャットのGUIを表示する方法を説明します。
グループチャット画面ではグループの作成、チャット画面からテキストメッセージや画像の送信、メンバーの追加削除などを行うことが出来ます。

### <a name="EasyWay"> 簡単に表示する </a>

デフォルトの設定で簡単にグループチャット画面を表示します。

Sample

```
#import <AppSteroid/FASGroupNavigationController.h>

	…
	…

- (IBAction)pushedGroupButton:(id)sender
{
    [FASGroupNavigationController presentGroupWithTarget:self
                                                animated:YES];
}
```

### <a name="SettingParameters"> パラメータを指定して表示する </a>

パラメータを指定してグループチャット画面を表示します。

Sample

```
#import <AppSteroid/FASGroupNavigationController.h>

	…
	…

- (IBAction)pushedGroupButton:(id)sender
{
    FASGroupNavigationController *groupNavigationController = [FASGroupNavigationController groupNavigationController];
    groupNavigationController.animated = YES;
    [self presentViewController:groupNavigationController animated:YES completion:nil];
}
```

### <a name="Layout"> レイアウトの変更 </a>

[FASGroupLayout](../Specs/Spec-Group.md#FASGroupLayout)クラスを利用することでレイアウトを変更することが出来ます。
それぞれのビューのレイアウトの変更方法については仕様書のサンプルコードを参照してください。

- [グループリストビュー](../Specs/Spec-Group.md#FASGroupLayout.groupListLayoutBlocks)
- [グループ作成ビュー](../Specs/Spec-Group.md#FASGroupLayout.groupCreateLayoutBlocks)
- [グループチャットビュー](../Specs/Spec-Group.md#FASGroupLayout.groupChatLayoutBlocks)
- [グループメンバービュー](../Specs/Spec-Group.md#FASGroupLayout.groupMemberLayoutBlocks)
- [グループメンバー追加ビュー](../Specs/Spec-Group.md#FASGroupLayout.groupMemberAdditionLayoutBlocks)

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

ゲーム内チャット機能はゲーム内で利用出来るシンプルなテキストチャット機能です。
テキストメッセージは保存されないので途中から参加したメンバーは過去のメッセージを閲覧することは出来ません。

### <a name="ObserveEvent"> チャットイベントの監視 </a>
利用するにはまず通知を受信出来るようにチャットのイベントを監視する必要があります。
監視の方法は[プッシュ通知のイベント監視](GetStarted-PushNotification.md#ObserveEvent)を参照してください。
監視すべきpathとactionは以下です。

```
path : group/message/in_game
action : created
```

### <a name="HowToSendMessageForInGame"> ゲーム内チャットにメッセージの送信 </a>

指定したグループに対して、ゲーム内チャットとしてメッセージを送信します。

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedSendButton:(id)sender
{
    [FASGroupMessage addMessageForInGameWithGroupId:@"xxxxxxxxxxxxxxxx"
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
