# Getting Started - Matchmaking

last update at 2014/10/7

---

- [マッチメイキング画面の表示](#HowToDisplayView)
	- [簡単に表示する](#EasyWay)
	- [パラメータを指定して表示する](#SettingParameters)
	- [レイアウトを変更する](#Layout)

---

## <a name="HowToDisplayView"> マッチメキング画面の表示 </a>

AppSteroidが提供するマッチメイキングのGUIを表示する方法を説明します。
マッチメイキング画面を表示すると自動的にマッチするユーザーを検索してマッチを成立させます。マッチが完了した後はデリゲートメソッドがコールされるようになっています。

### <a name="EasyWay"> 簡単に表示する </a>

デフォルトの設定で簡単にマッチメイキング画面を表示します。

Sample

```
#import <AppSteroid/FASGroupNavigationController.h>

	…
	…

- (IBAction)pushedMatchmakingButton:(id)sender
{
    [FASGroupNavigationController presentMatchmakingWithTarget:self
                                                      animated:YES];
}
```

### <a name="SettingParameters"> パラメータを指定して表示する </a>

パラメータを指定してマッチメイキング画面を表示します。
特に、マッチが成立した時に通知を受けれるようにするには、`matchmakingDelegate`を設定し、`FASMatchmakingNavigationControllerDelegate`のデリゲートメソッドを実装する必要があります。
その他のパラメータの設定項目に関しては[FASMatchmakingNavigationController](../Specs/Spec-Matchmaking.md#FASMatchmakingNavigationController)を参照してください。

Sample

```
#import <AppSteroid/FASGroupNavigationController.h>

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
    matchmakingNavigationController.minNumberOfPlayers = 2;
    matchmakingNavigationController.matchmakingDelegate = self;
    [self presentViewController:matchmakingNavigationController animated:YES completion:nil];
}

#pragma mark - FASMatchmakingNavigationControllerDelegate method

- (void)FASMatchmakingNavigationController:(FASMatchmakingNavigationController *)FASMatchmakingNavigationController
                      matchingWasCompleted:(FASMatch *)match
{
    [FASMatchmakingNavigationController dismissViewControllerAnimated:NO
                                                           completion:^
    {
        [self performSegueWithIdentifier:@"GameSegue" sender:match];
    }];
}

```

### <a name="Layout"> レイアウトの変更 </a>

[FASLeaderboardLayout](../Specs/Spec-Matchmaking.md#FASMatchmakingLayout)クラスを利用することでレイアウトを変更することが出来ます。
それぞれのビューのレイアウトの変更方法については仕様書のサンプルコードを参照してください。

- [マッチメイキングビュー](../Specs/Spec-Matchmaking.md#FASMatchmakingLayout.matchmakingLayoutBlocks)
