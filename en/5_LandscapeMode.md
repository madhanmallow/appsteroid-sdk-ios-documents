# Additional Implementation Required for Landscape Mode Games

It is highly recommended to support Portrait mode to get the best result for AppSteroid GUI.
Please follow the steps described below to support both Landscape and Portrait mode. Your game will remain Landscape.

1. Implement the following code under `AppController.mm` in `ios` directory.  

```
#import <AppSteroid/AppSteroid.h>
```
```
-(UIInterfaceOrientationMask)application:(UIApplication *)application
supportedInterfaceOrientationsForWindow:(UIWindow *)window
{
    if (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPhone)
    {
        if ([AppSteroid isAppSteroidGUI])
        {
            return UIInterfaceOrientationMaskAllButUpsideDown;
        }
        else
        {
            return UIInterfaceOrientationMaskLandscape;
        }
    }
    else  /* iPad */
    {
        if ([AppSteroid isAppSteroidGUI])
        {
            return UIInterfaceOrientationMaskAllButUpsideDown;
        }
        else
        {
            return UIInterfaceOrientationMaskLandscape;
        }
    }
}
```

2. Implement the following under `RootViewController.mm`.

```
-(void)viewWillAppear:(BOOL)animated {
    cocos2d::Director::getInstance()->resume();
    cocos2d::Director::getInstance()->startAnimation();
}

- (void)viewWillDisappear:(BOOL)animated {
    cocos2d::Director::getInstance()->pause();
    cocos2d::Director::getInstance()->stopAnimation();
}

- (NSUInteger) supportedInterfaceOrientations {
    return UIInterfaceOrientationMaskLandscape;
}
```