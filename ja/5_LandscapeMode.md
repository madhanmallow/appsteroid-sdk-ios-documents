# Landscapeモードのみのアプリに必要な追加実装

AppSteroidSDKが提供するGUI内ではテキストの入力などが必要な画面があり、Portraitモードにも対応させる必要があります。  
以下の手順を実装することにより、ゲーム自体はLandscapeモードになりますが、AppSteroidSDKが提供するGUI内ではLandscapeとPorrait両方をサポートすることが可能になります。

1. `AppDelegate.m`に以下を実装します。  

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