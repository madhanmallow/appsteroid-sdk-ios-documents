# Leaderboard Specifications

last update at 2014/010/7

---

## Introduction

リーダーボードの機能に関する仕様書です。
特定のリーダーボードにスコアを登録したり、ユーザーのランキングを取得したりする機能が提供されています。
リーダーボードの作成はFresviiのウェブコンソールから行ってください。
また、AppSteroidが提供するリーダーボードのGUIも表示することが出来ます。表示方法は[LeaderboardGetStarted](../GetStarted/GetStarted-Leaderboard.md)を参照してください。

---

## Classes

|Class|Description|
|------|-----|
|[FASLeaderboard](#FASLeaderboard)|リーダーボードモデルクラス |
|[FASScore](#FASScore)|スコアモデルクラス |
|[FASRank](#FASRank)|ランクモデルクラス |
|[FASLeaderboardNavigationController](#FASLeaderboardNavigationController)|リーダーボードビューのベースとなるNavigationController |
|[FASLeaderboardLayout](#FASLeaderboardLayout)|リーダーボードビュー関連のレイアウトを変更するためのクラス |



---

## APIs
### <a name="FASLeaderboard"> FASLeaderboard </a>
リーダーボードモデルクラス。リーダーボード機能にアクセスするためのクラスメソッドも提供しています。

#### Constants

|Constant|Description|
|------|-----|
|[FASLeaderboardUsedScoreType](#FASLeaderboard.FASLeaderboardUsedScoreType)|リーダーボードで利用されているスコアのタイプ。ベストスコアと最新スコアが定義されています。 |
|[FASLeaderboardCompletionHandler](#FASLeaderboard.FASLeaderboardCompletionHandler)|リーダーボード一件取得処理を行った際に利用されるブロックオブジェクト。 |
|[FASLeaderboardsCompletionHandler](#FASLeaderboard.FASLeaderboardsCompletionHandler)|リーダーボード一覧取得処理を行った際に利用されるブロックオブジェクト。 |

##### <a name="FASLeaderboard.FASLeaderboardSubmissionType"> FASLeaderboardSubmissionType </a>
リーダーボードで利用されているスコアのタイプ。ベストスコアと最新スコアが定義されています。

```
typedef NS_ENUM(NSInteger, FASLeaderboardUsedScoreType)
{
    FASLeaderboardUsedScoreTypeInvalid = -1,
    FASLeaderboardUsedScoreTypeBestScore,
    FASLeaderboardUsedScoreTypeRecentScore
};
```

###### Constants
###### FASLeaderboardUsedScoreTypeInvalid
不正なステータスが返却された際に利用されます。

###### FASLeaderboardUsedScoreTypeBestScore
ベストスコアのタイプです。

###### FASLeaderboardUsedScoreTypeRecentScore
最新スコアのタイプです。

##### <a name="FASLeaderboard.FASLeaderboardCompletionHandler"> (^FASLeaderboardCompletionHandler)(FASLeaderboard *leaderboard, NSError *error) </a>
グループメッセージ追加処理、グループメッセージ一件取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASLeaderboardCompletionHandler)(FASLeaderboard *leaderboard, NSError *error);

* Parameters
	* leaderboard
		* [FASLeaderboard](#FASLeaderboard)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASLeaderboard.FASLeaderboardsCompletionHandler"> (^FASLeaderboardsCompletionHandler)(NSArray *leaderboards, FASPagingMeta *meta, NSError *error) </a>
グループメセージ一覧取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASLeaderboardsCompletionHandler)(NSArray *leaderboards, FASPagingMeta *meta, NSError *error);

* Parameters
	* leaderboards
		* 複数の[FASLeaderboard](#FASLeaderboard)がNSArrayに格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[leaderboardId](#FASLeaderboard.leaderboardId)|リーダーボードID |
|[name](#FASLeaderboard.name)|リーダーボード名 |
|[submissionType](#FASLeaderboard.submissionType)|`best_score`もしくは`recent_score`  |
|[ascend](#FASLeaderboard.ascend)|昇順か否か |
|[createdAt](#FASLeaderboard.createdAt)|リーダーボード作成時刻 |
|[updatedAt](#FASLeaderboard.updatedAt)|リーダーボード更新時刻 |

##### <a name="FASLeaderboard.leaderboardId"> leaderboardId </a>
リーダーボードID

@property (nonatomic, readonly) NSString *leaderboardId;

##### <a name="FASLeaderboard.name"> name </a>
リーダーボード名

@property (nonatomic, readonly) NSString *name;

##### <a name="FASLeaderboard.usedScoreType"> usedScoreType </a>
`best_score`もしくは`recent_score`

@property (nonatomic, readonly) NSString *submissionType;

##### <a name="FASLeaderboard.ascend"> ascend </a>
昇順か否か

@property (nonatomic, readonly) BOOL ascend;

##### <a name="FASLeaderboard.createdAt"> createdAt </a>
リーダーボード作成時刻

@property (nonatomic, readonly) NSDate *createdAt;

##### <a name="FASLeaderboard.updatedAt"> updatedAt </a>
リーダーボード更新時刻

@property (nonatomic, readonly) NSDate *updatedAt;

#### Class Method

|Method|Description|
|------|-----|
|[fetchLeaderboardsWithPage:completion:](#FASLeaderboard.fetchLeaderboardsWithPagecompletion) |指定したリーダーボードIDのリーダーボード一覧を取得します。 |
|[fetchLeaderboardWithLeaderboardId:completion:](#FASLeaderboard.fetchLeaderboardWithLeaderboardIdcompletion) |指定したリーダーボードIDのリーダーボードを取得します。 |


##### <a name="FASLeaderboard.fetchLeaderboardsWithPagecompletion"> fetchLeaderboardsWithPage:completion: </a>
指定したリーダーボードIDのリーダーボード一覧を取得します。

\+ (void)fetchLeaderboardsWithPage:(NSUInteger)page
                        completion:(FASLeaderboardsCompletionHandler)completion;

* Parameters
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASLeaderboard.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASGroupMessage fetchLeaderboardsWithPage:1
                                    completion:(NSArray *leaderboards, FASPagingMeta *meta, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASLeaderboard.fetchLeaderboardWithLeaderboardIdcompletion"> fetchLeaderboardWithLeaderboardId:completion: </a>
指定したリーダーボードIDのリーダーボードを取得します。

\+ (void)fetchLeaderboardWithLeaderboardId:(NSString *)leaderboardId
                                completion:(FASLeaderboardCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASLeaderboard.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASGroupMessage fetchLeaderboardWithLeaderboardId:@"xxxxxxxxxxxxxx"
                                            completion:(FASLeaderboard *leaderboard, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```


### <a name="FASScore"> FASScore </a>
スコアモデルクラス。スコア機能にアクセスするためのクラスメソッドも提供しています。

#### Constants

|Constant|Description|
|------|-----|
|[FASScoreCompletionHandler](#FASScore.FASScoreCompletionHandler)|スコア登録、スコア一件取得処理を行った際に利用されるブロックオブジェクト。 |
|[FASScoresCompletionHandler](#FASScore.FASScoresCompletionHandler)|スコア一覧取得処理を行った際に利用されるブロックオブジェクト。 |


##### <a name="FASScore.FASScoreCompletionHandler"> (^FASScoreCompletionHandler)(FASScore *score, NSError *error) </a>
スコア登録、スコア一件取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASScoreCompletionHandler)(FASScore *score, NSError *error);

* Parameters
	* score
		* [FASScore](#FASScore)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASScore.FASScoresCompletionHandler"> (^FASScoresCompletionHandler)(NSArray *scores, NSError *error) </a>
スコア一覧取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASScoresCompletionHandler)(NSArray *scores, FASPagingMeta *meta, NSError *error);

* Parameters
	* scores
		* 複数の[FASScore](#FASScore)がNSArrayに格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[scoreId](#FASScore.scoreId)|スコアID |
|[value](#FASScore.value)|スコアの値 |
|[leaderboard](#FASScore.leaderboard)|リーダーボード情報 |
|[user](#FASScore.user)|ユーザー情報 |
|[createdAt](#FASScore.createdAt)|スコア作成時刻 |

##### <a name="FASScore.scoreId"> scoreId </a>
スコアID

@property (nonatomic, readonly) NSString *scoreId;

##### <a name="FASScore.value"> value </a>
スコアの値

@property (nonatomic, readonly) long long int value;

##### <a name="FASScore.leaderboard"> leaderboard </a>
リーダーボード情報。[FASLeaderboard](#FASLeaderboard)オブジェクト。

@property (nonatomic, readonly) FASLeaderboard *leaderboard;
##### <a name="FASScore.user"> user </a>
ユーザー情報。[FASUser](#FASUser)オブジェクト。

@property (nonatomic, readonly) FASUser *user;

##### <a name="FASScore.createdAt"> createdAt </a>
スコア作成時刻

@property (nonatomic, readonly) NSDate *createdAt;


#### Class Method

|Method|Description|
|------|-----|
|[submitScoreWithLeaderboardId:value:completion:](#FASScore.submitScoreWithLeaderboardIdvaluecompletion) |スコアを登録します。 |
|[submitScoreWithLeaderboardId:value:createdAt:completion:](#FASScore.submitScoreWithLeaderboardIdvaluecreatedAtcompletion) |作成時刻付きでスコアを登録します。 |
|[deleteScoreWithLeaderboaredId:scoreId:completion:](#FASScore.deleteScoreWithLeaderboaredIdscoreIdcompletion) |指定したスコアを削除します。 |
|[fetchScoreWithLeaderboardId:scoreId:completion:](#FASScore.fetchScoreWithLeaderboardIdscoreIdcompletion) |指定したスコアを取得します。 |
|[fetchScoresWithLeaderboardId:userId:page:completion:](#FASScore.fetchScoresWithLeaderboardIduserIdpagecompletion) |スコア一覧を取得します。 |
|[fetchScoresWithLeaderboardId:userId:startTime:sortBy:page:completion:](#FASScore.fetchScoresWithLeaderboardIduserIdstartTimesortBypagecompletion) |スコア一覧を取得します。 |

##### <a name="FASScore.submitScoreWithLeaderboardIdvaluecompletion"> submitScoreWithLeaderboardId:value:completion: </a>
スコアを登録します。

\+ (void)submitScoreWithLeaderboardId:(NSString *)leaderboardId
                                value:(long long int)value
                           completion:(FASScoreCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* value
		* スコアの値
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASScore.h>

	…
	…

- (IBAction)pushedSubmitButton:(id)sender
{
    [FASScore submitScoreWithLeaderboardId:@"xxxxxxxxxxxxxx"
                                     value:1000
                                completion:(FASScore *score, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASScore.deleteScoreWithLeaderboaredIdscoreIdcompletion"> submitScoreWithLeaderboardId:value:createdAt:completion: </a>
作成時刻付きでスコアを登録します。

\+ (void)submitScoreWithLeaderboardId:(NSString *)leaderboardId
                                value:(long long int)value
                            createdAt:(NSDate *)createdDate
                           completion:(FASScoreCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* value
		* スコアの値
	* createdAt
		* 作成時刻
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASScore.h>

	…
	…

- (IBAction)pushedSubmitButton:(id)sender
{
    [FASScore submitScoreWithLeaderboardId:@"xxxxxxxxxxxxxx"
                                     value:1000
                                 createdAt:[NSDate date]
                                completion:(FASScore *score, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASScore.submitScoreWithLeaderboardIdvaluecreatedAtcompletion"> deleteScoreWithLeaderboaredId:scoreId:completion: </a>
指定したスコアを削除します。

\+ (void)deleteScoreWithLeaderboaredId:(NSString *)leaderboardId
                               socreId:(NSString *)scoreId
                            completion:(FASCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* scoreId
		* スコアID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASScore.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASScore deleteScoreWithLeaderboaredId:@"xxxxxxxxxxxxxx"
                                    scoreId:@"yyyyyyyyyyyyy"
                                 completion:(NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASScore.fetchScoreWithLeaderboardIdscoreIdcompletion"> fetchScoreWithLeaderboardId:scoreId:completion: </a>
指定したスコアを取得します。

\+ (void)fetchScoreWithLeaderboardId:(NSString *)leaderboardId
                             scoreId:(NSString *)scoreId
                          completion:(FASScoreCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* scoreId
		* スコアID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASScore.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASScore fetchScoreWithLeaderboardId:@"xxxxxxxxxxxxxx"
                                  scoreId:@"yyyyyyyyyyyyy"
                               completion:(FASScore *score, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASScore.fetchScoresWithLeaderboardIduserIdpagecompletion"> fetchScoresWithLeaderboardId:userId:page:completion: </a>
対象ユーザーのベストスコア一覧を取得します。

\+ (void)fetchScoresWithLeaderboardId:(NSString *)leaderboardId
                               userId:(NSString *)userId
                                 page:(NSInteger)page
                           completion:(FASScoresCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* userId
		* ユーザーID
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASScore.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASScore fetchScoresWithLeaderboardId:@"xxxxxxxxxxxxxx"
                                    userId:@"yyyyyyyyyyyyy"
                                      page:1
                                completion:(NSArray *scores, FASPagingMeta *meta, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASScore.fetchScoresWithLeaderboardIduserIdstartTimesortBypagecompletion"> fetchScoresWithLeaderboardId:userId:startTime:sortBy:page:completion: </a>
対象ユーザーのスコア一覧を取得します。

\+ (void)fetchScoresWithLeaderboardId:(NSString *)leaderboardId
                               userId:(NSString *)userId
                            startTime:(NSDate *)startTime
                               sortBy:(NSString *)sortBy
                                 page:(NSInteger)page
                           completion:(FASScoresCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* userId
		* ユーザーID
	* startTime
		* 取得を開始する時刻
	* sortBy
		* `best_score` もしくは `recent_score`を指定
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASScore.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASScore fetchScoresWithLeaderboardId:@"xxxxxxxxxxxxxx"
                                    userId:@"yyyyyyyyyyyyy"
                                 startTime:[NSDate date]
                                    sortBy:@"best_score"
                                      page:1
                                completion:(NSArray *scores, FASPagingMeta *meta, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

### <a name="FASRank"> FASRank </a>
ランクモデルクラス。ランク機能にアクセスするためのクラスメソッドも提供しています。

#### Constants

|Constant|Description|
|------|-----|
|[FASRankCompletionHandler](#FASRank.FASRankCompletionHandler)|ランク取得処理を行った際に利用されるブロックオブジェクト。 |
|[FASRankingCompletionHandler](#FASRank.FASRankingCompletionHandler)|ランキング取得処理を行った際に利用されるブロックオブジェクト。 |


##### <a name="FASRank.FASRankCompletionHandler"> (^FASRankCompletionHandler)(FASRank *rank, NSError *error) </a>
ランク取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASRankCompletionHandler)(FASRank *rank, NSError *error);

* Parameters
	* rank
		* [FASRank](#FASRank)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASRank.FASRankingCompletionHandler"> (^FASRankingCompletionHandler)(NSArray *ranking, NSError *error) </a>
ランキング取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASRankingCompletionHandler)(NSArray *ranking, FASPagingMeta *meta, NSError *error);

* Parameters
	* ranking
		* 複数の[FASRank](#FASRank)がNSArrayに格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[rank](#FASRank.rank)|ランクの値 |
|[score](#FASRank.score)|スコア情報 |

##### <a name="FASRank.rank"> rank </a>
ランクの値

@property (nonatomic, readonly) long long int rank;

##### <a name="FASRank.score"> score </a>
スコア情報。[FASScore](#FASScore)のオブジェクト。

@property (nonatomic, readonly) FASScore *score;


#### Class Method

|Method|Description|
|------|-----|
|[fetchRankingWithLeaderboardId:startTime:onlyFriends:page:completion:](#FASRank.fetchRankingWithLeaderboardIdstartTimeonlyFriendspagecompletion) |ランキングを取得します。 |
|[fetchRankWithLeaderboardId:userId:startTime:onlyFriends:completion:](#FASRank.fetchRankWithLeaderboardIduserIdstartTimeonlyFriendscompletion) |特定ユーザーのランク情報を取得します。 |

##### <a name="FASRank.fetchRankingWithLeaderboardIdstartTimeonlyFriendspagecompletion"> fetchRankingWithLeaderboardId:startTime:onlyFriends:page:completion: </a>
ランキングを取得します。

\+ (void)fetchRankingWithLeaderboardId:(NSString *)leaderboardId
                             startTime:(NSDate *)startTime
                           onlyFriends:(BOOL)isOnlyFriends
                                  page:(NSUInteger)page
                            completion:(FASRankingCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* startTime
		* 取得を開始する時刻
	* onlyFriends
		* フレンドのみ表示したい場合は`YES`を指定。
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASRank.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASRank fetchRankingWithLeaderboardId:@"xxxxxxxxxxxxxx"
                                 startTime:[NSDate date]
                               onlyFriends:NO
                                      page:1
                                completion:(NSArray *ranking, FASPagingMeta *meta, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASRank.fetchRankWithLeaderboardIduserIdstartTimeonlyFriendscompletion"> fetchRankWithLeaderboardId:userId:startTime:onlyFriends:completion: </a>
特定ユーザーのランク情報を取得します。

\+ (void)fetchRankWithLeaderboardId:(NSString *)leaderboardId
                             userId:(NSString *)userId
                          startTime:(NSDate *)startTime
                        onlyFriends:(BOOL)isOnlyFriends
                         completion:(FASRankCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* userId
		* ユーザーID
	* startTime
		* 取得を開始する時刻
	* onlyFriends
		* フレンドのみ表示したい場合は`YES`を指定。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

Sample

```
#import <AppSteroid/FASRank.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASRank fetchRankWithLeaderboardId:@"xxxxxxxxxxxxxx"
                                 userId:@"yyyyyyyyyyyyyy"
                              startTime:[NSDate date]
                            onlyFriends:NO
                             completion:(FASRank *rank, NSError *error)
    {
        // 処理が完了したら呼ばれます。
    }];
}
```



### <a name="FASLeaderboardNavigationController"> FASLeaderboardNavigationController </a>
リーダーボードビューのベースとなるNavigationController

#### Properties

|Properties|Description|
|------|-----|
|[leaderboardId](#FASLeaderboardNavigationController.leaderboardId)|リーダーボードID |
|[onlyFriends](#FASLeaderboardNavigationController.onlyFriends)|フレンドのみ表示したい場合は`YES`を指定します。 |
|[animated](#FASLeaderboardNavigationController.animated)|ビューを閉じるときのアニメーション有無 |
|[dailySortOptions](#FASLeaderboardNavigationController.todaySortOptions)|リーダーボードの`today`セクションのソート方法を指定します。 |
|[weeklySortOptions](#FASLeaderboardNavigationController.weeklySortOptions)|リーダーボードの`weekly`セクションのソート方法を指定します。 |
|[totalSortOptions](#FASLeaderboardNavigationController.totalSortOptions)|リーダーボードの`total`セクションのソート方法を指定します。 |

##### <a name="FASLeaderboardNavigationController.leaderboardId"> leaderboardId </a>
表示したいリーダーボードのIDを指定します。

@property (nonatomic, copy) NSString *leaderboardId;

##### <a name="FASLeaderboardNavigationController.onlyFriends"> onlyFriends </a>
フレンドのみ表示したい場合は`YES`を指定します。デフォルトは`NO`です。

@property (nonatomic, assign) BOOL onlyFriends;

##### <a name="FASLeaderboardNavigationController.animated"> animated </a>
ビューを閉じるときにアニメーション付きで閉じるかどうかを設定します。デフォルトは`YES`です。

@property (nonatomic, assign) BOOL animated;

##### <a name="FASLeaderboardNavigationController.todaySortOptions"> dailySortOptions </a>
リーダーボードの`today`セクションのソート方法を指定します。[FASSortOptions](#FASSortOptions)の[dailyWithMinute:hour:](#FASSortOptions.dailyWithMinutehour)の返り値を指定してください。

@property (nonatomic, strong) FASSortOptions *dailySortOptions;

##### <a name="FASLeaderboardNavigationController.weeklySortOptions"> weeklySortOptions </a>
リーダーボードの`weekly`セクションのソート方法を指定します。[FASSortOptions](#FASSortOptions)の[weeklyWithMinute:hour:weekday:](#FASSortOptions.weeklyWithMinutehourweekday)の返り値を指定してください。

@property (nonatomic, strong) FASSortOptions *weeklySortOptions;

##### <a name="FASLeaderboardNavigationController.totalSortOptions"> totalSortOptions </a>
リーダーボードの`total`セクションのソート方法を指定します。[FASSortOptions](#FASSortOptions)の[total](#FASSortOptions.total)の返り値を指定してください。

@property (nonatomic, strong) FASSortOptions *totalSortOptions;

#### Class Method

|Method|Description|
|------|-----|
|[leaderboardNavigationController](#FASLeaderboardNavigationController.leaderboardNavigationController) |リーダーボードビューのベースとなる[FASLeaderboardNavigationController](#FASLeaderboardNavigationController)を返却します。 |
|[presentLeaderboardWithTarget:animated:](#FASLeaderboardNavigationController.presentLeaderboardWithTargetanimated) |リーダーボードビューを表示します。 |

##### <a name="FASLeaderboardNavigationController.leaderboardNavigationController"> leaderboardNavigationController </a>
リーダーボードビューのベースとなる[FASLeaderboardNavigationController](#FASLeaderboardNavigationController)を返却します。

\+ (FASLeaderboardNavigationController *)leaderboardNavigationController;

##### <a name="FASLeaderboardNavigationController.presentLeaderboardWithTargetanimated"> presentLeaderboardWithTarget:animated: </a>
リーダーボードビューを表示します。直近で作成したリーダーボードを表示します。

\+ (void)presentLeaderboardWithTarget:(UIViewController *)target
                             animated:(BOOL)animated;

* Parameters
	* target
		* ビューを表示する元となるViewControllerを指定します。
	* animated
		* YESならアニメーションさせて遷移します。

Sample

```
#import <AppSteroid/FASLeaderboardNavigationController.h>

	…
	…

- (IBAction)pushedLeaderboardButton:(id)sender
{
    [FASLeaderboardNavigationController presentLeaderboardWithTarget:self
                                                            animated:YES];
}
```

### <a name="FASLeaderboardLayout"> FASLeaderboardLayout </a>
リーダーボードビュー関連のレイアウトを変更します。

#### Properties

|Properties|Description|
|------|-----|
|[leaderboardLayoutBlocks](#FASLeaderboardLayout.leaderboardLayoutBlocks)|リーダーボードビューのレイアウトを変更するためのブロックオブジェクト |

##### <a name="FASLeaderboardLayout.leaderboardLayoutBlocks"> leaderboardLayoutBlocks </a>
リーダーボードビューのレイアウトを変更するためのブロックオブジェクト

@property (nonatomic, copy) FASLeaderboardViewController *(^leaderboardLayoutBlocks)(FASLeaderboardViewController *leaderboardViewController);

Sample - 背景色を変更するサンプル

```
[FASLeaderboardLayout sharedInstance].leaderboardLayoutBlocks = ^FASLeaderboardViewController *(FASLeaderboardViewController *leaderboardViewController)
    {
        leaderboardViewController.view.backgroundColor = [UIColor whiteColor];
        leaderboardViewController.tableView.backgroundColor = [UIColor whiteColor];
        if ([leaderboardViewController.navigationController.navigationBar respondsToSelector:@selector(barTintColor)])
        {
            leaderboardViewController.navigationController.navigationBar.tintColor = [UIColor greenColor];
            leaderboardViewController.navigationController.navigationBar.barTintColor = [UIColor whiteColor];
        }
        leaderboardViewController.navigationController.navigationBar.barStyle = UIBarStyleDefault;
        leaderboardViewController.navigationController.navigationBar.titleTextAttributes = @{NSForegroundColorAttributeName: [UIColor blackColor]};
        leaderboardViewController.leaderboardCellLayoutBlocks = ^FASLeaderboardCell *(FASLeaderboardCell *leaderboardCell)
        {
            leaderboardCell.contentView.backgroundColor = [UIColor whiteColor];
            leaderboardCell.userNameLabel.textColor = [UIColor blackColor];
            leaderboardCell.rankLabel.textColor = [UIColor blackColor];
            return leaderboardCell;
        };
        return leaderboardViewController;
    };
}
```

#### Class Method

|Method|Description|
|------|-----|
|[sharedInstance](#FASLeaderboardLayout.sharedInstance) |唯一のオブジェクトを返却します。 |

##### <a name="FASLeaderboardLayout.sharedInstance"> sharedInstance </a>
唯一のオブジェクトを返却します。

\+ (instancetype)sharedInstance;
