# Getting Started - Push Notification

last update at 2014/09/30

---

- [How To Setup Push Notification](#HowToSetupPushNotification)
	- [Register Certificate](#RegisterCertificates)
	- [Create p12 File](#CreateFiles)
	- [Upload p12 File](#UploadFiles)
	- [Implement Codes](#ImplementCodes)
- [Observing Push Notification Event](#ObserveEvent)
- [Sending Custom Message](#CustomMessage)
	- [Setting Channel](#SettingChannel)
	- [Using Storage](#UseKVS)
    - [Sending Message](#SendMessage)
- [Directly Show AppSteroid View](#DisplayFresviiGUI)

---

## <a name="HowToSetupPushNotification"> How To Setup Push Notification </a>

### <a name="RegisterCertificates"> Register Certificate </a>

Download your Push Notification certificate generated on iOS Dev Center.
![pn01](Images/ss_fresvii_pn_01.png "PN01")
Register your certificate on KeyChain, which will be registered with the name listed below.
* For Development : Apple Development IOS Push Services: Your.Bundle.ID
* For Production : Apple Production IOS Push Services: Your.Bundle.ID

### <a name="CreateFiles"> Create p12 File </a>

Open KeyChain, right click the certificate you've registered and select "Export".
![pn02](Images/ss_fresvii_pn_02.png "PN02")
Enter the file name and make sure the file format is "Personal Information Exchange(.p12)" before you "Save" it.
![pn03](Images/ss_fresvii_pn_03.png "PN03")
Enter the password and create your p12 file.
![pn04](Images/ss_fresvii_pn_04.png "PN04")

### <a name="UploadFiles"> Upload p12 File </a>

Login to the console [Fresvii](https://fresvii.com/), go to Settings->Notification and upload your p12 file. (1)
Enter the password you've setup when exporting the p12 file. (2)
Do not forget to click the `save` button after you setup. (3)
![pn05](Images/ss_fresvii_pn_05.png "PN05")
After a success upload, a screen like below will show up.
![pn06](Images/ss_fresvii_pn_06.png "PN06")

### <a name="ImplementCodes"> Implement Codes </a>

Implementation on `AppDelegate.h`, like shown below, is required to use push notification.

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
	…
	…

   [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge|
                                                     UIRemoteNotificationTypeSound|
                                                     UIRemoteNotificationTypeAlert)];

    return YES;
}

#pragma mark - Remote Push Notification methods.

- (void)application:(UIApplication *)application
didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    [FASNotification addDeviceToken:deviceToken completion:nil];
}

- (void)application:(UIApplication*)application
didFailToRegisterForRemoteNotificationsWithError:(NSError *)error
{
    LOG(@"Errorinregistration:%@",error);
}
```

## <a name="ObserveEvent"> Observing Push Notification Event </a>

Implementation on `AppDelegate.h`, like shown below, is required to observe push notification event related to AppSteroid.


```
#import <AppSteroid/FASNotification.h>

	…
	…

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
	…
	…

    [FASNotification handleDidFinishLaunchingWithOptions:launchOptions];

    return YES;
}

- (void)application:(UIApplication *)application
didReceiveRemoteNotification:(NSDictionary *)userInfo
{
    [FASNotification handleDidReceiveRemoteNotification:userInfo];
}

- (void)application:(UIApplication *)application
didReceiveRemoteNotification:(NSDictionary *)userInfo
fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
{
    completionHandler(UIBackgroundFetchResultNewData);
    [FASNotification handleDidReceiveRemoteNotification:userInfo];
}
```

If the settings shown above is completed, using [FASEvent](../Specs/Spec-Notification.md#FASEvent) enables to observe the event.
The code listed below is a sample code to observe friend request event.

Sample

```
#import <AppSteroid/FASEvent.h>

@implementation ViewController
{
    FASObserver *_observer;
}

- (void)viewWillAppear:(BOOL)animated
{
    [super viewWillAppear:animated];

    [self _observeEvent];
}

- (void)viewWillDisappear:(BOOL)animated
{
    [super viewWillDisappear:animated];

    [self _unobserveEvent];
}

- (void)_observeEvent
{
    _observer = [FASEvent observeEventWithPath:@"user/friendship/request"
                                        action:@"created"
                                  eventHandler:^(NSDictionary *params)
    {
        // Details of notification content is stored in params
    }];
}

- (void)_unobserveEvent
{
    [FASEvent unobserve:_observer];
}
```

## <a name="CustomMessage"> Sending Custom Message </a>

[FASCustomMessage](../Specs/Spec-Notification.md#FASCustomMessage) is used to send custom message to a specific user.
It will sent notification to users relevant to the channel setting.  Channel need to be setup on Fresvii web console.

### <a name="SettingChannel"> Setting Channel </a>

Channel can be setup on Fresvii web console.
The sample shows, how to pin down users who are using [Key-Value Storage](../Specs/Spec-Storage.md#FASStorage).

First setup the channel on the web console.
Use a variable, `bind_level`, to pin down the user for the key, `level`.

```

```

### <a name="UseKVS"> Using Storage </a>

Save a value, `10`, in the storage for the key, `level`.

Sample

```
#import <AppSteroid/FASStorage.h>

	…
	…

- (IBAction)pushedAddLevelButton:(id)sender
{
    NSDictionary *data = @{@"level" : @"10"};
    [FASStorage addData:data
             completion:^(NSError *error)
    {
        if (error)
        {
            // Error
            return;
        }

        // Success
    }];
}
```

### <a name="SendMessage"> Sending Message </a>

Send message to users who matches `level == 10`.

Sample

```
#import <AppSteroid/FASCustomMessage.h>

	…
	…

- (IBAction)pushedSendMessageToSameLevelUserButton:(id)sender
{
    // Channel name which was set upped on the web console
    NSString *channelName = @"level";
    // Parameter and value which was set upped on the web console
    NSDictionary *channelParams = @{@"bind_level" : @"10"};

    [FASCustomMessage sendMessageWithChannelName:channelName
                                          action:@"created"
                                   channelParams:channelParams
                                          params:nil
                                         subject:@"subject"
                                           sound:nil
                                     apnsEnabled:YES
                                      gcmEnabled:YES
                                      completion:^(FASCustomMessage *message, NSError *error)
    {
        if (error)
        {
            // Error
            return;
        }

        // Success
    }];
}
```

## <a name="DisplayFresviiGUI"> Directly Show AppSteroid View </a>

Directly show the relevant GUI provided by AppSteroid, when the app launches from push notification.
For example, a user can directly jump to "thread A" when receiving a notification about "thread A".  This function is set as a default feature. However, additional setup is required to prevent user to exist the game from a push notification.


```
// Automatically jumps to the target GUI from push notification.
[FASNotification allowsToHandlePushNotification:YES];

// Launch the app by tapping the push notification, but does not jump to the target GUI.
[FASNotification allowsToHandlePushNotification:NO];
```
