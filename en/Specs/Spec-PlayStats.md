# PlayStat Specifications

last update at 2015/3/25

---

## Introduction

Specification for features to get statistical game information.

---

## Classes

|Class|Description|
|------|-----|
|[FASPlayStat](#FASPlayStats)|Class to get statistical information |

---


### <a name="FASPlayStat"> FASPlayStat </a>
Class to get statistical information

#### Properties

|Properties|Description|
|------|-----|
|[FASPlayStatCompletionHandler](#FASPlayStat.FASPlayStatCompletionHandler)|Block object used when carrying out the process to receive statistical information. |
|[FASPlayStatsCompletionHandler](#FASPlayStat.FASPlayStatsCompletionHandler)|Block object used when carrying out the process to receive multiple statistical information. |

##### <a name="FASPlayStat.FASPlayStatCompletionHandler"> FASPlayStatCompletionHandler </a>
Block object used when carrying out the process to receive statistical information.

typedef void (^FASPlayStatCompletionHandler)(FASPlayStat *stat, NSError *error);

* Parameters
	* stat
		* [FASPlayStat](#FASPlayStat) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.
		
##### <a name="FASPlayStat.FASPlayStatsCompletionHandler"> FASPlayStatsCompletionHandler </a>
Block object used when carrying out the process to receive multiple statistical information. 

typedef void (^FASPlayStatsCompletionHandler)(NSArray *stats, FASPagingMeta *meta, NSError *error);

* Parameters
	* stats
		* Multiple [FASScore](#FASScore) are stored in NSArray.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[label](#FASPlayStat.label)|Label for aggregation |
|[value](#FASPlayStat.value)|Aggregation Value |
|[type](#FASPlayStat.type)|Type of aggregation. |

##### <a name="FASPlayStat.label"> label </a>
Label for aggregation

@property (nonatomic, readonly) NSString *label;

##### <a name="FASPlayStat.value"> value </a>
Aggregation Value 

@property (nonatomic, readonly) NSString. *value;

##### <a name="FASPlayStat.type"> type </a>
Type of aggregation target. We now have `leaderboard`,`user`,`key_value` for type.

@property (nonatomic, readonly) NSString *type;

#### Class Method

|Method|Description|
|------|-----|
|[fetchPlayStatsOfCurrentLoggedInUserWithCompletion:](#FASPlayStat.fetchPlayStatsOfCurrentLoggedInUserWithCompletion) |Get logged in user's statistic information |
|[fetchPlayStatsWithCcompletion:](#FASPlayStat.fetchPlayStatsWithCompletion) |Get all statistic information |
|[fetchPlayStatsWithUserIds:completion:](#FASPlayStat.fetchPlayStatsWithUserIdscompletion) |Get statistic information from a specific user |

##### <a name="FASPlayStat.fetchPlayStatsOfCurrentLoggedInUserWithCompletion"> fetchPlayStatsOfCurrentLoggedInUserWithCompletion: </a>
Get logged in user's statistic information

\+ (void)fetchPlayStatsOfCurrentLoggedInUserWithCompletion:(FASPlayStatsCompletionHandler)completion;

* Parameters
	* completion
		* Block object to be executed when the process is completed.
		
##### <a name="FASPlayStat.fetchPlayStatsWithCompletion"> fetchPlayStatsWithCcompletion: </a>
Get all statistic information

\+ (void)fetchPlayStatsWithCompletion:(FASPlayStatsCompletionHandler)completion;

* Parameters
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASPlayStat.fetchPlayStatsWithUserIdscompletion"> fetchPlayStatsWithUserIds:completion: </a>
Get statistic information from a specific user

\+ (void)fetchPlayStatsWithUserIds:(NSArray *)userIds
                       completion:(FASPlayStatsCompletionHandler)completion;

* Parameters
	* userIds
		* If of the user who you want to get the statistic info
	* completion
		* Block object to be executed when the process is completed.