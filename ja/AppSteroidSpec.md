# AppSteroid for iOS SDK仕様書

last update at 2015/2/26

---

## Introduction
AppSteroid for iOSは、iOS用の統合ゲーム用バックエンドサービスです。
本サービスを利用すると、無料かつ簡単に、モバイルゲーム用に洗練された各種バックエンドサービスをあなたのゲームアプリへ追加することができます。

---

## Classes

|Common Classes|Description|
|------|-----|
|[AppSteroid](#AppSteroid)|AppSteroid初期設定クラス |
|[FASTabBarController](#FASTabBarController)|AppSteroidが提供するTabBarControllerにアクセスするためのクラス |
|[FASPagingMeta](#FASPagingMeta)|配列データのメタ情報が格納されているクラス |

|User|Description|
|------|-----|
|[FASAccount](Specs/Spec-User.md#FASAccount)|ログインユーザーのアカウント操作に関するクラス |
|[FASSNSAccount](Specs/Spec-User.md#FASSNSAccount)|SNSアカウントの操作に関するクラス |
|[FASLoginUser](Specs/Spec-User.md#FASLoginUser)|ログインユーザーモデルクラス |
|[FASUser](Specs/Spec-User.md#FASUser)|ユーザーモデルクラス |
|[FASProfileNavigationController](Specs/Spec-User.md#FASProfileNavigationController)|プロフィールビューのベースとなるNavigationController |

|Notification|Description|
|------|-----|
|[FASNotification](Specs/Spec-Notification.md#FASNotification)|PushNotification用のデバイストークンの操作に関するクラス |
|[FASEvent](Specs/Spec-Notification.md#FASEvent)|PushNotificationを監視して通知を受け取るためのクラス |
|[FASObserver](Specs/Spec-Notification.md#FASObserver)|[FASEvent](Specs/Spec-Notification.md#FASEvent)で監視登録した際に作成されるクラス |

|Message|Description|
|------|-----|
|[FASDirectMessage](Specs/Spec-Message.md#FASDirectMessage)|Fresviiコンソールから送信されるダイレクトメッセージの操作に関するクラス |
|[FASCustomMessage](Specs/Spec-Message.md#FASCustomMessage)|特定の相手にプッシュ通知を送信する機能に関するクラス |

|Key-Value Storage|Description|
|------|-----|
|[FASStorage](Specs/Spec-Storage.md#FASStorage)|AppSteroidが提供するKey-Value Storageの操作に関するクラス |

|Voice Chat|Description|
|------|-----|
|[FASConference](Specs/Spec-VoiceChat.md#FASConference)|ボイスチャット機能に関するクラス |

|Play Movie|Description|
|------|-----|
|[FASVideo](Specs/Spec-PlayMovie.md#FASVideo)|録画したプレイムービーの操作に関するクラス |
|[FASMovieMaker](Specs/Spec-MovieMaker.md#FASMovieMaker)|ゲームのプレイムービーを録画する機能に関するクラス |

|Play Statistics|Description|
|------|-----|
|[FASPlayStats](Specs/Spec-PlayStats.md#FASPlayStats)|ゲームの統計情報を取得する機能に関するクラス |

|Forum|Description|
|------|-----|
|[FASForumNavigationController](Specs/Spec-Forum.md#FASForumNavigationController)|フォーラムビューのベースとなるNavigationController |

|Group|Description|
|------|-----|
|[FASGroup](Specs/Spec-Group.md#FASGroup)|グループモデルクラス |
|[FASGroupMember](Specs/Spec-Group.md#FASGroupMember)|グループメンバーモデルクラス |
|[FASGroupMessage](Specs/Spec-Group.md#FASGroupMessage)|グループメッセージモデルクラス |
|[FASGroupNavigationController](Specs/Spec-Group.md#FASGroupNavigationController)|グループビューのベースとなるNavigationController |

|Leaderboard|Description|
|------|-----|
|[FASLeaderboard](Specs/Spec-Leaderboard.md#FASLeaderboard)|リーダーボードモデルクラス |
|[FASScore](Specs/Spec-Leaderboard.md#FASScore)|スコアモデルクラス |
|[FASRank](Specs/Spec-Leaderboard.md#FASRank)|ランクモデルクラス |
|[FASSortOptions](Specs/Spec-Leaderboard.md#FASSortOptions)|ランキングの集計方法に関するクラス |
|[FASLeaderboardNavigationController](Specs/Spec-Leaderboard.md#FASLeaderboardNavigationController)|リーダーボードビューのベースとなるNavigationController |

|Matchmaking|Description|
|------|-----|
|[FASMatch](Specs/Spec-Matchmaking.md#FASMatch)|マッチモデルクラス |
|[FASMatchRequest](Specs/Spec-Matchmaking.md#FASMatchRequest)|マッチリクエストモデルクラス |
|[FASMatchInvitation](Specs/Spec-Matchmaking.md#FASMatchInvitation)|マッチ招待モデルクラス |
|[FASMatchPlayer](Specs/Spec-Matchmaking.md#FASMatchPlayer)|マッチプレイヤーモデルクラス |
|[FASGameContext](Specs/Spec-Matchmaking.md#FASGameContext)|ゲームコンテキストモデルクラス |
|[FASMatchmakingNavigationController](Specs/Spec-Matchmaking.md#FASMatchmakingNavigationController)|マッチメイキングのベースとなるNavigationController |

---

## APIs
### <a name="AppSteroid"> AppSteroid </a>
SDK利用のための共通の設定をすることが出来ます。
また、ユーザーデータの取得もこのクラスで可能です。

#### Constants

|Constant|Description|
|------|-----|
|[FASTab](#AppSteroid.FASTab)|[FASTabBarController](#FASTabBarController)で表示できるタブが定義されています。 |
|[FASResponseCompletionHandler](#AppSteroid.FASResponseCompletionHandler)|ネットワーク通信やデータベースへの書き込み、読み込み処理が完了したときに実行されるブロックオブジェクトです。|
|[FASCompletionHandler](#AppSteroid.FASCompletionHandler)|処理が完了したかどうかのみを通知するために実行されるブロックオブジェクトです。|

##### <a name="AppSteroid.FASTab"> FASTab </a>
[FASTabBarController](#FASTabBarController)で表示できるタブが定義されています。

```
typedef NS_ENUM(NSInteger, FASTab)
{
    FASTabForum       = (1UL << 0),
    FASTabLeaderboard = (1UL << 1),
    FASTabGroup       = (1UL << 2),
    FASTabProfile     = (1UL << 3)
};
```

###### Constants
###### FASTabForum
フォーラムタブ

###### FASTabLeaderboard
リーダーボードタブ

###### FASTabGroup
グループタブ

###### FASTabProfile
プロフィールタブ

##### <a name="AppSteroid.FASResponseCompletionHandler"> (^FASResponseCompletionHandler)(id response, NSError *error) </a>
ネットワーク通信やデータベースへの書き込み、読み込み処理が完了したときに実行されるブロックオブジェクトです。

typedef void (^FASResponseCompletionHandler)(id response, NSError *error)

* Parameters
  * response
    * 実行結果が格納されています。
  * error
    * エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="AppSteroid.FASCompletionHandler"> (^FASCompletionHandler)(NSError *error) </a>
処理が完了したかどうかのみを通知するために実行されるブロックオブジェクトです。

typedef void (^FASCompletionHandler)(NSError *error)

* Parameters
  * error
    * エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Class Methods

|Method|Description|
|------|-----|
|[startWithAppIdentifier:secretToken:](#AppSteroid.startWithAppIdentifiersecretToken)|SDKの利用を開始するために利用します。  |
|[startWithAppIdentifier:secretToken:development:](#AppSteroid_startWithAppIdentifiersecretTokendevelopment)|SDKの利用を開始するために利用します。 モード指定付き。 |
|[setTimeout:](#AppSteroid.setTimeout)|ネットワーク通信時のタイムアウト時間を設定します。 |
|[setTabs:](#AppSteroid.setTabs)|表示するタブを設定します。 |
|[sdkVersion](#AppSteroid.sdkVersion)|SDKのバージョンを返却します。 |
|[sdkBuildVersion](#AppSteroid.sdkBuildVersion)|SDKのビルドバージョンを返却します。 |

##### <a name="AppSteroid.startWithAppIdentifiersecretToken"> startWithAppIdentifier:secretToken: </a>
SDKの利用を開始するための初期設定を行います。開発モードは配布用となります。開発モードとして起動する場合、[モード引数を指定できるバージョン](#AppSteroid_startWithAppIdentifiersecretTokendevelopment)を実行していください。

\+ (void)startWithAppIdentifier:(NSString *)appIdentifier secretToken:(NSString *)secretToken

* Parameters
  * appIdentifier
    * アプリケーションID
  * secretToken
    * シークレットトークン


##### <a name="AppSteroid_startWithAppIdentifiersecretTokendevelopment"> startWithAppIdentifier:secretToken:development: </a>
SDKの利用を開始するための初期設定を行います。開発モードを指定して起動する事ができます。詳細は [開発モードについて](./DevelopmentMode.md) を確認ください。

\+ (void)startWithAppIdentifier:(NSString *)appIdentifier
                    secretToken:(NSString *)secretToken
                    development:(BOOL)development;

* Parameters
  * appIdentifier
    * アプリケーションID
  * secretToken
    * シークレットトークン
  * development
    * YESにした場合、開発モードとして起動します。配布用ビルド時は NOを指定します。

Sample

```
#import <AppSteroid/AppSteroid.h>

  …
  …

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // Required.
    // Start AppSteroid.
  NSString *appId = @"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
  NSString *secretToken = @"yyyyyyyyyyyyyyyyyyyyyyyyyyyy";
  [AppSteroid startWithAppIdentifier:appId secretToken:secretToken development:NO];

  // Optional.
  // You can set network timeout. Default is 30.0.
  [AppSteroid setTimeout:20.0];

  …
  …
   …

  return YES;
}
```

##### <a name="AppSteroid.setTimeout"> setTimeout: </a>
ネットワーク通信のタイムアウトを設定します。
デフォルト値は30秒です。

\+ (void)setTimeout:(NSUInteger)timeout

* Parameters
  * timeout
    * タイムアウトの秒数

##### <a name="AppSteroid.setTabs"> setTabs: </a>
表示するタブを設定します。
デフォルトは`FASTabForum | FASTabLeaderboard | FASTabGroup | FASTabProfile`です。

\+ (void)setTabs:(FASTab)tabs

* Parameters
  * tabs
    * [FASTab](#AppSteroid.FASTab)で定義されているタブ。`FASTabForum | FASTabProfile`のように指定します。

Sample

```
[AppSteroid setTabs:FASTabForum | FASTabLeaderboard | FASTabGroup | FASTabProfile];
```

##### <a name="AppSteroid.sdkVersion"> sdkVersion </a>
SDKのバージョンを`NSString`で返却します。

\+ (NSString *)sdkVersion

##### <a name="AppSteroid.sdkBuildVersion"> sdkBuildVersion </a>
SDKのビルドバージョンを`NSString`で返却します。

\+ (NSString *)sdkBuildVersion

### <a name="FASTabBarController"> FASTabBarController </a>
AppSteroidが提供するTabBarControllerにアクセスするためのクラス

#### Class Method

|Method|Description|
|------|-----|
|[presentTabBarControllerWithTarget:animated:](#FASTabBarController.presentTabBarControllerWithTargetanimated) |[AppSteroid#setTabs:](AppSteorid.setTabs)で定義されたタブを表示します。未定義の場合は`フォーラム`、`リーダーボード`、`メッセージ`、`プロフィール`のタブを表示します。 |

##### <a name="FASTabBarController.presentTabBarControllerWithTargetanimated"> presentTabBarControllerWithTarget: </a>
`フォーラム`、`リーダーボード`、`プロフィール`のTabBarControllerを表示します。

\+ (void)presentTabBarControllerWithTarget:(UIViewController *)target
                                  animated:(BOOL)animated;

* Parameters
  * target
    * TabBarControllerを表示する元となるViewControllerを指定します。
  * animated
    * YESならアニメーションさせて遷移します。NOならアニメーションはしません。

Sample

```

#import <AppSteroid/FASTabBarController.h>

  …
  …

- (IBAction)pushedFASTabBarButton:(id)sender
{
    [FASTabBarController presentTabBarControllerWithTarget:self
                                                  animated:YES];
}
```

### <a name="FASPagingMeta"> FASPagingMeta </a>
配列データのメタ情報が格納されているクラス

#### Properties

|Properties|Description|
|------|-----|
|[currentPage](#FASPagingMeta.currentPage)|現在のページ |
|[nextPage](#FASPagingMeta.nextPage)|次のページ |
|[perPage](#FASPagingMeta.perPage)|1ページあたりのコンテンツ数 |
|[totalCount](#FASPagingMeta.totalCount)|全コンテンツ数 |
|[totalPages](#FASPagingMeta.totalPages)|全ページ数 |

##### <a name="FASPagingMeta.currentPage"> currentPage </a>
現在のページ

@property (nonatomic, assign) NSUInteger currentPage

##### <a name="FASPagingMeta.nextPage"> nextPage </a>
次のページ

@property (nonatomic, assign) NSUInteger nextPage

##### <a name="FASPagingMeta.perPage"> perPage </a>
1ページあたりのコンテンツ数

@property (nonatomic, assign) NSUInteger perPage

##### <a name="FASPagingMeta.totalCount"> totalCount </a>
全コンテンツ数

@property (nonatomic, assign) NSUInteger totalCount

##### <a name="FASPagingMeta.totalPages"> totalPages </a>
全ページ数

@property (nonatomic, assign) NSUInteger totalPages
