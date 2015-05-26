# Getting Started - Forum

last update at 2014/10/7

---

- [フォーラム画面の表示](#HowToDisplayView)
	- [簡単に表示する](#EasyWay)
	- [パラメータを指定して表示する](#SettingParameters)
	- [タブにフォーラムを組み込む](#WithTab)
	- [レイアウトを変更する](#Layout)

---

## <a name="HowToDisplayForumView"> フォーラム画面の表示 </a>

AppSteroidが提供するフォーラムのGUIを表示する方法を説明します。
フォーラムではスレッドの作成、コメントや画像を投稿してアプリ内のユーザーとコミュニケーションをとることが可能です。

### <a name="EasyWay"> 簡単に表示する </a>

デフォルトの設定で簡単にフォーラム画面を表示します。

Sample

```
#import <AppSteroid/FASForumNavigationController.h>

	…
	…

- (IBAction)pushedForumButton:(id)sender
{
    [FASForumNavigationController presentForumWithTarget:self
                                                animated:YES];
}
```

### <a name="SettingParameters"> パラメータを指定して表示する </a>

パラメータを指定してフォーラム画面を表示します。

Sample

```
#import <AppSteroid/FASForumNavigationController.h>

	…
	…

- (IBAction)pushedForumButton:(id)sender
{
    FASForumNavigationController *forumNavigationController = [FASForumNavigationController forumNavigationController];
    forumNavigationController.animated = YES;
    [self presentViewController:forumNavigationController
                       animated:YES
                     completion:nil];
}
```

### <a name="WithTab"> タブにフォーラムを組み込む </a>

[AppSteroidGetStarted](../AppSteroidGetStarted.md#ShowTab)を参照してください。

### <a name="Layout"> レイアウトの変更 </a>

[FASForumLayout](../Specs/Spec-Forum.md#FASForumLayout)クラスを利用することでレイアウトを変更することが出来ます。
それぞれのビューのレイアウトの変更方法については仕様書のサンプルコードを参照してください。

- [フォーラムビュー](../Specs/Spec-Forum.md#FASForumLayout.forumLayoutBlocks)
- [スレッドビュー](../Specs/Spec-Forum.md#FASForumLayout.forumThreadLayoutBlocks)
- [スレッド作成ビュー](../Specs/Spec-Forum.md#FASForumLayout.forumCreateThreadLayoutBlocks)
