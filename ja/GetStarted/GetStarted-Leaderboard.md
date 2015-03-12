# Getting Started - Leaderboard

last update at 2014/10/7

---

- [リーダーボード画面の表示](#HowToDisplayView)
	- [簡単に表示する](#EasyWay)
	- [パラメータを指定して表示する](#SettingParameters)
	- [タブにリーダーボードを組み込む](#WithTab)
	- [レイアウトを変更する](#Layout)
- [リーダーボードAPIの利用](#HowToUseAPI)
	- [スコアの登録](#SubmitScore)

---

## <a name="HowToDisplayView"> リーダーボード画面の表示 </a>

AppSteroidが提供するリーダーボードのGUIを表示する方法を説明します。
リーダーボード画面ではランキングやスコアを閲覧することが出来ます。
リーダーボードの作成はFresviiのウェブコンソールから行います。

### <a name="EasyWay"> 簡単に表示する </a>

デフォルトの設定で簡単にリーダーボード画面を表示します。
表示されるリーダーボードは最新のリーダーボードのみです。

Sample

```
#import <AppSteroid/FASLeaderboardNavigationController.h>

	…
	…

- (IBAction)pushedLeaderboardButton:(id)sender
{
    [FASLeaderboardNavigationController presentLeaderboardWithTarget:self
                                                            animated:YES];
}
```

### <a name="SettingParameters"> パラメータを指定して表示する </a>

パラメータを指定してリーダーボード画面を表示します。
リーダーボードのIDはFresviiのウェブコンソールに表示されています。

Sample

```
#import <AppSteroid/FASLeaderboardNavigationController.h>

	…
	…

- (IBAction)pushedLeaderboardButton:(id)sender
{
    NSString *leaderboardId = @"xxxxxxxxxxxxxxxxxxxxxxxx";
    FASLeaderboardNavigationController *leaderboardNavigationController = [FASLeaderboardNavigationController leaderboardNavigationController];
    leaderboardNavigationController.leaderboardId = leaderboardId;
    leaderboardNavigationController.onlyFriends = NO;

    [self presentViewController:leaderboardNavigationController
                       animated:YES
                     completion:nil];
}
```

### <a name="WithTab"> タブにリーダーボードを組み込む </a>

[AppSteroidGetStarted](../AppSteroidGetStarted.md)の`タブ画面の表示`という項目を参照してください。

### <a name="Layout"> レイアウトの変更 </a>

[FASLeaderboardLayout](../Specs/Spec-Leaderboard.md#FASLeaderboardLayout)クラスを利用することでレイアウトを変更することが出来ます。
それぞれのビューのレイアウトの変更方法については仕様書のサンプルコードを参照してください。

- [リーダーボードビュー](../Specs/Spec-Leaderboard.md#FASLeaderboardLayout.leaderboardLayoutBlocks)

---

## <a name="HowToUseAPI"> リーダーボードAPIの利用 </a>

### <a name="SubmitScore"> スコアの登録 </a>

[FASScore](../Specs/Spec-Leaderboard.md#FASScore)の[submitScoreWithLeaderboardId:value:completion:](../Specs/Spec-Leaderboard.md#FASScore.submitScoreWithLeaderboardIdvaluecompletion)を利用して対象のリーダーボードに対してスコアを登録します。

Sample
0〜1000のランダムな値をスコアとして登録する

```
#import <AppSteroid/FASScore.h>

	…
	…

- (IBAction)pushedSubmitButton:(id)sender
{
    NSString *leaderboardId = @"xxxxxxxxxxxxxxxxxx";
    int score = arc4random() % 1000;
    [FASScore submitScoreWithLeaderboardId:leaderboardId
                                     value:score
                                completion:nil];
}
```
