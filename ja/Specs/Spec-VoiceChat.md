# Voice Chat Specifications

last update at 2014/10/7

---

## Introduction

ボイスチャットに関する機能の仕様書です。
ボイスチャットをするために必要なカンファレンスの作成や参加などの機能が提供されています。
利用方法は[VoiceChatGetStarted](../GetStarted/GetStarted-VoiceChat.md)を参照してください。

---

## Classes

|Class|Description|
|------|-----|
|[FASConference](#FASConference)|ボイスチャットの機能に関するモデルクラス |
|[FASConferenceParticipant](#FASConferenceParticipant)|カンファレンスの参加者に関するモデルクラス |
|[FASVoiceChatLayout](#FASVoiceChatLayout)|ボイスチャットビュー関連のレイアウトを変更するためのクラス |

---

## APIs
### <a name="FASConference"> FASConference </a>
ボイスチャットの機能に関するモデルクラスです。
ボイスチャットを開始するためにカンファレンス(ボイスチャットを行うためのグループ)の作成を行ったり、既存のカンファレンスに参加したりします。

#### Constants

|Constant|Description|
|------|-----|
|[FASConferenceIncomingBehavior](#FASConference.FASConferenceIncomingBehavior)|ボイスチャットの着信時の振る舞い |
|[FASConferenceViewVisibility](#FASConference.FASConferenceViewVisibility)|ボイスチャットの着信時の通話画面表示 |
|[FASConferenceIncomingHandler](#FASConference.FASConferenceIncomingHandler)|着信があった時に呼ばれるブロックオブジェクト |
|[FASParticipantsCompletionHandler](#FASConference.FASParticipantsCompletionHandler)|ボイスチャットの参加者を取得する際に利用されるブロックオブジェクト |

##### <a name="FASConference.FASConferenceIncomingBehavior"> FASConferenceIncomingBehavior </a>
ボイスチャットの着信時の振る舞い。未設定時はユーザへ確認します。

```obj-c
typedef NS_ENUM(NSInteger, FASConferenceIncomingBehavior)
{
    FASConferenceIncomingBehaviorAsk        = 0,
    FASConferenceIncomingBehaviorAutoAccept = 1,
    FASConferenceIncomingBehaviorCallback   = 2
};
```

##### <a name="FASConference.FASConferenceViewVisibility"> FASConferenceViewVisibility </a>
ボイスチャットの着信時の画面の表示。デフォルトは ```OnlyInFAS``` となります。ゲーム画面上で通話を行いたい場合は、```Never```または```OnlyInFAS```を指定してください。

```obj-c
typedef NS_ENUM(NSInteger, FASConferenceIncomingBehavior)
{
    FASConferenceViewVisibilityNever = -1,
    FASConferenceViewVisibilityOnlyInFAS,
    FASConferenceViewVisibilityAnyTime,
};
```

- Never: 通話画面を表示しません
- OnlyInFAS: SDK提供のGUIを表示中のみ通話画面を表示します
- AnyTime: 常に通話画面を表示します

##### <a name="FASConference.FASConferenceIncomingHandler"> (^FASConferenceIncomingHandler)(NSString *groupId) </a>
着信があった時に通知を受け取るブロックオブジェクト。YESを返すと着信を受け入れます。

typedef BOOL (^FASConferenceIncomingHandler)(NSString *groupId);

##### <a name="FASConference.FASParticipantsCompletionHandler"> (^FASParticipantsCompletionHandler)(NSString *groupId) </a>
ボイスチャットの参加者を取得する際に利用されるブロックオブジェクト

typedef void (^FASParticipantsCompletionHandler)(NSArray *participants, NSError *error);


#### Properties

|Properties|Description|
|------|-----|
|[callStates](#FASConference.callStates)| |

##### <a name="FASConference.callStates"> callStates </a>

@property (readonly) NSDictionary *callStates;

#### Class Methods

|Method|Description|
|------|-----|
|[sharedInstance](#FASConference.sharedInstance) |`FASConference`クラスのシングルトンオブジェクトを返却します。 |
|[hostConferenceWithGroupId:completion:](#FASConference.hostConferenceWithGroupIdcompletion) |カンファレンスを作成します。 |
|[fetchConferenceWithGroupId:completion:](#FASConference.fetchConferenceWithGroupIdcompletion) |現在のカンファレンスを取得します。 |
|[fetchConferenceParticipantsWithGroupId:completion:](#FASConference.fetchConferenceParticipantsWithGroupIdcompletion) |カンファレンスの参加者を取得します。 |
|[joinConferenceWithGroupId:completion:](#FASConference.joinConferenceWithGroupIdcompletion) |カンファレンスに参加します。 |
|[setMicrophoneVolume:speakerVolume:completion:](#FASConference.setMicrophoneVolumespeakerVolumecompletion) |マイクボリュームとスピーカーボリュームを設定します。 |

##### <a name="FASConference.sharedInstance"> sharedInstance </a>
`FASConference`クラスのシングルトンオブジェクトを返却します。

\+ (instancetype)sharedInstance;

##### <a name="FASConference.hostConferenceWithGroupIdcompletion"> hostConferenceWithGroupId:completion: </a>
カンファレンスを作成します。

\+ (void)hostConferenceWithGroupId:(NSString *)groupId
                         completion:(FASResponseCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

##### <a name="FASConference.fetchConferenceWithGroupIdcompletion"> fetchConferenceWithGroupId:completion: </a>
現在のカンファレンスを取得します。

\+ (void)fetchConferenceWithGroupId:(NSString *)groupId
                         completion:(FASResponseCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

##### <a name="FASConference.fetchConferenceParticipantsWithGroupIdcompletion"> fetchConferenceParticipantsWithGroupId:completion: </a>
カンファレンスの参加者を取得します。

\+ (void)fetchConferenceParticipantsWithGroupId:(NSString *)groupId
                                    completion:(FASParticipantsCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

##### <a name="FASConference.joinConferenceWithGroupIdcompletion"> joinConferenceWithGroupId:completion: </a>
カンファレンスに参加します。

\+ (void)joinConferenceWithGroupId:(NSString *)groupId
                        completion:(FASResponseCompletionHandler)completion;

* Parameters
	* groupId
		* グループID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

##### <a name="FASConference.setMicrophoneVolumespeakerVolumecompletion"> setMicrophoneVolume:speakerVolume:completion: </a>
マイクボリュームとスピーカーボリュームを設定します。
端末自身のボリュームをSDK内部で増幅又は減衰させる機能です。

\+ (void)setMicrophoneVolume:(float)microphoneVolume
               speakerVolume:(float)speakerVolume
                  completion:(FASResponseCompletionHandler)completion;

* Parameters
	* microphoneVolume
		* マイクのボリュームを指定します。
	* speakerVolume
		* スピーカーのボリュームを指定します。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

#### Instance Methods

|Method|Description|
|------|-----|
|[humanizedRole](#FASConference.humanizedRole) |現在のカンファレンスのロール名を取得します。 |
|[addDelegate:](#FASConference.addDelegate) |カンファレンスのステータスが変更した通知を受信するためのデリゲートを指定します。 |
|[removeDelegate:](#FASConference.removeDelegate) |デリゲートを削除します。 |
|[setIncomingHandler:](#FASConference.setIncomingHandler) |着信があった時に通知を受け取るブロックオブジェクトです。 |
|[currentGroup](#FASConference.currentGroup) |現在のグループIDを取得します。 |
|[isMute](#FASConference.isMute) |ミュートかどうかを取得します。 |
|[muteWithCompletion:](#FASConference.muteWithCompletion) |ミュートモードにします。 |
|[unmuteWithCompletion:](#FASConference.unmuteWithCompletion) |ミュートモードを解除します。 |
|[leaveWithCompletion:](#FASConference.leaveWithCompletion) |カンファレンスを脱退します。 |
|[elapsedTime](#FASConference.elapsedTime) |カンファレンスが作成されてからの経過時間を取得します。 |

##### <a name="FASConference.humanizedRole"> humanizedRole </a>
現在のカンファレンスのロール名を取得します。

\- (NSString *)humanizedRole;

##### <a name="FASConference.addDelegate"> addDelegate: </a>
カンファレンスのステータスが変更した通知を受信するためのデリゲートを指定します。

\- (void)addDelegate:(id<FASConferenceDelegate>)delegate;

* Parameters
	* delegate
		* オブジェクトを指定します。

##### <a name="FASConference.removeDelegate"> removeDelegate: </a>
デリゲートを削除します。

\- (void)removeDelegate:(id<FASConferenceDelegate>)delegate;

* Parameters
	* delegate
		* オブジェクトを指定します。

##### <a name="FASConference.setIncomingHandler"> setIncomingHandler: </a>
着信があった時に通知を受け取るブロックオブジェクトに、着信時の処理を記述します。

\- (void)setIncomingHandler:(FASConferenceIncomingHandler)handler;

* Parameters
	* handler
		* `FASConferenceIncomingHandler`を指定します。

##### <a name="FASConference.currentGroup"> currentGroup </a>
現在のグループIDを取得します。

\-(NSString *)currentGroup;

##### <a name="FASConference.isMute"> isMute </a>
ミュートかどうかを取得します。

\-(BOOL)isMute;

##### <a name="FASConference.muteWithCompletion"> muteWithCompletion: </a>
ミュートモードにします。

\+ (void)muteWithCompletion:(FASResponseCompletionHandler)completion;

* Parameters
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

##### <a name="FASConference.unmuteWithCompletion"> unmuteWithCompletion: </a>
ミュートモードを解除します。

\+ (void)unmuteWithCompletion:(FASResponseCompletionHandler)completion;

* Parameters
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

##### <a name="FASConference.leaveWithCompletion"> leaveWithCompletion:completion </a>
カンファレンスを脱退します。

\+ (void)leaveWithCompletion:(FASResponseCompletionHandler)completion;

* Parameters
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト

##### <a name="FASConference.elapsedTime"> elapsedTime </a>
カンファレンスが作成されてからの経過時間を取得します。

\-(NSTimeInterval)elapsedTime;

#### <a name="FASConferenceDelegate"> FASConferenceDelegate </a>
[FASConference](#FASConference)オブジェクトの状態を監視して変更された際に呼ばれるデリゲートメソッド。

|Method|Description|
|------|-----|
|[didConferenceStart:](#FASConferenceDelegate.didConferenceStart) |カンファレンスが開始された際にコールされます。 |
|[didConferenceFinish](#FASConferenceDelegate.didConferenceFinish) |カンファレンスが終了された際にコールされます。 |
|[didCallStateChange:](#FASConferenceDelegate.didCallStateChange) |カンファレンスの参加者に変更が会った際にコールされます。 |

##### <a name="FASConferenceDelegate.didConferenceStart"> didConferenceStart: </a>
カンファレンスが開始された際にコールされます。

\- (void)didConferenceStart:(NSString *)groupId;

* Parameters
	* groupId
		* グループID

##### <a name="FASConferenceDelegate.didConferenceFinish"> didConferenceFinish </a>
カンファレンスが終了された際にコールされます。

\- (void)didConferenceFinish;

##### <a name="FASConferenceDelegate.didCallStateChange"> didCallStateChange: </a>
カンファレンスの参加者に変更が会った際にコールされます。

\- (void)didCallStateChange:(NSArray *)participants;

* Parameters
	* participants
		* 参加者一覧

### <a name="FASConferenceParticipant"> FASConferenceParticipant </a>
カンファレンスの参加者に関するモデルクラスです。

#### Properties

|Method|Description|
|------|-----|
|[user](#FASConferenceParticipant.user) |カンファレンスに参加しているユーザー |

##### <a name="FASConferenceParticipant.user"> user </a>
カンファレンスに参加しているユーザーが[FASUser](Spec-User.md#FASUser)オブジェクトで格納されています。

@property (nonatomic, readonly) FASUser *user;

#### Instance Methods

|Method|Description|
|------|-----|
|[humanizedCallStatus](#FASConferenceParticipant.humanizedCallStatus) |参加者の通話状態を取得します。 |

##### <a name="FASConferenceParticipant.humanizedCallStatus"> humanizedCallStatus: </a>
参加者の通話状態を取得します。

-(NSString *)humanizedCallStatus;


### <a name="FASVoiceChatLayout"> FASVoiceChatLayout </a>
ボイスチャットビュー関連のレイアウトを変更します。

#### Properties

|Properties|Description|
|------|-----|
|[voiceChatayoutBlocks](#FASVoiceChatLayout.voiceChatayoutBlocks)|ボイスチャットビューのレイアウトを変更するためのブロックオブジェクト |

##### <a name="FASVoiceChatLayout.voiceChatayoutBlocks"> voiceChatayoutBlocks </a>
ボイスチャットビューのレイアウトを変更するためのブロックオブジェクト

@property (nonatomic, copy) FASVoiceChatViewController *(^voiceChatayoutBlocks)(FASVoiceChatViewController *voiceChatViewController);

Sample - 背景色を変更するサンプル

```
    [FASVoiceChatLayout sharedInstance].voiceChatayoutBlocks = ^FASVoiceChatViewController *(FASVoiceChatViewController *voiceChatViewController)
    {
        voiceChatViewController.view.backgroundColor = [UIColor whiteColor];
        voiceChatViewController.endLabel.textColor = [UIColor blackColor];
        voiceChatViewController.messageLabel.textColor = [UIColor blackColor];
        voiceChatViewController.timeLabel.textColor = [UIColor blackColor];
        if ([voiceChatViewController.navigationController.navigationBar respondsToSelector:@selector(barTintColor)])
        {
            voiceChatViewController.navigationController.navigationBar.tintColor = [UIColor greenColor];
            voiceChatViewController.navigationController.navigationBar.barTintColor = [UIColor whiteColor];
        }
        voiceChatViewController.navigationController.navigationBar.barStyle = UIBarStyleDefault;
        voiceChatViewController.navigationController.navigationBar.titleTextAttributes = @{NSForegroundColorAttributeName: [UIColor blackColor]};
        return voiceChatViewController;
    };
```

#### Class Method

|Method|Description|
|------|-----|
|[sharedInstance](#FASVoiceChatLayout.sharedInstance) |唯一のオブジェクトを返却します。 |

##### <a name="FASVoiceChatLayout.sharedInstance"> sharedInstance </a>
唯一のオブジェクトを返却します。

\+ (instancetype)sharedInstance;
