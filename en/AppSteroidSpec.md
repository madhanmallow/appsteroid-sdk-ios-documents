# AppSteroid for iOS SDK Specification

last update at 2014/2/26

---

## Introduction
AppSteroid for iOS is an integrated backend gaming service for iOS.
With AppSteroid, you can easily incorporate various backend services refined to mobile games into your apps for free.

---

## Classes

|Common Classes|Description|
|------|-----|
|[AppSteroid](#AppSteroid)|AppSteroid Initially Set Class |
|[FASTabBarController](#FASTabBarController)|Class to access TabBarController provided by AppSteroid |
|[FASPagingMeta](#FASPagingMeta)|Class storing meta information of array data. |

|User|Description|
|------|-----|
|[FASAccount](Specs/Spec-User.md#FASAccount)|Logged in user's account operation class |
|[FASSNSAccount](Specs/Spec-User.md#FASSNSAccount)|SNS account operation class |
|[FASLoginUser](Specs/Spec-User.md#FASLoginUser)|Login User model class |
|[FASUser](Specs/Spec-User.md#FASUser)|User model class|
|[FASProfileNavigationController](Specs/Spec-User.md#FASProfileNavigationController)|NavigationController for profile View |

|Notification|Description|
|------|-----|
|[FASNotification](Specs/Spec-Notification.md#FASNotification)|Class to operate device token for PushNotification |
|[FASEvent](Specs/Spec-Notification.md#FASEvent)|Class to observe PushNotification and receive notification |
|[FASObserver](Specs/Spec-Notification.md#FASObserver)|Class to be generated after adding observation on [FASEvent](Specs/Spec-Notification.md#FASEvent) |

|Message|Description|
|------|-----|
|[FASDirectMessage](Specs/Spec-Message.md#FASDirectMessage)|Class to operate direct message send from Fresvii web console |
|[FASCustomMessage](Specs/Spec-Message.md#FASCustomMessage)|Class related to function sending push message to a specific user |

|Key-Value Storage|Description|
|------|-----|
|[FASStorage](Specs/Spec-Storage.md#FASStorage)|Class to operate Key-Value Storage provided by AppSteroid |

|Voice Chat|Description|
|------|-----|
|[FASConference](Specs/Spec-VoiceChat.md#FASConference)|Class for function related to Voice Chat |

|Play Movie|Description|
|------|-----|
|[FASVideo](Specs/Spec-PlayMovie.md#FASVideo)|Class to operate recorded play movie |
|[FASMovieMaker](Specs/Spec-MovieMaker.md#FASMovieMaker)|Class for function to recored game play movie |

|Play Statistics|Description|
|------|-----|
|[FASPlayStats](Specs/Spec-PlayStats.md#FASPlayStats)|Class to get statistical information |


|Forum|Description|
|------|-----|
|[FASForumNavigationController](Specs/Spec-Forum.md#FASForumNavigationController)|NavigationController for Forum View |

|Group|Description|
|------|-----|
|[FASGroup](Specs/Spec-Group.md#fASGroup)|Group model Class |
|[FASGroupMember](Specs/Spec-Group.md#FASGroupMember)|Group Member model Class |
|[FASGroupMessage](Specs/Spec-Group.md#FASGroupMessage)|Group Message model Class |
|[FASGroupNavigationController](Specs/Spec-Group.md#FASGroupNavigationController)|NavigationController Group View |

|Leaderboard|Description|
|------|-----|
|[FASLeaderboard](Specs/Spec-Leaderboard.md#FASLeaderboard)|Leaderboard model Class |
|[FASScore](Specs/Spec-Leaderboard.md#FASScore)|Score model Class |
|[FASRank](Specs/Spec-Leaderboard.md#FASRank)|Rank model Class |
|[FASSortOptions](Specs/Spec-Leaderboard.md#FASSortOptions)|Ranking Aggregation Class |
|[FASLeaderboardNavigationController](Specs/Spec-Leaderboard.md#FASLeaderboardNavigationController)|NavigationController for Leaderboard |

|Matchmaking|Description|
|------|-----|
|[FASMatch](Specs/Spec-Matchmaking.md#FASMatch)|Match model Class |
|[FASMatchRequest](Specs/Spec-Matchmaking.md#FASMatchRequest)|Match Request model Class |
|[FASMatchInvitation](Specs/Spec-Matchmaking.md#FASMatchInvitation)|Match Invitation model Class |
|[FASMatchPlayer](Specs/Spec-Matchmaking.md#FASMatchPlayer)|Match Player model Class |
|[FASGameContext](Specs/Spec-Matchmaking.md#FASGameContext)|Game Context model Class |
|[FASMatchmakingNavigationController](Specs/Spec-Matchmaking.md#FASMatchmakingNavigationController)|NavigationController for Matchmaking |

---

## APIs
### <a name="AppSteroid"> AppSteroid </a>
A common setup is available to use the SDK.
You can also get user data using this Class.

#### Constants

|Constant|Description|
|------|-----|
|[FASTab](#AppSteroid.FASTab)|Tabs that can be displayed with [FASTabBarController](#FASTabBarController) are defined |
|[FASResponseCompletionHandler](#AppSteroid.FASResponseCompletionHandler)|Block Object to be executed when loading or uploading to the network or to the database is completed. |
|[FASCompletionHandler](#AppSteroid.FASCompletionHandler)|Block object to be executed only to notify if the process is completed or not.|

##### <a name="AppSteroid.FASTab"> FASTab </a>
Tabs that can be displayed with [FASTabBarController](#FASTabBarController) are defined

```
typedef NS_ENUM(NSInteger, FASTab)
{
    FASTabForum       = (1UL << 0),
    FASTabLeaderboard = (1UL << 1),
    FASTabGroup       = (1UL << 2),
    FASTabProfile     = (1UL << 3)
};
```

###### Constants
###### FASTabForum
Forum Tab

###### FASTabLeaderboard
Leaderboard Tab

###### FASTabGroup
Group Tab

###### FASTabProfile
Profile Tab

##### <a name="AppSteroid.FASResponseCompletionHandler"> (^FASResponseCompletionHandler)(id response, NSError *error) </a>
Block Object to be executed when loading or uploading to the network or to the database is completed.

typedef void (^FASResponseCompletionHandler)(id response, NSError *error)

* Parameters
  * response
    * Process result is stored.
  * error
    * Error detail is stored. It will be nil if there is no error.

##### <a name="AppSteroid.FASCompletionHandler"> (^FASCompletionHandler)(NSError *error) </a>
Block object to be executed only to notify if the process is completed or not.

typedef void (^FASCompletionHandler)(NSError *error)

* Parameters
  * error
    * Error detail is stored. It will be nil if there is no error.

#### Class Methods

|Method|Description|
|------|-----|
|[startWithAppIdentifier:secretToken:](#AppSteroid.startWithAppIdentifiersecretToken)|Initial setup to start using the SDK. |
|[startWithAppIdentifier:secretToken:development:](#AppSteroid_startWithAppIdentifiersecretTokendevelopment)|Initial setup to start using the SDK with development mode flag. |
|[setTimeout:](#AppSteroid.setTimeout)|Setup a timeout for network connection. |
|[setTabs:](#AppSteroid.setTabs)|Set tabs to display |
|[sdkVersion](#AppSteroid.sdkVersion)|Return SDK Version |
|[sdkBuildVersion](#AppSteroid.sdkBuildVersion)|Return SDK build version |

##### <a name="AppSteroid.startWithAppIdentifiersecretToken"> startWithAppIdentifier:secretToken: </a>
Initial setup to start using the SDK.

\+ (void)startWithAppIdentifier:(NSString *)appIdentifier secretToken:(NSString *)secretToken

* Parameters
  * appIdentifier
    * Application ID
  * secretToken
    * SecretToken

##### <a name="AppSteroid_startWithAppIdentifiersecretTokendevelopment"> startWithAppIdentifier:secretToken:development: </a>
Initial setup to start using the SDK. app can work for development mode. Please see following link. [What is Development Mode](./DevelopmentMode.md)

\+ (void)startWithAppIdentifier:(NSString *)appIdentifier
                    secretToken:(NSString *)secretToken
                    development:(BOOL)development;

* Parameters
  * appIdentifier
    * Application ID
  * secretToken
    * SecretToken
  * development
    * If it is set to YES, the app is going to work as development mode. you must make it "NO" for distribution.

Sample

```
#import <AppSteroid/AppSteroid.h>

  …
  …

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // Required.
    // Start AppSteroid.
  NSString *appId = @"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
  NSString *secretToken = @"yyyyyyyyyyyyyyyyyyyyyyyyyyyy";
  [AppSteroid startWithAppIdentifier:appId secretToken:secretToken development:NO];

  // Optional.
  // You can set network timeout. Default is 30.0.
  [AppSteroid setTimeout:20.0];

  …
  …
   …

  return YES;
}
```

##### <a name="AppSteroid.setTimeout"> setTimeout: </a>
Setup a timeout for network connection.
Default value is 30 second.

\+ (void)setTimeout:(NSUInteger)timeout

* Parameters
  * timeout
    * Timeout in second


##### <a name="AppSteroid.setTabs"> setTabs: </a>
Set tabs to display
Default tabs are, `FASTabForum | FASTabLeaderboard | FASTabGroup | FASTabProfile`.

\+ (void)setTabs:(FASTab)tabs

* Parameters
  * tabs
    * Tabs defined in [FASTab](#AppSteroid.FASTab). You can select tabs like the example, `FASTabForum | FASTabProfile`.

Sample

```
[AppSteroid setTabs:FASTabForum | FASTabLeaderboard | FASTabGroup | FASTabProfile];
```

##### <a name="AppSteroid.sdkVersion"> sdkVersion </a>
Return SDK version with `NSString`.

\+ (NSString *)sdkVersion

##### <a name="AppSteroid.sdkBuildVersion"> sdkBuildVersion </a>
Return SDK build version with `NSString`.

\+ (NSString *)sdkBuildVersion

### <a name="FASTabBarController"> FASTabBarController </a>
Class to access TabBarController provided by AppSteroid.

#### Class Method

|Method|Description|
|------|-----|
|[presentTabBarControllerWithTarget:animated:](#FASTabBarController.presentTabBarControllerWithTargetanimated) |[AppSteroid#setTabs:]Show tabs defined in (AppSteorid.setTabs). When nothing is defined, `Forum`, `Leaderboard`, `Message` and `Profile` will be displayed |

##### <a name="FASTabBarController.presentTabBarControllerWithTargetanimated"> presentTabBarControllerWithTarget: </a>
Show TabBarController for `Forum`,`Leaderboard` and `Profile`.

\+ (void)presentTabBarControllerWithTarget:(UIViewController *)target
                                  animated:(BOOL)animated;

* Parameters
  * target
    * Select a ViewController to show TabBarController.
  * animated
    * Yes will transit with animation. No will transit without animation.

Sample

```

#import <AppSteroid/FASTabBarController.h>

  …
  …

- (IBAction)pushedFASTabBarButton:(id)sender
{
    [FASTabBarController presentTabBarControllerWithTarget:self
                                                  animated:YES];
}
```

### <a name="FASPagingMeta"> FASPagingMeta </a>
Class storing meta information of array data.

#### Properties

|Properties|Description|
|------|-----|
|[currentPage](#FASPagingMeta.currentPage)|Current page |
|[nextPage](#FASPagingMeta.nextPage)|Next page |
|[perPage](#FASPagingMeta.perPage)|Number of contents per page |
|[totalCount](#FASPagingMeta.totalCount)|Total count of content. |
|[totalPages](#FASPagingMeta.totalPages)|Total pages |

##### <a name="FASPagingMeta.currentPage"> currentPage </a>
Current Page

@property (nonatomic, assign) NSUInteger currentPage

##### <a name="FASPagingMeta.nextPage"> nextPage </a>
Next Page

@property (nonatomic, assign) NSUInteger nextPage

##### <a name="FASPagingMeta.perPage"> perPage </a>
Number of contents per page

@property (nonatomic, assign) NSUInteger perPage

##### <a name="FASPagingMeta.totalCount"> totalCount </a>
Total count of content.

@property (nonatomic, assign) NSUInteger totalCount

##### <a name="FASPagingMeta.totalPages"> totalPages </a>
Total pages

@property (nonatomic, assign) NSUInteger totalPages
