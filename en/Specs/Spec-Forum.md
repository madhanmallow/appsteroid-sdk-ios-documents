# Forum Specifications

last update at 2014/10/24

---

## Introduction

Currently, we only provide the ability to display the GUI of the AppSteroid SDK Forum. Check [ForumGetStarted](../GetStarted/GetStarted-Forum.md) to see, how to display the GUI on your app.


---

## Classes

|Class|Description|
|------|-----|
|[FASForumNavigationController](#FASForumNavigationController)|NavigationController, which is the base of the Forum View|
|[FASForumLayout](#FASForumLayout)|Class to change layout of Forum View |

---


### <a name="FASForumNavigationController"> FASForumNavigationController </a>
NavigationController, which is the base of the Forum View

#### Properties

|Properties|Description|
|------|-----|
|[animated](#FASForumNavigationController.animated)|With or without the animation when closing the View |

##### <a name="FASForumNavigationController.animated"> animated </a>
A setting to close the view with or without an animation. Default setting is `YES`.

@property (nonatomic, assign) BOOL animated;

#### Class Method

|Method|Description|
|------|-----|
|[forumNavigationController](#FASForumNavigationController.forumNavigationController) |Return [FASForumNavigationController](#FASForumNavigationController), which is a base of Forum View |
|[presentForumWithTarget:animated:](#FASForumNavigationController.presentForumWithTargetanimated) |Show Forum View |

##### <a name="FASForumNavigationController.forumNavigationController"> forumNavigationController </a>
Return [FASForumNavigationController](#FASForumNavigationController), which is a base of Forum View

\+ (FASForumNavigationController *)forumNavigationController;

##### <a name="FASForumNavigationController.presentForumWithTargetanimated"> presentForumWithTarget:animated: </a>
Show `Forum` View

+ (void)presentForumWithTarget:(UIViewController *)target
                      animated:(BOOL)animated;

* Parameters
	* target
		* Select the base ViewController to display View.
	* animated
		* Yes will transit with animation. No will transit without animation.

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
You can change layout related to Forum View.

#### Properties

|Properties|Description|
|------|-----|
|[forumLayoutBlocks](#FASForumLayout.forumLayoutBlocks)|Block object used to change layout of Forum View |
|[forumThreadLayoutBlocks](#FASForumLayout.forumThreadLayoutBlocks)|Block object used to change layout of Thread View |
|[forumCreateThreadLayoutBlocks](#FASForumLayout.forumCreateThreadLayoutBlocks)|Block object used to change layout of Thread Creation View |

##### <a name="FASForumLayout.forumLayoutBlocks"> forumLayoutBlocks </a>
Block object used to change layout of Forum View

@property (nonatomic, copy) FASForumViewController *(^forumLayoutBlocks)(FASForumViewController *forumViewController);

Sample - Changing background color and navigation bar

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
Block object used to change layout of Thread View

@property (nonatomic, copy) FASForumThreadViewController *(^forumThreadLayoutBlocks)(FASForumThreadViewController *forumThreadViewController);

Sample - Changing background color

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
Block object used to change layout of Thread Creation View

@property (nonatomic, copy) FASForumCreateThreadViewController *(^forumCreateThreadLayoutBlocks)(FASForumCreateThreadViewController *forumCreateThreadViewController);

Sample - Changing background color

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
|[sharedInstance](#FASForumLayout.sharedInstance) |Return the object |

##### <a name="FASForumLayout.sharedInstance"> sharedInstance </a>
Return the object

\+ (instancetype)sharedInstance;
