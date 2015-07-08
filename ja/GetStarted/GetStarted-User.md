# Getting Started - User

last update at 2014/10/7

---

- [ユーザーの作成とログイン](#SignupAndLogin)

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
