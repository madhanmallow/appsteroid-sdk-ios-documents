# Getting Started - User

last update at 2014/10/7

---

- [ユーザーの作成とログイン](#SignupAndLogin)
- [プロフィール画面の表示](#HowToDisplayView)
	- [簡単に表示する](#EasyWay)
	- [パラメータを指定して表示する](#SettingParameters)
	- [タブにフォーラムを組み込む](#WithTab)
	- [レイアウトを変更する](#Layout)

---

## <a name="SignupAndLogin"> ユーザーの作成とログイン </a>

AppSteroidのほとんどの機能を利用するにはユーザーを作成してログインする必要があります。
ユーザー作成は以下のサンプルのように実装することが出来ます。

Sample

```
#import <AppSteroid/FASAccount.h>

	…
	…

- (IBAction)pushedUserCreateButton:(id)sender
{
	[FASAccount signUpUserWithName:@"UserName"
						 completion:^(FASLoginUser *loginUser, NSError *error)
    {
        if (error)
        {
            // エラー
            NSLog(@"%@", error);
            return;
        }
    }];
}
```

ユーザーの作成が完了したら以下のサンプルのようにログインします。

Sample

```
#import <AppSteroid/FASAccount.h>

	…
	…

- (IBAction)pushedLoginButton:(id)sender
{
    [FASAccount loginUserWithCompletion:^(FASLoginUser *loginUser, NSError *error)
    {
        if (error)
        {
            // エラー
            NSLog(@"%@", error);
            return;
        }
    }];
}
```

また、既にユーザーが作成されているかどうか、ログイン状態が切れていないかどうかは以下の関数で知ることが出来ます。

```
// ユーザーが作成されているかどうか
if ([FASAccount currentLoggedInUser].isSignedUp)
{
    // 既にユーザーが作成されています
}

// ログイン状態が切れているかどうか
if ([FASAccount currentLoggedInUser].isExpiredSession)
{
    // ログイン状態が切れています
}
```

## <a name="HowToDisplayView"> プロフィール画面の表示 </a>

AppSteroidが提供するプロフィールのGUIを表示する方法を説明します。
プロフィール画面では、プロフィールの閲覧やチャットの開始、友達一覧の表示等の機能が利用出来ます。
また、自身のプロフィール画面ではプロフィールの編集も行えます。

### <a name="EasyWay"> 簡単に表示する </a>

デフォルトの設定で簡単に自身のプロフィール画面を表示します。

Sample

```
#import <AppSteroid/FASProfileNavigationController.h>

	…
	…

- (IBAction)pushedProfileButton:(id)sender
{
    [FASProfileNavigationController presentProfileWithTarget:self
                                                    animated:YES];
}
```

### <a name="SettingParameters"> パラメータを指定して表示する </a>

パラメータを指定してプロフィール画面を表示します。
`userId`にプロフィールを表示したいユーザーのIDを指定します。指定が無い場合は現在のログインユーザーのプロフィールを表示します。

Sample

```
#import <AppSteroid/FASProfileNavigationController.h>

	…
	…

- (IBAction)pushedProfileButton:(id)sender
{
    FASProfileNavigationController *profileNavigationController = [FASProfileNavigationController profileNavigationController];
    profileNavigationController.animated = YES;
    profileNavigationController.userId = @"xxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
    [self presentViewController:profileNavigationController animated:YES completion:nil];
}
```

### <a name="WithTab"> タブにプロフィールを組み込む </a>

[AppSteroidGetStarted](../AppSteroidGetStarted.md)の`タブ画面の表示`という項目を参照してください。

### <a name="Layout"> レイアウトの変更 </a>

[FASProfileLayout](../Specs/Spec-User.md#FASProfileLayout)クラスを利用することでレイアウトを変更することが出来ます。
それぞれのビューのレイアウトの変更方法については仕様書のサンプルコードを参照してください。

- [プロフィールビュー](../Specs/Spec-User.md#FASProfileLayout.profileLayoutBlocks)
- [プロフィール編集ビュー](../Specs/Spec-User.md#FASProfileLayout.editProfileLayoutBlocks)
- [友達リストビュー](../Specs/Spec-User.md#FASProfileLayout.friendListLayoutBlocks)
- [友達リクエストビュー](../Specs/Spec-User.md#FASProfileLayout.friendRequestLayoutBlocks)
