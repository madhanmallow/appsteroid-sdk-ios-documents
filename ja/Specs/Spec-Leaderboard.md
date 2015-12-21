# Leaderboard Specifications

last update at 2015/12/19

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
|[FASGameEvent](#FASGameEvent)|ゲームイベントモデルクラス |
|[FASEventboard](#FASEventboard)|イベントボードモデルクラス |

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
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[leaderboardId](#FASLeaderboard.leaderboardId)|リーダーボードID |
|[leaderboardName](#FASLeaderboard.leaderboardName)|リーダーボード名 |
|[leaderboardDescription](#FASLeaderboard.leaderboardDescription)|リーダーボードの説明 |
|[iconUrl](#FASLeaderboard.iconUrl)|アイコン画像のURL |
|[submissionType](#FASLeaderboard.submissionType)|`best_score`もしくは`recent_score`  |
|[ascend](#FASLeaderboard.ascend)|昇順か否か |
|[createdAt](#FASLeaderboard.createdAt)|リーダーボード作成時刻 |
|[updatedAt](#FASLeaderboard.updatedAt)|リーダーボード更新時刻 |

##### <a name="FASLeaderboard.leaderboardId"> leaderboardId </a>
リーダーボードID

@property (nonatomic, readonly) NSString *leaderboardId;

##### <a name="FASLeaderboard.leaderboardName"> leaderboardName </a>
リーダーボード名

@property (nonatomic, readonly) NSString *leaderboardName;

##### <a name="FASLeaderboard.leaderboardDescription"> leaderboardDescription </a>
リーダーボードの説明

@property (nonatomic, readonly) NSString *leaderboardDescription;

##### <a name="FASLeaderboard.iconUrl"> iconUrl </a>
アイコン画像のURL

@property (nonatomic, readonly) NSString *iconUrl;

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
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[scoreId](#FASScore.scoreId)|スコアID |
|[value](#FASScore.value)|スコアの値 |
|[formattedValue](#FASScore.formattedValue)|フォーマットされたスコアの値 |
|[leaderboard](#FASScore.leaderboard)|リーダーボード情報 |
|[user](#FASScore.user)|ユーザー情報 |
|[createdAt](#FASScore.createdAt)|スコア作成時刻 |

##### <a name="FASScore.scoreId"> scoreId </a>
スコアID

@property (nonatomic, readonly) NSString *scoreId;

##### <a name="FASScore.value"> value </a>
スコアの値

@property (nonatomic, readonly) long long int value;

##### <a name="FASScore.formattedValue"> formattedValue </a>
フォーマットされたスコアの値

@property (nonatomic, readonly) NSString *formattedValue;

##### <a name="FASScore.leaderboard"> leaderboard </a>
リーダーボード情報。[FASLeaderboard](#FASLeaderboard)オブジェクト。

@property (nonatomic, readonly) FASLeaderboard *leaderboard;
##### <a name="FASScore.user"> user </a>
ユーザー情報。[FASUser](./Spec-User.md#FASUser)オブジェクト。

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
|[FASRankPeriod](#FASRank.FASRankPeriod)|集計するランキングの期間 |
|[FASRankCompletionHandler](#FASRank.FASRankCompletionHandler)|ランク取得処理を行った際に利用されるブロックオブジェクト。 |
|[FASRankingCompletionHandler](#FASRank.FASRankingCompletionHandler)|ランキング取得処理を行った際に利用されるブロックオブジェクト。 |

##### <a name="FASRank.FASRankPeriod"> FASRankPeriod </a>
集計するランキングの期間

```
typedef NS_ENUM(NSInteger, FASRankPeriod)
{
    FASRankPeriodDaily,
    FASRankPeriodWeekly,
    FASRankPeriodAll,
};
```
###### Constants
###### FASRankPeriodDaily
日間

###### FASRankPeriodWeekly
週間

###### FASRankPeriodAll
全ての期間

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
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
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
|[fetchRankingWithLeaderboardId:period:onlyFriends:page:completion:](#FASRank.fetchRankingWithLeaderboardIdperiodonlyFriendspagecompletion) |期間を指定してランキングを取得します。 |
|[fetchRankWithLeaderboardId:userId:period:onlyFriends:completion:](#FASRank.fetchRankWithLeaderboardIduserIdperiodonlyFriendscompletion) |特定ユーザーのランク情報を取得します。 |
|[fetchRankingWithEventboardId:onlyFriends:page:completion:](#FASRank.fetchRankingWithEventboardIdonlyFriendspagecompletion)|イベントに関するランキングを取得します。 |
|[fetchRankWithEventboardId:userId:onlyFriends:completion:](#FASRank.fetchRankWithEventboardIduserIdonlyFriendscompletion)|特定ユーザーのイベントに関するランク情報を取得します。 |

##### <a name="FASRank.fetchRankingWithLeaderboardIdperiodonlyFriendspagecompletion"> fetchRankingWithLeaderboardId:period:onlyFriends:page:completion: </a>
ランキングを取得します。

\+ (void)fetchRankingWithLeaderboardId:(NSString *)leaderboardId
                                period:(FASRankPeriod)period
                           onlyFriends:(BOOL)isOnlyFriends
                                  page:(NSUInteger)page
                            completion:(FASRankingCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* period
		* 集計期間
	* onlyFriends
		* フレンドのみ表示したい場合は`YES`を指定。
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

##### <a name="FASRank.fetchRankWithLeaderboardIduserIdperiodonlyFriendscompletion"> fetchRankWithLeaderboardId:userId:period:onlyFriends:completion: </a>
特定ユーザーのランク情報を取得します。

+ (void)fetchRankWithLeaderboardId:(NSString *)leaderboardId
                            userId:(NSString *)userId
                            period:(FASRankPeriod)period
                       onlyFriends:(BOOL)isOnlyFriends
                        completion:(FASRankCompletionHandler)completion;

* Parameters
	* leaderboardId
		* リーダーボードID
	* userId
		* ユーザーID
	* period
		* 集計期間
	* onlyFriends
		* フレンドのみ表示したい場合は`YES`を指定。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

##### <a name="FASRank.fetchRankingWithEventboardIdonlyFriendspagecompletion"> fetchRankingWithLeaderboardId:onlyFriends:page:completion: </a>
ランキングを取得します。

\+ (void)fetchRankingWithEventboardId:(NSString *)eventboardId
                          onlyFriends:(BOOL)isOnlyFriends
                                 page:(NSUInteger)page
                           completion:(FASRankingCompletionHandler)completion;

* Parameters
	* eventboardId
		* イベントボードID
	* onlyFriends
		* フレンドのみ表示したい場合は`YES`を指定。
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

##### <a name="FASRank.fetchRankWithEventboardIduserIdonlyFriendscompletion"> fetchRankWithLeaderboardId:userId:onlyFriends:completion: </a>
特定ユーザーのランク情報を取得します。

+ (void)fetchRankWithEventboardId:(NSString *)eventboardId
	                       userId:(NSString *)userId
                      onlyFriends:(BOOL)isOnlyFriends
                       completion:(FASRankCompletionHandler)completion;

* Parameters
	* eventboardId
		* イベントボードID
	* userId
		* ユーザーID
	* onlyFriends
		* フレンドのみ表示したい場合は`YES`を指定。
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

### <a name="FASGameEvent"> FASGameEvent </a>
ゲームイベントモデルクラス。ゲームイベントの作成はコンソールから行うことができます。

#### Constants

|Constant|Description|
|------|-----|
|[FASGameEventStatus](#FASGameEvent.FASGameEventStatus)|ゲームイベントの状態に関する定数群。 |
|[FASGameEventCompletionHandler](#FASGameEvent.FASGameEventCompletionHandler)|ゲームイベント処理を行った際に利用されるブロックオブジェクト。 |
|[FASGameEventsCompletionHandler](#FASGameEvent.FASGameEventsCompletionHandler)|複数のゲームイベント取得処理を行った際に利用されるブロックオブジェクト。 |

##### <a name="FASGameEvent.FASGameEventStatus"> FASGameEventStatus </a>
ゲームイベントの状態に関する定数が定義されています。  
ゲームイベントを取得する際に利用します。

```
typedef NS_ENUM(NSInteger, FASGameEventStatus)
{
    FASGameEventStatusUpcoming,
    FASGameEventStatusOngoing,
    FASGameEventStatusPast,
};
```

###### Constants
###### FASGameEventStatusUpcoming
まだ開始されていないゲームイベントの状態

###### FASGameEventStatusOngoing
現在開催中のゲームイベントの状態

###### FASGameEventStatusPast
すでに終了したゲームイベントの状態

##### <a name="FASGameEvent.FASGameEventCompletionHandler"> (^FASGameEventCompletionHandler)(FASGameEvent *event, NSError *error) </a>
ゲームイベント処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASGameEventCompletionHandler)(FASGameEvent *event, NSError *error);

* Parameters
	* event
		* [FASGameEvent](#FASGameEvent)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASGameEvent.FASGameEventsCompletionHandler"> (^FASRankingCompletionHandler)(NSArray *ranking, NSError *error) </a>
複数のゲームイベント取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASGameEventsCompletionHandler)(NSArray *events, FASPagingMeta *meta, NSError *error);

* Parameters
	* events
		* 複数の[FASGameEvent](#FASGameEvent)がNSArrayに格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[eventId](#FASGameEvent.eventId)|ゲームイベントID |
|[eventName](#FASGameEvent.eventName)|ゲームイベント名 |
|[eventDescription](#FASGameEvent.eventDescription)|ゲームイベントの説明 |
|[imageUrl](#FASGameEvent.imageUrl)|ゲームイベントの画像URL |
|[webSiteUrl](#FASGameEvent.webSiteUrl)|ゲームイベントのウェブサイトURL |
|[startAt](#FASGameEvent.startAt)|ゲームイベント開始時刻 |
|[endAt](#FASGameEvent.endAt)|ゲームイベント終了時刻 |
|[createdAt](#FASGameEvent.createdAt)|ゲームイベントが作成された時刻 |

##### <a name="FASGameEvent.eventId"> eventId </a>
ゲームイベントID

@property (nonatomic, readonly) NSString *eventId;

##### <a name="FASGameEvent.eventName"> eventName </a>
ゲームイベント名

@property (nonatomic, readonly) NSString *eventName;

##### <a name="FASGameEvent.eventDescription"> eventDescription </a>
ゲームイベントの説明

@property (nonatomic, readonly) NSString *eventDescription;

##### <a name="FASGameEvent.imageUrl"> imageUrl </a>
ゲームイベントの画像URL

@property (nonatomic, readonly) NSString *imageUrl;

##### <a name="FASGameEvent.webSiteUrl"> webSiteUrl </a>
ゲームイベントのウェブサイトURL

@property (nonatomic, readonly) NSString *webSiteUrl;

##### <a name="FASGameEvent.startAt"> startAt </a>
ゲームイベント開始時刻

@property (nonatomic, readonly) NSDate *startAt;

##### <a name="FASGameEvent.endAt"> endAt </a>
ゲームイベント終了時刻

@property (nonatomic, readonly) NSDate *endAt;

##### <a name="FASGameEvent.createdAt"> createdAt </a>
ゲームイベントが作成された時刻

@property (nonatomic, readonly) NSDate *createdAt;


#### Class Method

|Method|Description|
|------|-----|
|[fetchGameEventsWithStatus:page:completion:](#FASGameEvent.fetchGameEventsWithStatuspagecompletion) |ゲームイベントのリストを取得します。 |
|[fetchGameEventWithEventId:completion:](#FASGameEvent.fetchGameEventWithEventIdcompletion) |ゲームイベントを取得します。 |

##### <a name="FASGameEvent.fetchGameEventsWithStatuspagecompletion"> fetchGameEventsWithStatus:page:completion: </a>
ゲームイベントのリストを取得します。

\+ (void)fetchGameEventsWithStatus:(FASGameEventStatus)status
                             page:(NSUInteger)page
                       completion:(FASGameEventsCompletionHandler)completion;

* Parameters
	* status
		* ゲームイベントの状態を指定します。[FASGameEventStatus](#FASGameEvent.FASGameEventStatus)を参照してください。
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

##### <a name="FASGameEvent.fetchGameEventWithEventIdcompletion"> fetchGameEventWithEventId:completion: </a>
ゲームイベントを取得します。

\+ (void)fetchGameEventWithEventId:(NSString *)eventId
                       completion:(FASGameEventCompletionHandler)completion;

* Parameters
	* eventId
		* ゲームイベントID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

### <a name="FASEventboard"> FASEventboard </a>
ゲームイベントに登録されているリーダーボードのモデル。

#### Constants

|Constant|Description|
|------|-----|
|[FASEventboardCompletionHandler](#FASEventboard.FASEventboardCompletionHandler)|イベントボード処理を行った際に利用されるブロックオブジェクト。 |
|[FASEventboardsCompletionHandler](#FASEventboard.FASEventboardsCompletionHandler)|複数のイベントボード取得処理を行った際に利用されるブロックオブジェクト。 |

##### <a name="FASEventboard.FASEventboardCompletionHandler"> (^FASEventboardCompletionHandler)(FASEventboard *eventboard, NSError *error) </a>
イベントボード処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASEventboardCompletionHandler)(FASEventboard *eventboard, NSError *error);

* Parameters
	* eventboard
		* [FASEventboard](#FASEventboard)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASEventboard.FASEventboardsCompletionHandler"> (^FASEventboardsCompletionHandler)(NSArray *eventboards, FASPagingMeta *meta, NSError *error) </a>
複数のイベントボード取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASEventboardsCompletionHandler)(NSArray *eventboards, FASPagingMeta *meta, NSError *error);

* Parameters
	* eventboards
		* 複数の[FASEventboard](#FASEventboard)がNSArrayに格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[eventboardId](#FASEventboard.eventboardId)|イベントボードID |
|[leaderboard](#FASEventboard.leaderboard)|ゲームイベントに登録されているリーダーボード |
|[gameEvent](#FASEventboard.gameEvent)|ゲームイベント |

##### <a name="FASEventboard.eventboardId"> eventboardId </a>
イベントボードID

@property (nonatomic, readonly) NSString *eventboardId;

##### <a name="FASEventboard.leaderboard"> leaderboard </a>
ゲームイベントに登録されている[FASLeaderboard](#FASLeaderboard)オブジェクト。

@property (nonatomic, readonly) FASLeaderboard *leaderboard;

##### <a name="FASEventboard.gameEvent"> gameEvent </a>
[FASGameEvent](#FASGameEvent)オブジェクト。

@property (nonatomic, readonly) FASGameEvent *gameEvent;

#### Class Method

|Method|Description|
|------|-----|
|[fetchEventboardsWithPage:completion:](#FASEventboard.fetchEventboardsWithPagecompletion) |イベントボード一覧を取得します。 |
|[fetchEventboardsWithEventId:page:completion:](#FASEventboard.fetchEventboardsWithEventIdpagecompletion) |イベントIDを指定してイベントボード一覧を取得します。 |
|[fetchEventboardWithEventboardId:completion:](#FASEventboard.fetchEventboardWithEventboardIdcompletion) |イベントボードを取得します。 |

##### <a name="FASEventboard.fetchEventboardsWithPagecompletion"> fetchEventboardsWithPage:completion: </a>
イベントボード一覧を取得します。

\+ (void)fetchEventboardsWithPage:(NSUInteger)page
                      completion:(FASEventboardsCompletionHandler)completion;

* Parameters
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

##### <a name="FASEventboard.fetchEventboardsWithEventIdpagecompletion"> fetchEventboardsWithEventId:page:completion: </a>
イベントIDを指定してイベントボード一覧を取得します。

\+ (void)fetchEventboardsWithEventId:(NSString *)eventId
                               page:(NSUInteger)page
                         completion:(FASEventboardsCompletionHandler)completion;

* Parameters
	* eventId
		* ゲームイベントID
	* page
		* ページ番号
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

##### <a name="FASEventboard.fetchEventboardWithEventboardIdcompletion"> fetchEventboardWithEventboardId:completion: </a>
イベントボードを取得します。

\+ (void)fetchEventboardWithEventboardId:(NSString *)eventboardId
                             completion:(FASEventboardCompletionHandler)completion;

* Parameters
	* eventboardId
		* イベントボードID
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。
