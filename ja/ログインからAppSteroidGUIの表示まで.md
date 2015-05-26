
#　ログインして AppSteroid GUI を表示する

### 手順
- **Step 1.** [GettingStarted](./GettingStarted.md) を参考に初期設定を完了させてください。
- **Step 2.** サインアップ済みユーザーでログインする
  - **Case 1.** サインアップ済みのユーザーがいない場合　→　新たにサインアップしてログインする
  - **Case 2.** サインアップ済みユーザーがいる場合　→　サインアップ済みのユーザーからユーザーを選択してログインする
- **Step 3.** GUI を表示する

### サンプルコード
```
#import <AppSteroid/FASAccount.h>
#import <AppSteroid/FASTabBarController.h>
```
```
- (IBAction)pushedAppSteroidButton:(id)sender
{
	FASLoginUser *loginUser = [FASAccount currentLoggedInUser];	
	// サインアップ済みのユーザーがいない場合
    if (!loginUser || !loginUser.isSignedUp)
    {
		[FASAccount signUpUserCompletion:^(FASLoginUser *loginUser, NSError *error)
		{
			if (error)
			{
				NSLog(@"%@", error);
				return;
			}
			[FASTabBarController presentTabBarControllerWithTarget:self
												           animated:YES];
		}];
	}
	// サインアップ済みユーザーがいる場合
	else
	{
		[FASTabBarController presentTabBarControllerWithTarget:self
									           	   animated:YES];
	}
}
```