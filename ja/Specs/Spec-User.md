# User Specifications

last update at 2014/10/8

---

## Introduction

ユーザーに関する機能の仕様書です。
ユーザーの作成、ログイン、プロフィールの変更等の機能が提供されています。
また、AppSteroidが提供するユーザーのプロフィールGUIを表示することも出来ます。
詳しくは[UserGetStarted](../GetStarted/GetStarted-User.md)を参照してください。

---

## Classes

|Class|Description|
|------|-----|
|[FASAccount](#FASAccount)|ログインユーザーのアカウント操作に関するクラス |
|[FASSNSAccount](#FASSNSAccount)|SNSアカウントの操作に関するクラス |
|[FASLoginUser](#FASLoginUser)|ログインユーザーモデルクラス |
|[FASUser](#FASUser)|ユーザーモデルクラス |

---

## APIs
### <a name="FASAccount"> FASAccount </a>
サインアップ、ログインを行うためのクラスです。
サインアップではユーザー名、プロフィール文、プロフィール画像を指定することが出来ます。
また、処理成功時には`FASLoginUser`が返却されます。

#### Class Methods

|Method|Description|
|------|-----|
|[signUpUserWithCompletion:](#FASAccount.signUpUserWithCompletion)|何も指定せずにサインアップをします。 |
|[signUpUserWithName:completion:](#FASAccount.signUpUserWithNamecompletion)|ユーザー名を指定してサインアップをします。 |
|[signUpUserWithName:description:profileImage:completion:](#FASAccount.signUpUserWithNamedescriptionprofileImagecompletion)|指定したユーザー名、プロフィール文、プロフィール画像でサインアップをします。 |
|[loginUserWithCompletion:](#FASAccount.loginUserWithCompletion) |ログイン処理を行います。 |
|[loginUserWithLifeTime:completion:](#FASAccount.loginUserWithLifeTimecompletion) |ログインの有効時間を指定してログイン処理を行います。 |
|[currentLoggedInUser](#FASAccount.currentLoggedInUser) |現在ログイン中のユーザーを返却します。 |

##### <a name="FASAccount.signUpUserWithCompletion">　signUpUserWithCompletion: </a>
何も指定せずにサインアップをします。  
ユーザー重複時の挙動に関しては[こちら](../8_ユーザー名重複時の挙動に関して.md)を参照してください。

\+ (void)signUpUserWithCompletion:(FASLoginUserHandler)completion

* Parameters
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

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
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASAccount.signUpUserWithNamecompletion"> signUpUserWithName:completion: </a>
ユーザー名を指定してサインアップをします。  
ユーザー重複時の挙動に関しては[こちら](../8_ユーザー名重複時の挙動に関して.md)を参照してください。

\+ (void)signUpUserWithName:(NSString *)userName
                  completion:(FASLoginUserHandler)completion

* Parameters
  * userName
    * ユーザー名。
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

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
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASAccount.signUpUserWithNamedescriptionprofileImagecompletion"> signUpUserWithName:description:profileImage:completion: </a>
指定したユーザー名、プロフィール文、プロフィール画像でサインアップをします。  
ユーザー重複時の挙動に関しては[こちら](../8_ユーザー名重複時の挙動に関して.md)を参照してください。

\+ (void)signUpUserWithName:(NSString *)userName
                description:(NSString *)description
               profileImage:(UIImage *)profileImage
                 completion:(FASLoginUserHandler)completion

* Parameters
  * userName
    * ユーザー名。
  * description
    * ユーザーのプロフィール文。255文字まで設定出来ます。
  * profileImage
    * ユーザーのプロフィール画像。
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

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
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASAccount.loginUserWithCompletion"> loginUserWithCompletion: </a>
ログイン処理を行います。
ログイン状態は1日保持されます。

\+ (void)loginUserWithCompletion:(FASLoginUserHandler)completion

* Parameters
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASAccount.h>

  …
  …

- (IBAction)pushedLoginButton:(id)sender
{
    [FASAccount loginUserWithCompletion:^(FASLoginUser *loginUser, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASAccount.loginUserWithLifeTimecompletion"> loginUserWithLifeTime:completion: </a>
ログイン処理を行います。
lifetimeで指定した時間だけログイン状態を保持します。

\+ (void)loginUserWithLifeTime:(NSUInteger)lifetime
                    completion:(FASLoginUserHandler)completion

* Parameters
  * lifetime
    * サインインの状態を保持する時間を秒で設定します。10秒以上86400秒以下で設定することが出来ます。デフォルトでは86400秒(1日)になっています。
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

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
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASAccount.currentLoggedInUser"> currentLoggedInUser </a>
現在ログイン中のユーザーを返却します。

\+ (FASLoginUser *)currentLoggedInUser;

### <a name="FASSNSAccount"> FASSNSAccount </a>
ログインユーザーのSNSアカウントの登録、削除、参照を行うためのクラスです。

#### Constants

|Constant|Description|
|------|-----|
|[FASSNSAccountCompletionHandler](#FASSNSAccount.FASSNSAccountCompletionHandler)| SNSアカウント追加時に利用されるブロックオブジェクト |
|[FASSNSAccountsCompletionHandler](#FASSNSAccount.FASSNSAccountsCompletionHandler)| SNSアカウント情報取得時に利用されるブロックオブジェクト |

#####　<a name="FASSNSAccount.FASSNSAccountCompletionHandler"> (^FASSNSAccountCompletionHandler)(FASSNSAccount *snsAccount, NSError *error) </a>
処理成功時に`FASSNSAccount`のオブジェクトが一つだけ返却されます。処理に失敗した時はエラーが返却されます。

typedef void (^FASSNSAccountCompletionHandler)(FASSNSAccount *snsAccount, NSError *error)

* Parameters
  * snsAccount
    * `FASSNSAccount`のオブジェクトです。SNSアカウント情報にはプロパティ経由で参照できます。
  * error
    * エラーの詳細が格納されています。エラーがない場合はnilになります。

#####　<a name="FASSNSAccount.FASSNSAccountsCompletionHandler"> (^FASSNSAccountsCompletionHandler)(NSArray *snsAccounts, FASPagingMeta *meta, NSError *error) </a>
処理成功時に`FASSNSAccount`のオブジェクトが格納されたNSArrayオブジェクトと、リストのめた情報である`FASPagingMeta`のオブジェクトが返却されます。処理に失敗した時はエラーが返却されます。

typedef void (^FASSNSAccountsCompletionHandler)(NSArray *snsAccounts, NSError *error)

* Parameters
  * snsAccounts
    * `FASSNSAccount`のオブジェクトが格納されたNSArrayです。各SNSアカウント情報にはプロパティ経由で参照できます。
  * meta
    * リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
  * error
    * エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[snsAccountId](#FASSNSAccount.snsAccountId)|SNSアカウントを管理するためのID |
|[provider](#FASSNSAccount.provider)|設定されたプロバイダー名 |
|[uid](#FASSNSAccount.uid)|設定されたUID |
|[createdAt](#FASSNSAccount.createdAt)|SNSアカウントが作成された時刻 |
|[updatedAt](#FASSNSAccount.updatedAt)|SNSアカウントが更新された時刻 |

##### <a name="FASSNSAccount.snsAccountId"> snsAccountId </a>
SNSアカウントを管理するためのIDが格納されます。

@property (nonatomic, readonly) NSString *snsAccountId

##### <a name="FASSNSAccount.provider"> provider </a>
設定されたプロバイダー名が格納されます。

@property (nonatomic, readonly) NSString *provider

##### <a name="FASSNSAccount.uid"> uid </a>
設定されたUIDが格納されます。

@property (nonatomic, readonly) NSString *uid

##### <a name="FASSNSAccount.createdAt"> createdAt </a>
SNSアカウントが作成された時刻が格納されます。

@property (nonatomic, readonly) NSDate *createdAt

##### <a name="FASSNSAccount.updatedAt"> updatedAt </a>
SNSアカウントが更新された時刻が格納されます。

@property (nonatomic, readonly) NSDate *updatedAt

#### Class Methods

|Method|Description|
|------|-----|
|[addUserSNSAccount:userId:secretToken:completion:](#FASSNSAccount.addUserSNSAccountuserIdsecretTokencompletion) |指定したプロバイダ名とUIDをログインユーザーと紐づけます。 |
|[deleteUserSNSAccount:](#FASSNSAccount.deleteUserSNSAccount) |ログインユーザーのSNSアカウントを削除します。 |
|[fetchUserSNSAccounts:](#FASSNSAccount.fetchUserSNSAccounts) |ログインユーザーのSNSアカウントを取得します。 |

##### <a name="FASSNSAccount.addUserSNSAccountuserIdsecretTokencompletion"> addUserSNSAccount:userId:secretToken:completion: </a>
指定したプロバイダ名とUIDをログインユーザーと紐づけます。

\+ (void)addUserSNSAccount:(NSString *)provider
                    userId:(NSString *)uid
               secretToken:(NSString *)secretToken
                completion:(FASSNSAccountCompletionHandler)completion

* Parameters
  * provider
    * SNSプロバイダ名。
  * uid
    * SNSプロバイダから提供されているユーザーID。
  * secretToken
    * Fresviiが提供するシークレットトークン。
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

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
    // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASSNSAccount.deleteUserSNSAccount"> deleteUserSNSAccount: </a>
ログインユーザーのSNSアカウントを削除します。

\+ (void)deleteUserSNSAccount:(FASCompletionHandler)completion

* Parameters
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASSNSAccount.h>

  …
  …

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASSNSAccount deleteUserSNSAccount:^(NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASSNSAccount.fetchUserSNSAccounts"> fetchUserSNSAccounts: </a>
ログインユーザーのSNSアカウントを取得します。

\+ (void)fetchUserSNSAccounts:(FASSNSAccountsCompletionHandler)completion

* Parameters
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

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
        // 処理が完了したら呼ばれます。
    }];
}
```

### <a name="FASLoginUser"> FASLoginUser </a>
ログインユーザーの情報が格納されている`FASUser`の子クラスです。
このクラスからログインユーザーの情報を更新することも出来ます。
ログインユーザーは常に一人なので唯一のオブジェクトになっています。

#### Constants

|Constant|Description|
|------|-----|
|[FASLoginUserHandler](#FASLoginUser.FASLoginUserCompletionHandler)|サインアップ処理やログイン処理を行った際に利用されるブロックオブジェクト。 |

#####　<a name="FASLoginUser.FASLoginUserCompletionHandler"> (^FASLoginUserCompletionHandler)(FASLoginUser *loginUser, NSError *error) </a>
`FASAccount`でサインアップ処理やログイン処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASLoginUserCompletionHandler)(FASLoginUser *loginUser, NSError *error)

* Parameters
  * loginUser
    * ログインユーザーの情報が格納されています。
  * error
    * エラーの詳細が格納されている。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[userName](#FASLoginUser.userName)|ユーザー名の取得、変更を行います。  |
|[userDescription](#FASLoginUser.userDescription)|プロフィール文の取得、変更を行います。 |
|[profileImage](#FASLoginUser.profileImage)|プロフィール画像の取得、変更を行います。 |
|[expireDate](#FASLoginUser.expireDate)|ログインユーザーのログイン状態が有効な時間が格納されています。 |
|[isSignedUp](#FASLoginUser.isSignedUp)|サインアップ済みかどうかを確認します。 |
|[isExpiredSession](#FASLoginUser.isExpiredSession)|ログイン状態が有効かどうかをかを確認します。 |

##### <a name="FASLoginUser.userName"> userName </a>
ユーザー名の取得、変更を行います。
変更は`saveWithCompletion:`を利用するとサーバーに反映されます。
変更の取り消しは`reset`を利用してください。

@property (nonatomic, readwrite) NSString *userName

##### <a name="FASLoginUser.userDescription"> userDescription </a>
プロフィール文の取得、変更を行います。
変更は`saveWithCompletion:`を利用するとサーバーに反映されます。
変更の取り消しは`reset`を利用してください。

@property (nonatomic, readwrite) NSString *userDescription

##### <a name="FASLoginUser.profileImage"> profileImage </a>
プロフィール画像の取得、変更を行います。
変更は`saveWithCompletion:`を利用するとサーバーに反映されます。
変更の取り消しは`reset`を利用してください。

@property (nonatomic, readwrite) UIImage *profileImage

##### <a name="FASLoginUser.expireDate"> expireDate </a>
ログインユーザーのログイン状態が有効な時間が格納されています。

@property (nonatomic, readonly) NSDate *expireDate

##### <a name="FASLoginUser.isSignedUp"> isSignedUp </a>
サインアップ済みかどうかを確認します。

@property (nonatomic, readonly) BOOL isSignedUp

#####  <a name="FASLoginUser.isExpiredSession"> isExpiredSession </a>
ログイン状態が有効かどうかをかを確認します。

@property (nonatomic, readonly) BOOL isExpiredSession

#### Instance Methods

|Method|Description|
|------|-----|
|[saveWithCompletion:](#FASLoginUser.saveWithCompletion) |プロフィールの変更をサーバーに保存します。 |
|[reset](#FASLoginUser.reset) |プロフィールを変更前に戻します。 |

##### <a name="FASLoginUser.saveWithCompletion"> saveWithCompletion: </a>
プロフィールの変更をサーバーに保存します。  
ユーザー重複時の挙動に関しては[こちら](../8_ユーザー名重複時の挙動に関して.md)を参照してください。

\- (void)saveWithCompletion:(FASCompletionHandler)completion

* Parameters
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

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
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASLoginUser.reset"> reset </a>
プロフィールを変更前に戻します。

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
ユーザーの情報が格納されています。
ユーザーID,ユーザーコードからユーザーを呼び出すことも出来ます。
ユーザー情報は参照のみできます。

#### Constants

|Constant|Description|
|------|-----|
|[FASUserCompletionHandler](#FASUser.FASUserCompletionHandler)|ユーザー作成、ユーザー情報の取得処理を行った際に利用されるブロックオブジェクト。 |
|[FASUsersCompletionHandler](#FASUser.FASUsersCompletionHandler)|複数のユーザー情報の取得処理を行った際に利用されるブロックオブジェクト。 |


##### <a name="FASUser.FASUserCompletionHandler"> (^FASUserCompletionHandler)(FASUser *user, NSError *error) </a>
ユーザー作成、ユーザー情報の取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASUserCompletionHandler)(FASUser *user, NSError *error)

* Parameters
  * user
    * ユーザーの情報が格納されています。
  * error
    * エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASUser.FASUsersCompletionHandler"> (^FASUsersCompletionHandler)(NSArray *users, FASPagingMeta *meta, NSError *error) </a>
複数のユーザー情報の取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASUsersCompletionHandler)(NSArray *users, FASPagingMeta *meta, NSError *error)

* Parameters
  * users
    * 複数のユーザーの情報がNSArrayに格納されています。
  * meta
    * リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
  * error
    * エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[userId](#FASUser.userId)|ユーザーID |
|[userName](#FASUser.userName)|ユーザー名 |
|[userCode](#FASUser.userCode)|ユーザーコード |
|[userDescription](#FASUser.userDescription)|ユーザーのプロフィール文 |
|[profileImageURL](#FASUser.profileImageURL)|ユーザーのプロフィール画像URL |
|[profileImage](#FASUser.profileImage)|ユーザーのプロフィール画像 |
|[friendStatus](#FASUser.friendStatus)|ユーザーのフレンドステータス |
|[createdAt](#FASUser.createdAt)|ユーザーが作成された時刻 |
|[updatedAt](#FASUser.updatedAt)|ユーザー情報が更新された時刻 |
|[official](#FASUser.official)|オフィシャルユーザーかどうか |

##### <a name="FASUser.userId"> userId </a>
ユーザーID

@property (nonatomic, readonly) NSString *userId;

##### <a name="FASUser.userName"> userName </a>
ユーザー名

@property (nonatomic, readonly) NSString *userName;

##### <a name="FASUser.userCode"> userCode </a>
ユーザーコード

@property (nonatomic, readonly) NSString *userCode;

##### <a name="FASUser.userDescription"> userDescription </a>
ユーザーのプロフィール文

@property (nonatomic, readonly) NSString *userDescription;

##### <a name="FASUser.profileImageURL"> profileImageURL </a>
ユーザーのプロフィール画像URL

@property (nonatomic, readonly) NSString *profileImageURL;

##### <a name="FASUser.profileImage"> profileImage </a>
ユーザーのプロフィール画像

@property (nonatomic, readonly) UIImage *profileImage;

##### <a name="FASUser.friendStatus"> friendStatus </a>
ユーザーのフレンドステータス

@property (nonatomic, readonly) NSString *friendStatus;

##### <a name="FASUser.createdAt"> createdAt </a>
ユーザーが作成された時刻

@property (nonatomic, readonly) NSDate *createdAt;

##### <a name="FASUser.updatedAt"> updatedAt </a>
ユーザー情報が更新された時刻

@property (nonatomic, readonly) NSDate *updatedAt;

##### <a name="FASUser.official"> official </a>
オフィシャルユーザーかどうか

@property (nonatomic, readonly, getter = isOfficial) BOOL official;

#### Class Methods

|Method|Description|
|------|-----|
|[fetchUserWithUserId:completion:](#FASUser.fetchUserWithUserIdcompletion) |ユーザーIDにマッチするユーザーを取得します。 |
|[fetchUserWithUserCode:completion:](#FASUser.fetchUserWithUserCodecompletion) |ユーザーコードにマッチするユーザーを取得します。 |
|[fetchUsersWithProvider:uid:completion:](#FASUser.fetchUsersWithProvideruidcompletion) |プロバイダ名とUIDにマッチするユーザーのリストを取得します。 |

##### <a name="FASUser.fetchUserWithUserIdcompletion"> fetchUserWithUserId:completion: </a>
ユーザーIDにマッチするユーザーを取得します。

\+ (void)fetchUserWithUserId:(NSString *)userId
                  completion:(FASUserCompletionHandler)completion;

* Parameters
  * userId
    * 情報を取得したいユーザーのID。
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

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
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASUser.fetchUserWithUserCodecompletion"> fetchUserWithUserCode:completion: </a>
ユーザーコードにマッチするユーザーを取得します。

\+ (void)fetchUserWithUserCode:(NSString *)userCode
                    completion:(FASUserCompletionHandler)completion

* Parameters
  * userCode
    * 情報を取得したいユーザーのユーザーコード。
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

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
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASUser.fetchUsersWithProvideruidcompletion"> fetchUsersWithProvider:uid:completion: </a>
プロバイダ名とUIDにマッチするユーザーのリストを取得します。

\+ (void)fetchUsersWithProvider:(NSString *)provider
                            uid:(NSString *)uid
                     completion:(FASUsersCompletionHandler)completion

* Parameters
  * provider
    * SNSプロバイダ名。
  * uid
    * SNSプロバイダから提供されているユーザーID。
  * completion
    * 処理が完了した時に実行されるブロックオブジェクト。

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
        // 処理が完了したら呼ばれます。
    }];
}
```
