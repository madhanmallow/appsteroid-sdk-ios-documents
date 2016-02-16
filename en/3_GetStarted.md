# Get Started with AppSteroid for iOS 

last update at 2015/12/10

---

- [Installation](#Installation)
- [Initial Settings](#Initialization)
- [Show AppSteroid Tab](#ShowTab)
- [How to update SDK](#HowToUpdate)

---

AppSteroid for iOS supports iOS7.0 and higher.  
Please make sure you have completed registering your App on the Web Console before implementing the SDK. [How to register your App](./2_AppRegistration.md)

## <a name="Installation"> Installation </a>

1. Download Framework

Download the Framework for iOS SDK from [Fresvii Website](https://fresvii.com/downloads)

2. Move the Framework and Bundle into your project directory.
![directory](GetStarted/Images/ss_fresvii_04.png "Framework and Bundle")

3. Add Framework
Add `AppSteroid.framework` to `Link Binary With Libraries` under `Build Phases`.(Please ignore this step if the framework is already added.)
![framework](GetStarted/Images/ss_fresvii_01.png "AppSteroid.framework")

4. Bundle Addition
Add `AppSteroid.bundle` to `Copy Bundle Resources` under `Build Phases`.(Please ignore this step if the bundle is already added.)
![bundle](GetStarted/Images/ss_fresvii_02.png "AppSteroid.bundle")

5. Build Settings
Please define the `-ObjC` under `Other Linker Flags`.
![flags](GetStarted/Images/ss_fresvii_03.png "Flags")

## <a name="Initialization"> Initialization </a>

In order to start using AppSteroid, you will need to perform a initial setup when the app launch.
Please define [startWithAppIdentifier:secretToken:](7_Spec.md#AppSteroid.startWithAppIdentifiersecretToken) under [AppSteroid](7_Spec.md#AppSteroid) for `application:didFinishLaunchingWithOptions:` under `AppDelegate.m`.
This API needs to pass the app ID and secret token as an argument. Check [How to register your app](./2_AppRegistration.md) for steps to get your App ID and secret token.

```obj-c
#import <AppSteroid/AppSteroid.h>
                           
    …
    …

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // Start AppSteroid.
    NSString *appId = @"xxxxxxxxxxxxxxxxxxxxxxx";
    NSString *secretToken = @"yyyyyyyyyyyyyyyyyyyyyyyy";
 #ifdef DEBUG
    BOOL development = YES;
 #else
    BOOL development = NO;
 #endif
    [AppSteroid startWithAppIdentifier:appId
                           secretToken:secretToken
                           development:development];
	
	…
	…
	…
	
	return YES;
}
```

## <a name="ShowGUI"> Show AppSteroidGUI </a>

You don't have to develop any function for user signup or login. AppSteroid will generating/login users automatically when the app is launched. Add the code below to instantly show GUI provided by AppSteroid.

```obj-c
- (IBAction)pushedTabButton:(id)sender
{
    [FASTabBarController presentTabBarControllerWithTarget:self
                                                  animated:YES];
}
```

## <a name="HowToUpdate"> How to Update SDK </a>

Noting special required. 
Delete the old SDK and install the latest version.