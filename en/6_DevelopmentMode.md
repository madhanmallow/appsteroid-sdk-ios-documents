# About Development Mode

---

## <a name="Introduction"></a>Description
All applications on AppSteroid have two data areas. One for development and other for production.  When you are operating your application on development mode, all datas will be stored on a different database from production where end-users would not have any access to it. (They will not see any text, images posted on development mode.) This allow you to test and develop your application without messing up your production data.


### <a name="development_mode"></a>Start Development Mode (Code example)

You can start the development mode by calling startWithAppIdentifier:secretToken:development: on startup.  An ideal use of this mode is for simulation on testing devices after building the app on development mode.  For distribution, the app should be build in production mode.  Following is a code example using Macro.

```obj-c
// AppDeletegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  …

#ifdef DEBUG
  [AppSteroid startWithAppIdentifier:"$YOUR_APP_ID"
                         secretToken:"$YOUR_APP_SECRET"
                         development:YES];
#else
  [AppSteroid startWithAppIdentifier:"$YOUR_APP_ID"
                         secretToken:"$YOUR_APP_SECRET"
                         development:NO];
#endif

  …

}

```

You can process the app on development mode by changing the Build Configuration to Debug, and change it to Release/AdHoc to process on production mode.

User data are saved separately per mode, so if you are using one device for both mode, the app will restore the user information that is tailored to the mode you are on. This allows you to easily switch between production data and development data on your development.

**※Note** All data managed on the Web Console is production data.


## About Types of APNs Certificate

APNs Certificate also have two different types, Development and Production. (Please check the iOS Dev Center for more information).

You can register either type of certificate, development or production, on the Web Console.  The certificate type registered on the web console and the Provisioning Profile type used on build **Must Match** to make it work.  (e.g. if the APNs on console is development, Provisioning Profile used for build must be development.)

Use the fowling method when registering the device token to check which Provisioning Profile you used on build.

```obj-c
// FASNotification.h
+ (void)addDeviceToken:(NSData *)deviceToken
       certificateType:(FASCertificateType)certificateType
            completion:(FASCompletionHandler)completion;
```


```obj-c
// AppDelegate.m
- (void)application:(UIApplication *)application
didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
  …
    [FASNotification addDeviceToken:deviceToken
                    certificateType:FASCertificateTypeDevelopment
                         completion:nil];
  …
}

```

If you call the method without the certificate type argument, it will consider "development" on development mode and "production" on production mode.  If the certificate type does not match, an error will be returned.


### Notes on Certificate Registration

If you Register Production APNs certificate for development mode environment on the Web Console and launch the App on Xcode with the Debug setting (Meaning Provisioning Profile is on development), the SDK will try to register the device token as Development automatically.  This will cause an error since the certificate registered on the server (Production) and the environment noticed on device token registration (Development) does not match.
You can avoid this error by selecting and calling FASCertificateTypeProduction on addDeviceToken:certificateType:completion.  It is the same other way around, (Registered Certificate: Development, Provisioning Profile used on Build: Production）


#### Simplest way for setup

1. Setup APNs Certificate for both Production and Development on the Web Console.
2. On development, build with Provisioning Profile(Development) and process as [Development Mode](#development_mode).
3. On production, build with Provisioning Profile(Distribution) and process as [Production Mode](#development_mode).

In this case, you can process the method on device token registration without the certificate type argument.
We highly recommend to use the settings above.
