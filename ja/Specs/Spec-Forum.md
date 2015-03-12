# Forum Specifications

last update at 2014/10/7

---

## Introduction

フォーラムに関する機能の仕様書です。
現在はAppSteroidが提供するフォーラムのGUIを表示する機能のみ提供されています。表示方法は[ForumGetStarted](../GetStarted/GetStarted-Forum.md)を参照してください。

---

## Classes

|Class|Description|
|------|-----|
|[FASForumNavigationController](#FASForumNavigationController)|フォーラムビューのベースとなるNavigationController |
|[FASForumLayout](#FASForumLayout)|フォーラムビュー関連のレイアウトを変更するためのクラス |
---


### <a name="FASForumNavigationController"> FASForumNavigationController </a>
フォーラムビューのベースとなるNavigationController。

#### Properties

|Properties|Description|
|------|-----|
|[animated](#FASForumNavigationController.animated)|ビューを閉じるときのアニメーション有無 |

##### <a name="FASForumNavigationController.animated"> animated </a>
ビューを閉じるときにアニメーション付きで閉じるかどうかを設定します。デフォルトは`YES`です。

@property (nonatomic, assign) BOOL animated;

#### Class Method

|Method|Description|
|------|-----|
|[forumNavigationController](#FASForumNavigationController.forumNavigationController) |フォーラムビューのベースとなる[FASForumNavigationController](#FASForumNavigationController)を返却します。 |
|[presentForumWithTarget:animated:](#FASForumNavigationController.presentForumWithTargetanimated) |フォーラムビューを表示します。 |

##### <a name="FASForumNavigationController.forumNavigationController"> forumNavigationController </a>
フォーラムビューのベースとなる[FASForumNavigationController](#FASForumNavigationController)を返却します。

\+ (FASForumNavigationController *)forumNavigationController;

##### <a name="FASForumNavigationController.presentForumWithTargetanimated"> presentForumWithTarget:animated: </a>
`フォーラム`ビューを表示します。

+ (void)presentForumWithTarget:(UIViewController *)target
                      animated:(BOOL)animated;

* Parameters
	* target
		* ビューを表示する元となるViewControllerを指定します。
	* animated
		* YESならアニメーションさせて遷移します。NOならアニメーションはしません。

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


### <a name="FASForumLayout"> FASForumLayout </a>
フォーラムビュー関連のレイアウトを変更します。

#### Properties

|Properties|Description|
|------|-----|
|[forumLayoutBlocks](#FASForumLayout.forumLayoutBlocks)|フォーラムビューのレイアウトを変更するためのブロックオブジェクト |
|[forumThreadLayoutBlocks](#FASForumLayout.forumThreadLayoutBlocks)|スレッドビューのレイアウトを変更するためのブロックオブジェクト |
|[forumCreateThreadLayoutBlocks](#FASForumLayout.forumCreateThreadLayoutBlocks)|スレッド作成ビューのレイアウトを変更するためのブロックオブジェクト |

##### <a name="FASForumLayout.forumLayoutBlocks"> forumLayoutBlocks </a>
フォーラムビューのレイアウトを変更するためのブロックオブジェクト

@property (nonatomic, copy) FASForumViewController *(^forumLayoutBlocks)(FASForumViewController *forumViewController);

Sample - 背景色とナビゲーションバーを変更するサンプル

```
    [FASForumLayout sharedInstance].forumLayoutBlocks = ^FASForumViewController *(FASForumViewController *forumViewController)
    {
        forumViewController.view.backgroundColor = [UIColor whiteColor];
        forumViewController.navigationController.navigationBar.barStyle = UIBarStyleDefault;
        forumViewController.navigationController.navigationBar.tintColor = [UIColor greenColor];
        forumViewController.navigationController.navigationBar.barTintColor = [UIColor whiteColor];
        forumViewController.navigationController.navigationBar.titleTextAttributes = @{NSForegroundColorAttributeName: [UIColor blackColor]};
        forumViewController.forumCellLayoutBlocks = ^FASForumCell *(FASForumCell *forumCell)
        {
            forumCell.backgroundColor = [UIColor whiteColor];
            forumCell.contentView.backgroundColor = [UIColor whiteColor];
            return forumCell;
        };
        return forumViewController;
    };
```

##### <a name="FASForumLayout.forumThreadLayoutBlocks"> forumThreadLayoutBlocks </a>
スレッドビューのレイアウトを変更するためのブロックオブジェクト

@property (nonatomic, copy) FASForumThreadViewController *(^forumThreadLayoutBlocks)(FASForumThreadViewController forumThreadViewController);

Sample - 背景色を変更するサンプル

```
[FASForumLayout sharedInstance].forumThreadLayoutBlocks = ^FASForumThreadViewController *(FASForumThreadViewController *forumThreadViewController)
    {
        forumThreadViewController.view.backgroundColor = [UIColor whiteColor];
        forumThreadViewController.forumThreadCellLayoutBlocks = ^(FASForumThreadCell *forumThreadCell)
        {
            forumThreadCell.backgroundColor = [UIColor whiteColor];
            forumThreadCell.contentView.backgroundColor = [UIColor whiteColor];
            return forumThreadCell;
        };
        return forumThreadViewController;
    };
```

##### <a name="FASForumLayout.forumCreateThreadLayoutBlocks"> forumCreateThreadLayoutBlocks </a>
スレッド作成ビューのレイアウトを変更するためのブロックオブジェクト

@property (nonatomic, copy) FASForumCreateThreadViewController *(^forumCreateThreadLayoutBlocks)(FASForumCreateThreadViewController *forumCreateThreadViewController);

Sample - 背景色を変更するサンプル

```
[FASForumLayout sharedInstance].forumCreateThreadLayoutBlocks = ^FASForumCreateThreadViewController *(FASForumCreateThreadViewController *forumCreateThradViewController)
    {
        [forumCreateThradViewController.chooseButton setTitleColor:[UIColor blackColor] forState:UIControlStateNormal];
        forumCreateThradViewController.view.backgroundColor = [UIColor whiteColor];
        return forumCreateThradViewController;
    };
```

#### Class Method

|Method|Description|
|------|-----|
|[sharedInstance](#FASForumLayout.sharedInstance) |唯一のオブジェクトを返却します。 |

##### <a name="FASForumLayout.sharedInstance"> sharedInstance </a>
唯一のオブジェクトを返却します。

\+ (instancetype)sharedInstance;
