# AppSteroid for iOS Get Started

last update at 2014/10/7

---

AppSteroid for iOSはiOS6.0以上をサポートしています。

## 導入

1. Frameworkのダウンロード

Fresviiのウェブサイトから以下のどちらかのフレームワークをダウンロードしてください。

```
- ボイスチャット無しのバージョン
	- appsteroid-ios-X.X.X.zip
- ボイスチャット機能ありのバージョン
	- appsteroid-ios-with-voicechat-X.X.X.zip
```
___ボイスチャットの利用にはこちらの`導入`と合わせて[GetStarted-VoiceChat.md](GetStarted/GetStarted-VoiceChat.md#HowToUseAPI)も参照してください。___


2. Frameworkの追加
`Build Phases`の`Link Binary With Libraries`に`AppSteroid.framework`以下を追加してください。
![framework](GetStarted/Images/ss_fresvii_01.png "AppSteroid.framework")

3. Bundleの追加
`Build Phases`の`Copy Bundle Resourves`に`AppSteroid.bundle`を追加してください。
![bundle](GetStarted/Images/ss_fresvii_02.png "AppSteroid.bundle")

4. Build Settings
`Other Linker Flags`に`-ObjC`を記述してください。
![flags](GetStarted/Images/ss_fresvii_03.png "Flags")

5. AppSteroidの利用を開始するためには、アプリケーションが起動するタイミングで初期設定をおこなう必要があります。
`AppDelegate.m`の`application:didFinishLaunchingWithOptions:`に[AppSteroid](AppSteroidSpec.md#AppSteroid)の[startWithAppIdentifier:secretToken:](AppSteroidSpec.md#AppSteroid.startWithAppIdentifiersecretToken)を記述してください。
このAPIはアプリIDとシークレットトークンを引数に渡す必要があります。

Sample

```
#import <AppSteroid/AppSteroid.h>

    …
    …

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // Start AppSteroid.
    NSString *appId = @"xxxxxxxxxxxxxxxxxxxxxxx";
    NSString *secretToken = @"yyyyyyyyyyyyyyyyyyyyyyyy";
    [AppSteroid startWithAppIdentifier:appId secretToken:secretToken];

	…
	…
	…

	return YES;
}
```

## タブ画面の表示

### 簡単に表示する

`Forum`,`Leaderboard`,`Profile`の順番にタブビューを表示します。
表示させたいビューを指定したりする場合は、下の`タブに表示するビューを指定する`を参照してください。

Sample

```
#import <AppSteroid/FASTabBarController.h>

	…
	…

- (IBAction)pushedTabButton:(id)sender
{
    [FASTabBarController presentTabBarControllerWithTarget:self
                                                  animated:YES];
}
```

### タブに表示するビューを指定する

利用したいビューを指定してタブビューを表示します。
詳しくはサンプルコードを参照してください。

Sample

```
#import <AppSteroid/FASTabBarController.h>

    …
    …

- (IBAction)pushedTabButton:(id)sender
{
    // Forum
    FASForumNavigationController *forumNavigationController = [FASForumNavigationController forumNavigationController];
    forumNavigationController.animated = YES;

    // Leaderboard
    NSString *leaderboardId = [[NSUserDefaults standardUserDefaults] objectForKey:@"leaderboardId"];
    FASSortOptions *dailyOption = [FASSortOptions dailyWithMinute:0 hour:0];
    FASLeaderboardNavigationController *leaderboardNavigationController = [FASLeaderboardNavigationController leaderboardNavigationController];
    leaderboardNavigationController.leaderboardId = leaderboardId;
    leaderboardNavigationController.onlyFriends = NO;
    leaderboardNavigationController.animated = YES;
    leaderboardNavigationController.dailySortOptions = dailyOption;

    // Group
    FASGroupNavigationController *groupNavigationController = [FASGroupNavigationController groupNavigationController];
    groupNavigationController.animated = YES;

    // Profile
    FASProfileNavigationController *profileNavigationController = [FASProfileNavigationController profileNavigationController];
    profileNavigationController.animated = YES;

    NSArray *controllers = @[
                             forumNavigationController,
                             leaderboardNavigationController,
                             groupNavigationController,
                             profileNavigationController
                             ];

    FASTabBarController *tabBarController = [[FASTabBarController alloc] init];
    tabBarController.viewControllers = controllers;
    [self presentViewController:tabBarController
                       animated:YES
                     completion:nil];
}
```
