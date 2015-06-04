# Getting Started - Matchmaking

last update at 2015/5/26

---

- [マッチメイキングの概要](#Abstruct)
- [マッチメイキング画面の表示](#HowToDisplayView)
	- [簡単に表示する](#EasyWay)
	- [パラメータを指定して表示する](#SettingParameters)
	- [マッチする条件を指定する](#Segment)
	- [レイアウトを変更する](#Layout)
- [マッチの成立をハンドリングする](#HandlingMatchCompletion)
- [ターン制ゲームへの対応](#GameContext)
	- [イベントの登録と削除](#GameContextEvent)
	- [ゲームコンテキストのアップデート](#GameContextUpdate)

---

## <a name="Abstruct"> マッチメイキングの概要 </a>
- マッチメイキングは対戦相手を探すための機能です。
- マッチメイクへの参加方法は以下の３パターンのいずれかとなります。
    - **リクエストの作成:** マッチ条件を指定してリクエスト作成します。招待ユーザを指定した場合は新しいマッチオブジェクトが作成されます。
    招待ユーザを指定しなかった場合、マッチ条件に一致するマッチが既に存在する場合はそちらに参加します。
    存在しない場合は新しいマッチオブジェクトを作成し他の参加者を待ちます。
    - **招待の承認:** マッチメイクリクエスト者から招待をもらい参加します。友達同士での対戦などで利用します。
    招待を承認後、参加を取り消す場合は招待ID（=リクエストID）を使ってリクエストのキャンセルを実行します。
    - **マッチへの参加:** マッチIDを指定して明示的に任意のマッチに参加します。
    参加中のマッチの、他の参加者が全員キャンセルした場合は参加が取り消されます。
- マッチメイク成立後はマッチ毎に以下のものが作成されます。
    - **マッチメイク用グループ** ゲーム中のチャット、ボイスチャット等に利用する。
    - **ゲームコンテキスト** ターンベースゲームの共有データとして利用する。初期作成時の更新ユーザはアプリ公式ユーザ。詳しくは[ターン制ゲームへの対応](#GameContext)を参照してください。

## <a name="HowToDisplayView"> マッチメキング画面の表示 </a>

AppSteroidが提供するマッチメイキングのGUIを表示する方法を説明します。
マッチメイキング画面を表示すると自動的にマッチするユーザーを検索してマッチを成立させます。マッチが完了した後はデリゲートメソッドがコールされるようになっています。

### <a name="EasyWay"> 簡単に表示する </a>

デフォルトの設定で簡単にマッチメイキング画面を表示します。

Sample

```
#import <AppSteroid/FASMatchmakingNavigationController.h>

	…
	…

- (IBAction)pushedMatchmakingButton:(id)sender
{
    [FASMatchmakingNavigationController presentMatchmakingWithTarget:self
                                                            animated:YES];
}
```

### <a name="SettingParameters"> パラメータを指定して表示する </a>

パラメータを指定してマッチメイキング画面を表示します。  
パラメータの種類は[FASMatchmakingViewController](../Specs/Spec-Matchmaking.md#FASMatchmakingNavigationController)を参照してください。

Sample

```
#import <AppSteroid/FASMatchmakingNavigationController.h>

@interface ViewController ()
<
    FASMatchmakingNavigationControllerDelegate
>

@end

	…
	…

- (IBAction)pushedMatchmakingButton:(id)sender
{
    FASMatchmakingNavigationController *matchmakingNavigationController = [FASMatchmakingNavigationController matchmakingNavigationController];
    FASMatchmakingViewController *matchmakingViewController = matchmakingNavigationController.matchmakingViewController;
    matchmakingViewController.minNumberOfPlayers = 3;
    matchmakingViewController.maxNumberOfPlayers = 6;
    [self presentViewController:matchmakingNavigationController animated:YES completion:nil];
}
```

### <a name="Segment"> マッチする条件を指定する </a>

マッチメイキングではマッチする条件を指定することができます。例えば同じ国の人同士でマッチングや同じレベルの人とマッチングといった指定をすることができます。利用するパラメータは[FASMatchmakingViewController#segment](../Specs/Spec-Matchmaking.md#FASMatchmakingNavigationController.segment)です。  
この`segment`に文字列を指定することで、同じ文字列を持っている人同士でマッチングを行います。例えば同じ国の人でマッチングしたい場合は

```
matchmakingViewController.segment = @"Japan";
```

と指定することで、同じ`Japan`という`segment`を指定している人とのみマッチングをすることが可能になります。ですので`segment`に`USA`と指定している人とはマッチングすることは出来なくなります。

### <a name="Layout"> レイアウトの変更 </a>

[FASLeaderboardLayout](../Specs/Spec-Matchmaking.md#FASMatchmakingLayout)クラスを利用することでレイアウトを変更することが出来ます。
それぞれのビューのレイアウトの変更方法については仕様書のサンプルコードを参照してください。

- [マッチメイキングビュー](../Specs/Spec-Matchmaking.md#FASMatchmakingLayout.matchmakingLayoutBlocks)

## <a name="HandlingMatchCompletion"> マッチの成立をハンドリングする </a>
マッチの成立後、マッチメイキングのビューを閉じてゲーム画面に遷移するコードは開発者の方に行ってもらう必要があります。  
まずはマッチの成立を受信するために、`NSNotificationCenter`を利用して通知の登録を行います。登録は`- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions`に記述することをお勧めします。これは、アプリ未起動時にマッチの招待(プッシュ通知)からアプリを起動した際に、マッチの成立の通知を受け取れるようにするためです。

```
#import <AppSteroid/FASMatchmakingViewController.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
	// マッチ成立時のイベントを登録
	[[NSNotificationCenter defaultCenter] addObserver:self
	                                         selector:@selector(matchmakingCompleted:)
	                                             name:kFASMatchmakingCompleted
	                                           object:nil];
	                                           
}

#pragma mark - FASMatchmakigViewController Notification methods

- (void)matchmakingCompleted:(NSNotification *)notification
{
	// マッチ成立時に呼ばれる
}

```

## <a name="GameContext"> ターン制ゲームへの対応 </a>
マッチ成立後にターン制ゲームを開始する場合は、[FASGameContext](Specs/Spec-Matchmaking.md#FASGameContext)を利用します。  
**ゲームコンテキスト**とは、マッチに参加しているプレイヤーに送信可能なオブジェクト（[FASGameContext](Specs/Spec-Matchmaking.md#FASGameContext)）です。

### <a name="GameContextEvent"> イベントの登録と削除 </a>
ゲームコンテキストを送信すると、相手プレイヤーにpath:`match_making/context`action:`created`の通知が送信されます。通知の登録方法は以下のサンプルコードを参照するか、[GetStarted-PushNotification](./GetStarted/GetStarted-PushNotification#ObserveEvent)を参照してください。

1. コンテキスト受信時のイベントを登録
2. ビューから離れた時にイベントの削除を行う
3. ゲームコンテキストを取得する
4. ゲームコンテキストの受信を処理する

```
#import <AppSteroid/FASGameContext.h>
#import <AppSteroid/FASEvent.h>

@implementation TurnBasedGameViewController
{
    FASObserver *_observer;
}

- (void)viewWillAppear:(BOOL)animated
{
    [super viewWillAppear:animated];
    
    // 1. コンテキスト受信時のイベントを登録
    _observer = [FASEvent observeEventWithPath:@"match_making/context"
                                        action:@"created"
                                  eventHandler:^(NSDictionary *params)
    {
        [self _fetchGameContext];
    }];
}

- (void)viewDidDisappear:(BOOL)animated
{
    [super viewDidDisappear:animated];
    
    // 2. ビューから離れた時にイベントの削除を行う
    [FASEvent unobserve:_observer];
}

- (void)_fetchGameContext
{
	// 3. ゲームコンテキストを取得する
    [FASGameContext fetchGameContextWithMatchId:@"match_id"
                                     completion:^(FASGameContext *gameContext, NSError *error)
     {
         // 4. ゲームコンテキストの受信を処理する
     }];
}

```

### <a name="GameContextUpdate"> ゲームコンテキストのアップデート </a>
ターンの終了時にゲームコンテキストをアップデートします。アップデートすると相手にプッシュ通知が送信され相手のターンになります。

1. ゲームコンテキストをアップデートする。
2. ゲームコンテキストのアップデートの完了を処理する。

```
- (IBAction)pushedSubmitButton:(id)sender
{
	// 1. ゲームコンテキストをアップデートする。
	[FASGameContext updateGameContextWithMatchId:@"match_id"
	                                       value:@{@"score" : @"100"}
                                      completion:^(FASGameContext *gameContext, NSError *error)
        {
             // 2. ゲームコンテキストのアップデートの完了を処理する。
         }];
    }
}
```