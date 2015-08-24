# Notification Specifications

last update at 2014/09/30

---

## Introduction

Specification for function related to PushNotification and Notification Event.
Functions such as, API to set device token on AppSteroid server or to observe a specific push notification to receive information are provided.

---

## Classes

|Class|Description|
|------|-----|
|[FASNotification](#FASNotification)|Class for handling PushNotification. |
|[FASEvent](#FASEvent)|Class to receive notification from an observed PushNotification. |
|[FASObserver](#FASObserver)|Class to be generated after registering observation on [FASEvent](#FASEvent). |


---

## APIs
### <a name="FASNotification"> FASNotification </a>
Class for handling PushNotification.

#### Constants
|Constant|Description|
|------|-----|
|[FASCertificateType](#FASNotification_FASCertificateType)|APNs Certificate type |

##### <a name="FASNotification_FASCertificateType"> FASCertificateType </a>
APNs Certificate type.

```obj-c
typedef NS_ENUM(NSInteger, FASCertificateType)
{
    FASCertificateTypeDevelopment = 0,
    FASCertificateTypeProduction  = 1
};
```

* Development: APNs Development iOS Certificate
* Production: APNs Production iOS Certificate


#### Class Methods

|Method|Description|
|------|-----|
|[addDeviceToken:completion:](#FASNotification.addDeviceTokencompletion) |Add a specified device token. |
|[addDeviceToken:certificateType:completion:](#FASNotification_addDeviceTokencertificateTypecompletion) |Add a specified device token with APNs type. |
|[deleteDeviceToken:completion:](#FASNotification.deleteDeviceTokencompletion) |Delete a specified device token. |
|[fetchNotificationMessageWithId:completion:](#FASNotification.fetchNotificationMessageWithIdcompletion) |Get detailed information about PushNotification. |
|[handleDidReceiveRemoteNotification:](#FASNotification.handleDidReceiveRemoteNotification) |Handel PushNotification sent through AppSteroid server. Especially, it is required to implement this method to use [FASEvent](#FASEvent).  |
|[allowsToHandlePushNotification:](#FASNotification.allowsToHandlePushNotification) |Setup to launch the feature related to the notification automatically or not, when launching the app from background using PushNotification send by AppSteroid. |
|[isAllowedToHandlePushNotification](#FASNotification.isAllowedToHandlePushNotification) |Return, to handle PushNotification related to AppSteroid or not. |

##### <a name="FASNotification.addDeviceTokencompletion"> addDeviceToken:completion: </a>
Add a specified device token.

\+ (void)addDeviceToken:(NSData *)deviceToken
             completion:(FASCompletionHandler)completion;

* Parameters
	* deviceToken
		* Device token required to receive PushNotification.
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (void)application:(UIApplication *)application
didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
	[FASNotification addDeviceToken:deviceToken
	                     completion:^(NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASNotification_addDeviceTokencertificateTypecompletion"> addDeviceToken:certificateType:completion: </a>
Add a specified device token with APNs type. Please see folloing link for more infomation. [What is Development Mode](../6_DevelopmentMode.md)

\+ (void)addDeviceToken:(NSData *)deviceToken
				certificateType:(FASCertificateType)certificateType
             completion:(FASCompletionHandler)completion;

* Parameters
	* deviceToken
		* Device token required to receive PushNotification.
	* certificateType
		* APNs certificate type in build environment.
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (void)application:(UIApplication *)application
didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
	[FASNotification addDeviceToken:deviceToken
	                     completion:^(NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASNotification.deleteDeviceTokencompletion"> deleteDeviceToken: </a>
Delete a specified device token.

\+ (void)deleteDeviceToken:(NSData *)deviceToken
                completion:(FASCompletionHandler)completion;

* Parameters
	* deviceToken
		* Device token required to receive PushNotification.
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASNotification deleteDeviceToken:deviceToken
                            completion:^(NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASNotification.fetchNotificationMessageWithIdcompletion"> fetchNotificationMessageWithId:completion: </a>
Get detailed information from id value stored in userInfo under PushNotification sent through AppSteroid server.

\+ (void)fetchNotificationMessageWithId:(NSString *)messageId
                             completion:(FASResponseCompletionHandler)completion;

* Parameters
	* messageId
		* Set id value stored in userInfo.
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (void)fetchNotificationMessageWithMessageId:(NSString *)messageId
{
    [FASNotification fetchNotificationMessageWithId:messageId
                                         completion:^(id response, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASNotification.handleDidReceiveRemoteNotification"> handleDidReceiveRemoteNotification: </a>
Handel PushNotification sent through AppSteroid server. Especially, it is required to implement this method to use [FASEvent](#FASEvent).

\+ (void)handleDidReceiveRemoteNotification:(NSDictionary *)userInfo;

* Parameters
	* userInfo
		* A method to receive PushNotification, `application:didReceiveRemoteNotification:` or `application:didReceiveRemoteNotification:fetchCompletionHandler:` is used as it is.

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (void)application:(UIApplication *)application
didReceiveRemoteNotification:(NSDictionary *)userInfo
{
    [FASNotification handleDidReceiveRemoteNotification:userInfo];
}
```

##### <a name="FASNotification.allowsToHandlePushNotification"> allowsToHandlePushNotification: </a>
Setup to launch the feature related to the notification automatically or not, when launching the app from background using PushNotification send by AppSteroid. Default setting is `Yes`.

\+ (void)allowsToHandlePushNotification:(BOOL)boolean;

* Parameters
	* boolean
		* Setting to handle the function related to notification or not.

Sample

```
#import <AppSteroid/FASNotification.h>

	…
	…

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
	…
	…
    [FASNotification allowsToHandlePushNotification:YES];
    …
    …
}
```

##### <a name="FASNotification.isAllowedToHandlePushNotification"> isAllowedToHandlePushNotification </a>
Return, to handle PushNotification related to AppSteroid or not.

\+ (BOOL)isAllowedToHandlePushNotification;

### <a name="FASEvent"> FASEvent </a>
A Class to observer PushNotification under AppSteroid and notify to a specified path and action.

#### Constants

|Constant|Description|
|------|-----|
|[FASEventHandler](#FASEvent.FASEventHandler) |Block object to be executed when receiving PushNotification related to the specified path and action. |

##### <a name="FASEvent.FASEventHandler"> FASEventHandler </a>
Block object to be executed when receiving PushNotification related to the specified path and action.


typedef void (^FASEventHandler)(NSDictionary *params);

* Parameters
	* params
		* Detail information about notification is stored in `NSDictionary` type.

#### Class Method

|Method|Description|
|------|-----|
|[observeEventWithDelegate:path:action:](#FASEvent.observeEventWithDelegatepathaction) |Add observation to receive notification through delegate method. |
|[observeEventWithPath:action:eventHandler:](#FASEvent.observeEventWithPathactioneventHandler) |Add observation to receive notification through block object. |
|[unobserve:](#FASEvent.unobserve)|Cancel observation. |

##### <a name="FASEvent.observeEventWithDelegatepathaction"> observeEventWithDelegate:path:action: </a>
Add observation to receive notification through delegate method.

\+ (FASObserver \*)observeEventWithDelegate:(id<FASEventDelegate>)delegate
                                       path:(NSString \*)path
                                     action:(NSString \*)action

* Parameters
	* delegate
		* Select a class to receive delegate method which is defined in [FASEventDelegate](#FASEventDelegate).
	* path
		* Select the name of the feature that triggered to send PushNotification. It deals with `resource` under `userInfo`.
	* action
		* Select the name of the features action that triggered to send PushNotification. It deals with `action` under `userInfo`.

* Return Value
	* [FASObserver](#FASObserver) Object. Used when using [unobserve:](#FASEvent.unobserve).

Sample

```
#import <AppSteroid/FASEvent.h>

	…
	…

@implementation FASEventViewController
{
    FASObserver *_observer;
}

- (void)viewDidLoad
{
	…
	…

	_observer = [FASEvent observeEventWithDelegate:self
	                                          path:@"user/friendship/request"
	                                        action:@"created"];
}

- (void)created:(NSDictionary *)params
{
	// It will be executed after receiving a specified path and action's PushNotification.
}
```

##### <a name="FASEvent.observeEventWithPathactioneventHandler"> observeEventWithPath:action:eventHandler: </a>
Add observation to receive notification through block object.

\+ (FASObserver \*)observeEventWithPath:(NSString \*)path
                                 action:(NSString \*)action
                           eventHandler:(FASEventHandler)handler

* Parameters
	* path
		* Select the name of the feature that triggered to send PushNotification. It deals with `resource` under `userInfo`.
	* action
		* Select the name of the features action that triggered to send PushNotification. It deals with `action` under `userInfo`.
	* handler
		* Block object to be executed when a PushNotification receives a notification.

* Return Value
	* [FASObserver](#FASObserver) Object. Used when using [unobserve:](#FASEvent.unobserve).


Sample

```
#import <AppSteroid/FASEvent.h>

	…
	…

@implementation FASEventViewController
{
    FASObserver *_observer;
}

- (void)viewDidLoad
{
	…
	…

	_observer = [FASEvent observeEventWithPath:@"user/friendship/request"
                                        action:@"created"
                                  eventHandler:^(NSDictionary *params)
    {
        // It will be executed after receiving a specified path and action's PushNotification.
    }];
}
```
##### <a name="FASEvent.unobserve"> unobserve: </a>
Cancel observation.

\+ (void)unobserve:(FASObserver \*)observer

* Parameters
	* observer
		* Select an object that was returned when adding observation.

Sample

```
#import <AppSteroid/FASEvent.h>

	…
	…

@implementation FASEventViewController
{
    FASObserver *_observer;
}

- (void)dealloc
{
	[FASEvent unobserve:_observer];
}
```

#### <a name="FASEventDelegate"> FASEventDelegate </a>
Delegate method to be called when receiving a PushNotification. This delegate method can be used when adding observation on `observeEventWithDelegate:path:action:`.

|Method|Description|
|------|-----|
|[created:](#FASEventDelegate.created) |Method to be called when `created` was the selected `action`. |
|[updated:](#FASEventDelegate.updated) |Method to be called when `updated` was the selected `action`. |
|[joined:](#FASEventDelegate.joined) |Method to be called when `joined` was the selected `action`. |
|[accepted:](#FASEventDelegate.accepted) |Method to be called when `accepted` was the selected `action`. |

##### <a name="FASEventDelegate.created"> created: </a>
Method to be called when `created` was the selected `action` under parameter, `userInfo`, in PushNotification.

\- (void)created:(NSDictionary *)params

* Parameters
	* params
		* userInfo, which you will get when receiving the PushNotification, is stored.

##### <a name="FASEventDelegate.updated"> updated: </a>
Method to be called when `updated` was the selected `action` under parameter, `userInfo`, in PushNotification.

\- (void)updated:(NSDictionary *)params

* Parameters
	* params
		* userInfo, which you will get when receiving the PushNotification, is stored.

##### <a name="FASEventDelegate.joined"> joined: </a>
Method to be called when `joined` was the selected `action` under parameter, `userInfo`, in PushNotification.

\- (void)joined:(NSDictionary *)params

* Parameters
	* params
		* userInfo, which you will get when receiving the PushNotification, is stored.

##### <a name="FASEventDelegate.accepted"> accepted: </a>
Method to be called when `accepted` was the selected `action` under parameter, `userInfo`, in PushNotification.

\- (void)accepted:(NSDictionary *)params

* Parameters
	* params
		* userInfo, which you will get when receiving the PushNotification, is stored.

### <a name="FASObserver"> FASObserver </a>
Class to be generated when adding observation on [FASEvent](#FASEvent). It will be used to cancel observation.
