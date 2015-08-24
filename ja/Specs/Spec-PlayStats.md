# PlayStat Specifications

last update at 2015/3/25

---

## Introduction

ゲームの統計情報を取得する機能に関する仕様書です。

---

## Classes

|Class|Description|
|------|-----|
|[FASPlayStat](#FASPlayStats)|統計情報を取得するためのクラス |

---


### <a name="FASPlayStat"> FASPlayStat </a>
統計情報を取得するためのクラス

#### Properties

|Properties|Description|
|------|-----|
|[FASPlayStatCompletionHandler](#FASPlayStat.FASPlayStatCompletionHandler)|統計情報の受信処理を行った際に利用されるブロックオブジェクト |
|[FASPlayStatsCompletionHandler](#FASPlayStat.FASPlayStatsCompletionHandler)|複数の統計情報の受信処理を行った際に利用されるブロックオブジェクト |

##### <a name="FASPlayStat.FASPlayStatCompletionHandler"> FASPlayStatCompletionHandler </a>
統計情報の受信処理を行った際に利用されるブロックオブジェクト

typedef void (^FASPlayStatCompletionHandler)(FASPlayStat *stat, NSError *error);

* Parameters
	* stat
		* [FASPlayStat](#FASPlayStat)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。
		
##### <a name="FASPlayStat.FASPlayStatsCompletionHandler"> FASPlayStatsCompletionHandler </a>
複数の統計情報の受信処理を行った際に利用されるブロックオブジェクト

typedef void (^FASPlayStatsCompletionHandler)(NSArray *stats, FASPagingMeta *meta, NSError *error);

* Parameters
	* stats
		* 複数の[FASPlayStat](#FASPlayStat)がNSArrayに格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../7_Spec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[label](#FASPlayStat.label)|集計用のラベル |
|[value](#FASPlayStat.value)|集計値 |
|[type](#FASPlayStat.type)|集計対象の種類 |

##### <a name="FASPlayStat.label"> label </a>
集計用のラベル

@property (nonatomic, readonly) NSString *label;

##### <a name="FASPlayStat.value"> value </a>
集計値

@property (nonatomic, readonly) NSString. *value;

##### <a name="FASPlayStat.type"> type </a>
集計対象の種類。現在は`leaderboard`,`user`,`key_value`の種類があります。

@property (nonatomic, readonly) NSString *type;

#### Class Method

|Method|Description|
|------|-----|
|[fetchPlayStatsOfCurrentLoggedInUserWithCompletion:](#FASPlayStat.fetchPlayStatsOfCurrentLoggedInUserWithCompletion) |ログインユーザーの統計情報を取得します。 |
|[fetchPlayStatsWithCcompletion:](#FASPlayStat.fetchPlayStatsWithCompletion) |全ての統計情報を取得します。 |
|[fetchPlayStatsWithUserIds:completion:](#FASPlayStat.fetchPlayStatsWithUserIdscompletion) |対象ユーザーの統計情報を取得します。 |

##### <a name="FASPlayStat.fetchPlayStatsOfCurrentLoggedInUserWithCompletion"> fetchPlayStatsOfCurrentLoggedInUserWithCompletion: </a>
ログインユーザーの統計情報を取得します。

\+ (void)fetchPlayStatsOfCurrentLoggedInUserWithCompletion:(FASPlayStatsCompletionHandler)completion;

* Parameters
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。
		
##### <a name="FASPlayStat.fetchPlayStatsWithCompletion"> fetchPlayStatsWithCcompletion: </a>
全ての統計情報を取得します。

\+ (void)fetchPlayStatsWithCompletion:(FASPlayStatsCompletionHandler)completion;

* Parameters
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。

##### <a name="FASPlayStat.fetchPlayStatsWithUserIdscompletion"> fetchPlayStatsWithUserIds:completion: </a>
対象ユーザーの統計情報を取得します。

\+ (void)fetchPlayStatsWithUserIds:(NSArray *)userIds
                       completion:(FASPlayStatsCompletionHandler)completion;

* Parameters
	* userIds
		* 統計を取得したいユーザーのId
	* completion
		* 処理が完了した時に実行されるブロックオブジェクト。