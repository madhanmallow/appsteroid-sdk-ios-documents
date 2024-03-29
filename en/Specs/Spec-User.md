# User Specifications

last update at 2014/10/24

---

## Introduction

Specification for functions related to User.
Functions such as creating user, logging in, editing profile are provided. You can also use a profile GUI provided by AppSteroid. Check [UserGetStarted](../GetStarted/GetStarted-User.md) for detail usage.


---


## Classes

|Class|Description|
|------|-----|
|[FASAccount](#FASAccount)|Class related to Login User Account Operation |
|[FASSNSAccount](#FASSNSAccount)|Class related to SNS Account Operation |
|[FASLoginUser](#FASLoginUser)|Login User Model Class |
|[FASUser](#FASUser)|User Model Class |
|[FASProfileNavigationController](#FASProfileNavigationController)|NavigationController for Profile View |
|[FASProfileLayout](#FASProfileLayout) |Class to change layout of profile View |

---

## APIs
### <a name="FASAccount"> FASAccount </a>
This is a class for signing up and logging in.
A user name, profile text, and a profile image can be specified at signup. Also, `FASLoginUser` will be returned when the process succeeds.


#### Class Methods

|Method|Description|
|------|-----|
|[signUpUserWithCompletion:](#FASAccount.signUpUserWithCompletion)|Signup without any setup. |
|[signUpUserWithName:completion:](#FASAccount.signUpUserWithNamecompletion)|Signup with user name. |
|[signUpUserWithName:description:profileImage:completion:](#FASAccount.signUpUserWithNamedescriptionprofileImagecompletion)|Signup with user name, profile text, and profile image. |
|[loginUserWithCompletion:](#FASAccount.loginUserWithCompletion) |Preform Login. |
|[loginUserWithLifeTime:completion:](#FASAccount.loginUserWithLifeTimecompletion) |Select a login expiration time and preform login. |
|[currentLoggedInUser](#FASAccount.currentLoggedInUser) |Return users currently logged in. |

##### <a name="FASAccount.signUpUserWithCompletion">　signUpUserWithCompletion: </a>
Signup without any setup.
For behavior on user name duplication, please see [this](../8_DuplicatedUserName.md) document.

\+ (void)signUpUserWithCompletion:(FASLoginUserHandler)completion

* Parameters
  * completion
    * Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASAccount.h>

  …
  …

- (IBAction)pushedSignUpButton:(id)sender
{
    NSString *userName = @"UserName";
    [FASAccount signUpUserWithCcompletion:^(FASLoginUser *loginUser, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASAccount.signUpUserWithNamecompletion"> signUpUserWithName:completion: </a>
Signup with user name.
For behavior on user name duplication, please see [this](../8_DuplicatedUserName.md) document.

\+ (void)signUpUserWithName:(NSString *)userName
                  completion:(FASLoginUserHandler)completion

* Parameters
  * userName
    * User name
  * completion
    * Block object to be executed when the process is completed.

###### Sample
```
#import <AppSteroid/FASAccount.h>

  …
  …

- (IBAction)pushedSignUpButton:(id)sender
{
    NSString *userName = @"UserName";
    [FASAccount signUpUserWithName:userName
                        completion:^(FASLoginUser *loginUser, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASAccount.signUpUserWithNamedescriptionprofileImagecompletion"> signUpUserWithName:description:profileImage:completion: </a>
Signup with user name, profile text, and profile image.
For behavior on user name duplication, please see [this](../8_DuplicatedUserName.md) document.

\+ (void)signUpUserWithName:(NSString *)userName
                description:(NSString *)description
               profileImage:(UIImage *)profileImage
                 completion:(FASLoginUserHandler)completion

* Parameters
  * userName
    * User name
  * description
    * User profile text, with up to 255 letters.
  * profileImage
    * User profile image.
  * completion
    * Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASAccount.h>

  …
  …

- (IBAction)pushedSignUpButton:(id)sender
{
    NSString *userName = @"UserName";
    NSString *userDescription = @"UserDescription";
    UIImage *profileImage = [UIImage imageNamed:@"profile_image"];
    [FASAccount signUpUserWithName:userName
                       description:userDescription
                      profileImage:profileImage
                        completion:^(FASLoginUser *loginUser, NSError *error)
    {
        // it will be called when the process is completed.
    }];
}
```

##### <a name="FASAccount.loginUserWithCompletion"> loginUserWithCompletion: </a>
Preform Login.  Login status will be preserved for 1 day.

\+ (void)loginUserWithCompletion:(FASLoginUserHandler)completion

* Parameters
  * completion
    * Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASAccount.h>

  …
  …

- (IBAction)pushedLoginButton:(id)sender
{
    [FASAccount loginUserWithCompletion:^(FASLoginUser *loginUser, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASAccount.loginUserWithLifeTimecompletion"> loginUserWithLifeTime:completion: </a>
Select a login expiration time with lifetime, and preform login.

\+ (void)loginUserWithLifeTime:(NSUInteger)lifetime
                    completion:(FASLoginUserHandler)completion

* Parameters
  * lifetime
    * Sets the time of preserving login status in seconds. Can be set between 10 sec up to 86400 sec. It is set to 86400 sec as a default value.
  * completion
    * Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASAccount.h>

  …
  …

- (IBAction)pushedLoginButton:(id)sender
{
    NSUInteger lifetime = 86400;
    [FASAccount loginUserWithLifeTime:lifetime
                           completion:^(FASLoginUser *loginUser, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASAccount.currentLoggedInUser"> currentLoggedInUser </a>
Return users currently logged in.


\+ (FASLoginUser *)currentLoggedInUser;

### <a name="FASSNSAccount"> FASSNSAccount </a>
Class for registering, deleting, and referencing login user's SNS account.

#### Constants

|Constant|Description|
|------|-----|
|[FASSNSAccountCompletionHandler](#FASSNSAccount.FASSNSAccountCompletionHandler)|Block object used when adding SNS accounts. |
|[FASSNSAccountsCompletionHandler](#FASSNSAccount.FASSNSAccountsCompletionHandler)|Block object is used when getting SNS account information. |

#####　<a name="FASSNSAccount.FASSNSAccountCompletionHandler"> (^FASSNSAccountCompletionHandler)(FASSNSAccount *snsAccount, NSError *error) </a>
One object of `FASSNSAccount` will be returned when the process goes successfully. It returns an error when the process fails.

typedef void (^FASSNSAccountCompletionHandler)(FASSNSAccount *snsAccount, NSError *error)

* Parameters
  * snsAccount
    * Object of `FASSNSAccount`. Check the SNS account info through property.
  * error
    * Error detail is stored. It will be nil when there is no error.

#####　<a name="FASSNSAccount.FASSNSAccountsCompletionHandler"> (^FASSNSAccountsCompletionHandler)(NSArray *snsAccounts, FASPagingMeta *meta, NSError *error) </a>
An NSArray object that stores object of `FASSNSAccount` and another object of `FASPagingMeta` that stores meta information will be returned when the process goes successfully.  It returns an error when the process fails.

typedef void (^FASSNSAccountsCompletionHandler)(NSArray *snsAccounts, NSError *error)

* Parameters
  * snsAccounts
    * NSArray that stores object of `FASSNSAccount`. You can check the SNS account info through property.
  * meta
    * You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../7_Spec.md#FASPagingMeta) for more information.
  * error
    * Error detail is stored. It will be nil when there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[snsAccountId](#FASSNSAccount.snsAccountId)|ID to manage SNS account |
|[provider](#FASSNSAccount.provider)|Provider name set for the account |
|[uid](#FASSNSAccount.uid)|UID set for the account |
|[createdAt](#FASSNSAccount.createdAt)|Time when the SNS account was created |
|[updatedAt](#FASSNSAccount.updatedAt)|Time when the SNS account was updated |

##### <a name="FASSNSAccount.snsAccountId"> snsAccountId </a>
ID to manage SNS account is stored.

@property (nonatomic, readonly) NSString *snsAccountId

##### <a name="FASSNSAccount.provider"> provider </a>
Provider name set for the account is stored.

@property (nonatomic, readonly) NSString *provider

##### <a name="FASSNSAccount.uid"> uid </a>
UID set for the account is stored.

@property (nonatomic, readonly) NSString *uid

##### <a name="FASSNSAccount.createdAt"> createdAt </a>
Time when the SNS account was created is stored.

@property (nonatomic, readonly) NSDate *createdAt

##### <a name="FASSNSAccount.updatedAt"> updatedAt </a>
Time when the SNS account was updated is stored.

@property (nonatomic, readonly) NSDate *updatedAt

#### Class Methods

|Method|Description|
|------|-----|
|[addUserSNSAccount:userId:secretToken:completion:](#FASSNSAccount.addUserSNSAccountuserIdsecretTokencompletion) |Associates a specified provider name and UID with a login user. |
|[deleteUserSNSAccount:](#FASSNSAccount.deleteUserSNSAccount) |Deletes a login user's SNS account. |
|[fetchUserSNSAccounts:](#FASSNSAccount.fetchUserSNSAccounts) |Acquires a login user's SNS account. |

##### <a name="FASSNSAccount.addUserSNSAccountuserIdsecretTokencompletion"> addUserSNSAccount:userId:secretToken:completion: </a>
Associates a specified provider name and UID with a login user.

\+ (void)addUserSNSAccount:(NSString *)provider
                    userId:(NSString *)uid
               secretToken:(NSString *)secretToken
                completion:(FASSNSAccountCompletionHandler)completion

* Parameters
  * provider
    * SNS provider name
  * uid
    * User ID provided from SNS provider
  * secretToken
    * SecretToken provided by AppSteroid
  * completion
    * Block object to be executed when the process is completed.

Response例

```
{
  "id":"c03e7b15e8ec4cdd99350e153a945fbb",
  "provider":"provider",
  "uid":"uid",
  "created_at":"2014-04-06T10:58:56.751Z",
  "updated_at":"2014-04-06T10:58:56.751Z"
}
```

Sample

```
#import <AppSteroid/FASSNSAccount.h>

  …
  …

- (IBAction)pushedAddButton:(id)sender
{
    NSString *provider = @"ProviderName";
    NSString *userID = @"UserId";
    NSStrign *secretToken = @"xxxxxxxxxxxxxxxxxxxxxxxx";
    [FASSNSAccount addUserSNSAccount:provider
                              userId:userID
                         secretToken:secretToken
                          completion:^(FASSNSAccount *snsAccount, NSError *error)
    {
    // It will be called when the process is completed.
    }];
}
```

##### <a name="FASSNSAccount.deleteUserSNSAccount"> deleteUserSNSAccount: </a>
Deletes a login user's SNS account.

\+ (void)deleteUserSNSAccount:(FASCompletionHandler)completion

* Parameters
  * completion
    * Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASSNSAccount.h>

  …
  …

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASSNSAccount deleteUserSNSAccount:^(NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASSNSAccount.fetchUserSNSAccounts"> fetchUserSNSAccounts: </a>
Get a login user's SNS account.

\+ (void)fetchUserSNSAccounts:(FASSNSAccountsCompletionHandler)completion

* Parameters
  * completion
    * Block object to be executed when the process is completed.

Response例

```
[
  {
    "id":"c03e7b15e8ec4cdd99350e153a945fbb",
    "provider":"provider",
    "uid":"uid",
    "created_at":"2014-04-06T10:58:56.000Z",
    "updated_at":"2014-04-06T10:58:56.000Z"
  }
]
```

Sample

```
#import <AppSteroid/FASSNSAccount.h>

  …
  …

- (IBAction)pushedFetchButton:(id)sender
{
    [FASSNSAccount fetchUserSNSAccounts:^(NSArray *snsAccounts, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

### <a name="FASLoginUser"> FASLoginUser </a>
This is a subclass of `FASUser` where login user information is stored. Login user information can be updated from this class. Login users are always individuals, so they are solitary objects.

#### Constants

|Constant|Description|
|------|-----|
|[FASLoginUserHandler](#FASLoginUser.FASLoginUserCompletionHandler)|Block object used when carrying out the process to signup or login. |

#####　<a name="FASLoginUser.FASLoginUserCompletionHandler"> (^FASLoginUserCompletionHandler)(FASLoginUser *loginUser, NSError *error) </a>
Block object used when carrying out the process to signup or login using `FASAccount`.

typedef void (^FASLoginUserCompletionHandler)(FASLoginUser *loginUser, NSError *error)

* Parameters
  * loginUser
    * The login user information is stored here.
  * error
    * Error details are stored here. When there is no error, it will be nil.

#### Properties

|Properties|Description|
|------|-----|
|[userName](#FASLoginUser.userName)|Get and changes user names. |
|[userDescription](#FASLoginUser.userDescription)|Get and changes profile text. |
|[profileImage](#FASLoginUser.profileImage)|Get and changes profile images. |
|[expireDate](#FASLoginUser.expireDate)|Login users' login expiration date are stored. |
|[isSignedUp](#FASLoginUser.isSignedUp)|Checks whether a user has already signed up or not. |
|[isExpiredSession](#FASLoginUser.isExpiredSession)|Checks whether a user's login status has expired or not. |

##### <a name="FASLoginUser.userName"> userName </a>
Get and changes user names.
Using `saveWithCompletion:` will reflect changes on the server. Use `reset` to cancel changes.

@property (nonatomic, readwrite) NSString *userName

##### <a name="FASLoginUser.userDescription"> userDescription </a>
Get and changes profile text.
Using `saveWithCompletion:` will reflect changes on the server. Use `reset` to cancel changes.

@property (nonatomic, readwrite) NSString *userDescription

##### <a name="FASLoginUser.profileImage"> profileImage </a>
Get and changes profile images.
Using `saveWithCompletion:` will reflect changes on the server. Use `reset` to cancel changes.

@property (nonatomic, readwrite) UIImage *profileImage

##### <a name="FASLoginUser.expireDate"> expireDate </a>
Login users' login expiration date are stored.

@property (nonatomic, readonly) NSDate *expireDate

##### <a name="FASLoginUser.isSignedUp"> isSignedUp </a>
Checks whether a user has already signed up or not.

@property (nonatomic, readonly) BOOL isSignedUp

#####  <a name="FASLoginUser.isExpiredSession"> isExpiredSession </a>
Checks whether a user's login status has expired or not.

@property (nonatomic, readonly) BOOL isExpiredSession

#### Instance Methods

|Method|Description|
|------|-----|
|[saveWithCompletion:](#FASLoginUser.saveWithCompletion) |Saves profile changes to the server. |
|[reset](#FASLoginUser.reset) |Reset profile to the condition before change was made. |

##### <a name="FASLoginUser.saveWithCompletion"> saveWithCompletion: </a>
Saves profile changes to the server.
For behavior on user name duplication, please see [this](../8_DuplicatedUserName.md) document.

\- (void)saveWithCompletion:(FASCompletionHandler)completion

* Parameters
  * completion
    * Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASLoginUser.h>

  …
  …

- (IBAction)pushedSubmitButton:(id)sender
{
    FASLoginUser *loginUser = [FASAccount currentLoggedInUser];
    [loginUser saveWithCompletion:^(NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASLoginUser.reset"> reset </a>
Reset profile to the condition before change was made.

\- (void)reset;

Sample

```
#import <AppSteroid/FASLoginUser.h>

  …
  …

- (IBAction)pushedCancelButton:(id)sender
{
    FASLoginUser *loginUser = [FASAccount currentLoggedInUser];
    [loginUser reset];
}
```

### <a name="FASUser"> FASUser </a>
User information is stored.  User can be called using a user ID or user code.  User information can only be referenced.

#### Constants

|Constant|Description|
|------|-----|
|[FASUserCompletionHandler](#FASUser.FASUserCompletionHandler)|Block object used when carrying out the process to get user information, user creation. |
|[FASUsersCompletionHandler](#FASUser.FASUsersCompletionHandler)|Block object used when carrying out the process to get multiple user information. |


##### <a name="FASUser.FASUserCompletionHandler"> (^FASUserCompletionHandler)(FASUser *user, NSError *error) </a>
Block object used when carrying out the process to get user information, user creation.

typedef void (^FASUserCompletionHandler)(FASUser *user, NSError *error)

* Parameters
  * user
    * User information is stored here.
  * error
    * Error details are stored here. When there is no error, it will be nil.

##### <a name="FASUser.FASUsersCompletionHandler"> (^FASUsersCompletionHandler)(NSArray *users, FASPagingMeta *meta, NSError *error) </a>
Block object used when carrying out the process to get multiple user information.

typedef void (^FASUsersCompletionHandler)(NSArray *users, FASPagingMeta *meta, NSError *error)

* Parameters
  * users
    * Multiple user information is stored in NSArray.
  * meta
    * You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../7_Spec.md#FASPagingMeta) for more information.
  * error
    * Error details are stored here. When there is no error, it will be nil.

#### Properties

|Properties|Description|
|------|-----|
|[userId](#FASUser.userId)|User ID |
|[userName](#FASUser.userName)|User name |
|[userCode](#FASUser.userCode)|User code |
|[userDescription](#FASUser.userDescription)|User profile text |
|[profileImageURL](#FASUser.profileImageURL)|User profile image URL |
|[profileImage](#FASUser.profileImage)|User profile image |
|[friendStatus](#FASUser.friendStatus)|User friend status |
|[launchCount](#FASUserBridge.launchCount)|Launch Count |
|[launchTime](#FASUserBridge.launchTime)|Total activated time |
|[friendRequestsCount](#FASUserBridge.friendRequestsCount)|Friend request count |
|[friendsCount](#FASUserBridge.friendsCount)|Friend count |
|[videosCount](#FASUserBridge.videosCount)|Video count |
|[createdAt](#FASUser.createdAt)|Date and time of when a user was created. |
|[updatedAt](#FASUser.updatedAt)|Date and time of when a user information was update. |
|[official](#FASUser.official)|Whether it is an official user or not. |

##### <a name="FASUser.userId"> userId </a>
User ID

@property (nonatomic, readonly) NSString *userId;

##### <a name="FASUser.userName"> userName </a>
User name

@property (nonatomic, readonly) NSString *userName;

##### <a name="FASUser.userCode"> userCode </a>
User code

@property (nonatomic, readonly) NSString *userCode;

##### <a name="FASUser.userDescription"> userDescription </a>
User profile text

@property (nonatomic, readonly) NSString *userDescription;

##### <a name="FASUser.profileImageURL"> profileImageURL </a>
User profile image URL

@property (nonatomic, readonly) NSString *profileImageURL;

##### <a name="FASUser.profileImage"> profileImage </a>
User profile image

@property (nonatomic, readonly) UIImage *profileImage;

##### <a name="FASUser.friendStatus"> friendStatus </a>
User friend status

@property (nonatomic, readonly) NSString *friendStatus;

##### <a name="FASUser.launchCount"> launchCount </a>
Launch Count

@property (nonatomic, readonly) NSUInteger launchCount;

##### <a name="FASUser.launchTime"> launchTime </a>
Total activated time

@property (nonatomic, readonly) NSUInteger launchTime;

##### <a name="FASUser.friendRequestsCount"> friendRequestsCount </a>
Friend request count

@property (nonatomic, readonly) NSUInteger friendRequestsCount;

##### <a name="FASUser.friendsCount"> friendsCount </a>
Friend count

@property (nonatomic, readonly) NSUInteger friendsCount;

##### <a name="FASUser.videosCount"> videosCount </a>
Video count

@property (nonatomic, readonly) NSUInteger videosCount;

##### <a name="FASUser.createdAt"> createdAt </a>
Date and time of when a user was created.

@property (nonatomic, readonly) NSDate *createdAt;

##### <a name="FASUser.updatedAt"> updatedAt </a>
Date and time of when a user information was updated.

@property (nonatomic, readonly) NSDate *updatedAt;

##### <a name="FASUser.official"> official </a>
Whether it is an official user or not.

@property (nonatomic, readonly, getter = isOfficial) BOOL official;

#### Class Methods

|Method|Description|
|------|-----|
|[fetchUserWithUserId:completion:](#FASUser.fetchUserWithUserIdcompletion) |Get user that match the user ID. |
|[fetchUserWithUserCode:completion:](#FASUser.fetchUserWithUserCodecompletion) |Get user that match the user code. |
|[fetchUsersWithProvider:uid:completion:](#FASUser.fetchUsersWithProvideruidcompletion) |Get list of users that match the provider name and UID name. |
|[fetchCSRUserWithCompletion:](#FASUser.fetchCSRUserWithCompletion) |Get CSR User. |

##### <a name="FASUser.fetchUserWithUserIdcompletion"> fetchUserWithUserId:completion: </a>
Get user that match the user ID.

\+ (void)fetchUserWithUserId:(NSString *)userId
                  completion:(FASUserCompletionHandler)completion;

* Parameters
  * userId
    * ID of the user who you would like to get information from.
  * completion
    * Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASUser.h>

  …
  …

- (IBAction)pushedFetchButton:(id)sender
{
    NSString *userId = @"UserId";
  [FASUser fetchUserWithUserId:userId
                      completion:^(FASUser *user, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASUser.fetchUserWithUserCodecompletion"> fetchUserWithUserCode:completion: </a>
Get user that match the user code.

\+ (void)fetchUserWithUserCode:(NSString *)userCode
                    completion:(FASUserCompletionHandler)completion

* Parameters
  * userCode
    * User Code of the user who you would like to get information from.
  * completion
    * Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASUser.h>

  …
  …

- (IBAction)pushedFetchButton:(id)sender
{
  NSString *userCode = @"UserCode";
  [FASUser fetchUserWithUserCode:userCode
                        completion:^(FASUser *user, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASUser.fetchUsersWithProvideruidcompletion"> fetchUsersWithProvider:uid:completion: </a>
Get list of users that match the provider name and UID name.

\+ (void)fetchUsersWithProvider:(NSString *)provider
                            uid:(NSString *)uid
                     completion:(FASUsersCompletionHandler)completion

* Parameters
  * provider
    * SNS provider name.
  * uid
    * User ID provided from SNS provider
  * completion
    * Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASUser.h>

  …
  …

- (IBAction)pushedFetchButton:(id)sender
{
    NSString *provider = @"ProviderName";
    NSString *userId = @"UserId";
    [FASUser fetchUsersWithProvider:provider
                                uid:userId
                         completion:^(NSArray *users, PagingMeta *meta, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASUser.fetchCSRUserWithCompletion"> fetchCSRUserWithCompletion: </a>
Get user list　matching with the provider name and UID

\+ (void)fetchCSRUserWithCompletion:(FASUserCompletionHandler)completion;

* Parameters
  * completion
    * Block object to be executed when the process is completed.