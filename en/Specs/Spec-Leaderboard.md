# Leaderboard Specifications

last update at 2014/10/24

---

## Introduction

Specification for functions related to Leaderboard.
You can submit scores to a specific leaderboard or get ranking info from a specific users. Leaderboard can be created and easily be managed on the AppSteroid web console.  We also provide a leaderboard GUI for integration. Check [LeaderboardGetStarted](../GetStarted/GetStarted-Leaderboard.md) for more information about GUI.

---

## Classes

|Class|Description|
|------|-----|
|[FASLeaderboard](#FASLeaderboard)|Leaderboard model class |
|[FASScore](#FASScore)|Score model class |
|[FASRank](#FASRank)|Rank model class |
|[FASSortOptions](#FASSortOptions)|Class for sorting ranking |
|[FASLeaderboardNavigationController](#FASLeaderboardNavigationController)|NavigationController, which is a base of Leaderboard view |
|[FASLeaderboardLayout](#FASLeaderboardLayout)|Class to change layout of Leaderboard View |


---

## APIs
### <a name="FASLeaderboard"> FASLeaderboard </a>
Leaderboard model class. Also provides class method to access Leaderboard features.

#### Constants

|Constant|Description|
|------|-----|
|[FASLeaderboardUsedScoreType](#FASLeaderboard.FASLeaderboardUsedScoreType)|Score types used for leaderboard. Best score and latest score is defined. |
|[FASLeaderboardCompletionHandler](#FASLeaderboard.FASLeaderboardCompletionHandler)|Block object used when carrying out the process to get a single leaderboard. |
|[FASLeaderboardsCompletionHandler](#FASLeaderboard.FASLeaderboardsCompletionHandler)|Block object used when carrying out the process to get a list of leaderboard. |

##### <a name="FASLeaderboard.FASLeaderboardSubmissionType"> FASLeaderboardSubmissionType </a>
Score types used for leaderboard. Best score and latest score is defined.

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
Used when a invalid status was returned.

###### FASLeaderboardUsedScoreTypeBestScore
Score type for Leaderboard using Best Score

###### FASLeaderboardUsedScoreTypeRecentScore
Score type for Leaderboard using Latest Score

##### <a name="FASLeaderboard.FASLeaderboardCompletionHandler"> (^FASLeaderboardCompletionHandler)(FASLeaderboard *leaderboard, NSError *error) </a>
Block object used when carrying out the process to get a single leaderboard.

typedef void (^FASLeaderboardCompletionHandler)(FASLeaderboard *leaderboard, NSError *error);

* Parameters
	* leaderboard
		* [FASLeaderboard](#FASLeaderboard) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASLeaderboard.FASLeaderboardsCompletionHandler"> (^FASLeaderboardsCompletionHandler)(NSArray *leaderboards, FASPagingMeta *meta, NSError *error) </a>
Block object used when carrying out the process to get a list of leaderboard.

typedef void (^FASLeaderboardsCompletionHandler)(NSArray *leaderboards, FASPagingMeta *meta, NSError *error);

* Parameters
	* leaderboards
		* Multiple [FASLeaderboard](#FASLeaderboard) are stored in NSArray.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[leaderboardId](#FASLeaderboard.leaderboardId)|Leaderboard ID |
|[name](#FASLeaderboard.name)|Leaderboard Name |
|[submissionType](#FASLeaderboard.submissionType)|`best_score` or `recent_score`  |
|[ascend](#FASLeaderboard.ascend)|Ascend order or not |
|[createdAt](#FASLeaderboard.createdAt)|Leaderboard creation date & time |
|[updatedAt](#FASLeaderboard.updatedAt)|Leaderboard updated date & time |

##### <a name="FASLeaderboard.leaderboardId"> leaderboardId </a>
Leaderboard ID

@property (nonatomic, readonly) NSString *leaderboardId;

##### <a name="FASLeaderboard.name"> name </a>
Leaderboard Name

@property (nonatomic, readonly) NSString *name;

##### <a name="FASLeaderboard.usedScoreType"> usedScoreType </a>
`best_score` or `recent_score`

@property (nonatomic, readonly) NSString *submissionType;

##### <a name="FASLeaderboard.ascend"> ascend </a>
Ascend order or not

@property (nonatomic, readonly) BOOL ascend;

##### <a name="FASLeaderboard.createdAt"> createdAt </a>
Leaderboard creation date & time

@property (nonatomic, readonly) NSDate *createdAt;

##### <a name="FASLeaderboard.updatedAt"> updatedAt </a>
Leaderboard updated date & time

@property (nonatomic, readonly) NSDate *updatedAt;

#### Class Method

|Method|Description|
|------|-----|
|[fetchLeaderboardsWithPage:completion:](#FASLeaderboard.fetchLeaderboardsWithPagecompletion) |Get leaderboard list from a specified leaderboard ID. |
|[fetchLeaderboardWithLeaderboardId:completion:](#FASLeaderboard.fetchLeaderboardWithLeaderboardIdcompletion) |Get leaderboard from a specified leaderboard ID. |


##### <a name="FAS Leaderboard.fetchLeaderboardsWithPagecompletion"> fetchLeaderboardsWithPage:completion: </a>
Get leaderboard list from a specified leaderboard ID.

\+ (void)fetchLeaderboardsWithPage:(NSUInteger)page
                        completion:(FASLeaderboardsCompletionHandler)completion;

* Parameters
	* page
		* Page number
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASLeaderboard.fetchLeaderboardWithLeaderboardIdcompletion"> fetchLeaderboardWithLeaderboardId:completion: </a>
Get leaderboard from a specified leaderboard ID.

\+ (void)fetchLeaderboardWithLeaderboardId:(NSString *)leaderboardId
                                completion:(FASLeaderboardCompletionHandler)completion;

* Parameters
	* leaderboardId
		* Leaderboard ID
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed.
    }];
}
```


### <a name="FASScore"> FASScore </a>
Score model Class. Also provides class method to access Score features.

#### Constants

|Constant|Description|
|------|-----|
|[FASScoreCompletionHandler](#FASScore.FASScoreCompletionHandler)|Block object used when carrying out the process to submit a score and get a score. |
|[FASScoresCompletionHandler](#FASScore.FASScoresCompletionHandler)|Block object used when carrying out the process to get score list. |


##### <a name="FASScore.FASScoreCompletionHandler"> (^FASScoreCompletionHandler)(FASScore *score, NSError *error) </a>
Block object used when carrying out the process to submit a score and get a score.

typedef void (^FASScoreCompletionHandler)(FASScore *score, NSError *error);

* Parameters
	* score
		* [FASScore](#FASScore) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASScore.FASScoresCompletionHandler"> (^FASScoresCompletionHandler)(NSArray *scores, NSError *error) </a>
Block object used when carrying out the process to get score list.

typedef void (^FASScoresCompletionHandler)(NSArray *scores, FASPagingMeta *meta, NSError *error);

* Parameters
	* scores
		* Multiple [FASScore](#FASScore) are stored in NSArray.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[scoreId](#FASScore.scoreId)|Score ID |
|[value](#FASScore.value)|Score Value |
|[leaderboard](#FASScore.leaderboard)|Leaderboard information |
|[user](#FASScore.user)|User information |
|[createdAt](#FASScore.createdAt)|Score creation date & time |

##### <a name="FASScore.scoreId"> scoreId </a>
Score ID

@property (nonatomic, readonly) NSString *scoreId;

##### <a name="FASScore.value"> value </a>
Score Value

@property (nonatomic, readonly) long long int value;

##### <a name="FASScore.leaderboard"> leaderboard </a>
Leaderboard information. [FASLeaderboard](#FASLeaderboard) Object.

@property (nonatomic, readonly) FASLeaderboard *leaderboard;
##### <a name="FASScore.user"> user </a>
User information. [FASUser](#FASUser) Object.

@property (nonatomic, readonly) FASUser *user;

##### <a name="FASScore.createdAt"> createdAt </a>
Score creation date & time.

@property (nonatomic, readonly) NSDate *createdAt;


#### Class Method

|Method|Description|
|------|-----|
|[submitScoreWithLeaderboardId:value:completion:](#FASScore.submitScoreWithLeaderboardIdvaluecompletion) |Submit score |
|[submitScoreWithLeaderboardId:value:createdAt:completion:](#FASScore.submitScoreWithLeaderboardIdvaluecreatedAtcompletion) |Submit score with date and time |
|[deleteScoreWithLeaderboaredId:scoreId:completion:](#FASScore.deleteScoreWithLeaderboaredIdscoreIdcompletion) |Delete specified score |
|[fetchScoreWithLeaderboardId:scoreId:completion:](#FASScore.fetchScoreWithLeaderboardIdscoreIdcompletion) |Get specified score |
|[fetchScoresWithLeaderboardId:userId:page:completion:](#FASScore.fetchScoresWithLeaderboardIduserIdpagecompletion) |Get best score list of a target user |
|[fetchScoresWithLeaderboardId:userId:startTime:sortBy:page:completion:](#FASScore.fetchScoresWithLeaderboardIduserIdstartTimesortBypagecompletion) |Get score list of a target user |

##### <a name="FASScore.submitScoreWithLeaderboardIdvaluecompletion"> submitScoreWithLeaderboardId:value:completion: </a>
Submit score

\+ (void)submitScoreWithLeaderboardId:(NSString *)leaderboardId
                                value:(long long int)value
                           completion:(FASScoreCompletionHandler)completion;

* Parameters
	* leaderboardId
		* Leaderboard ID
	* value
		* Score value
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASScore.deleteScoreWithLeaderboaredIdscoreIdcompletion"> submitScoreWithLeaderboardId:value:createdAt:completion: </a>
Submit score with date and time

\+ (void)submitScoreWithLeaderboardId:(NSString *)leaderboardId
                                value:(long long int)value
                            createdAt:(NSDate *)createdDate
                           completion:(FASScoreCompletionHandler)completion;

* Parameters
	* leaderboardId
		* Leaderboard ID
	* value
		* Score Value
	* createdAt
		* Created date and time
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASScore.submitScoreWithLeaderboardIdvaluecreatedAtcompletion"> deleteScoreWithLeaderboaredId:scoreId:completion: </a>
Delete specified score

\+ (void)deleteScoreWithLeaderboaredId:(NSString *)leaderboardId
                               socreId:(NSString *)scoreId
                            completion:(FASCompletionHandler)completion;

* Parameters
	* leaderboardId
		* Leaderboard ID
	* scoreId
		* Score ID
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASScore.fetchScoreWithLeaderboardIdscoreIdcompletion"> fetchScoreWithLeaderboardId:scoreId:completion: </a>
Get specified score

\+ (void)fetchScoreWithLeaderboardId:(NSString *)leaderboardId
                             scoreId:(NSString *)scoreId
                          completion:(FASScoreCompletionHandler)completion;

* Parameters
	* leaderboardId
		* Leaderboard ID
	* scoreId
		* Score ID
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASScore.fetchScoresWithLeaderboardIduserIdpagecompletion"> fetchScoresWithLeaderboardId:userId:page:completion: </a>
Get best score list of a target user

\+ (void)fetchScoresWithLeaderboardId:(NSString *)leaderboardId
                               userId:(NSString *)userId
                                 page:(NSInteger)page
                           completion:(FASScoresCompletionHandler)completion;

* Parameters
	* leaderboardId
		* Leaderboard ID
	* userId
		* User ID
	* page
		* Page number
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed
    }];
}
```

##### <a name="FASScore.fetchScoresWithLeaderboardIduserIdstartTimesortBypagecompletion"> fetchScoresWithLeaderboardId:userId:startTime:sortBy:page:completion: </a>
Get score list of a target user

\+ (void)fetchScoresWithLeaderboardId:(NSString *)leaderboardId
                               userId:(NSString *)userId
                            startTime:(NSDate *)startTime
                               sortBy:(NSString *)sortBy
                                 page:(NSInteger)page
                           completion:(FASScoresCompletionHandler)completion;

* Parameters
	* leaderboardId
		* Leaderboard ID
	* userId
		* User ID
	* startTime
		* Time to start collecting data
	* sortBy
		* Select `best_score` or `recent_score`
	* page
		* Page number
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed
    }];
}
```

### <a name="FASRank"> FASRank </a>
Rank model Class. Also provides class method to access Rank features.

#### Constants

|Constant|Description|
|------|-----|
|[FASRankCompletionHandler](#FASRank.FASRankCompletionHandler)|Block object used when carrying out the process to get Rank. |
|[FASRankingCompletionHandler](#FASRank.FASRankingCompletionHandler)|Block object used when carrying out the process to get Ranking.　|


##### <a name="FASRank.FASRankCompletionHandler"> (^FASRankCompletionHandler)(FASRank *rank, NSError *error) </a>
Block object used when carrying out the process to get Rank.

typedef void (^FASRankCompletionHandler)(FASRank *rank, NSError *error);

* Parameters
	* rank
		* [FASRank](#FASRank) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASRank.FASRankingCompletionHandler"> (^FASRankingCompletionHandler)(NSArray *ranking, NSError *error) </a>
Block object used when carrying out the process to get Ranking.

typedef void (^FASRankingCompletionHandler)(NSArray *ranking, FASPagingMeta *meta, NSError *error);

* Parameters
	* ranking
		* Multiple [FASRank](#FASRank) are stored in NSArray.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[rank](#FASRank.rank)|Rank value |
|[score](#FASRank.score)|Score information |

##### <a name="FASRank.rank"> rank </a>
Rank value

@property (nonatomic, readonly) long long int rank;

##### <a name="FASRank.score"> score </a>
Score information. [FASScore](#FASScore) Object.

@property (nonatomic, readonly) FASScore *score;


#### Class Method

|Method|Description|
|------|-----|
|[fetchRankingWithLeaderboardId:startTime:onlyFriends:page:completion:](#FASRank.fetchRankingWithLeaderboardIdstartTimeonlyFriendspagecompletion) |Get Ranking |
|[fetchRankWithLeaderboardId:userId:startTime:onlyFriends:completion:](#FASRank.fetchRankWithLeaderboardIduserIdstartTimeonlyFriendscompletion) |Get rank information of a specific user. |

##### <a name="FASRank.fetchRankingWithLeaderboardIdstartTimeonlyFriendspagecompletion"> fetchRankingWithLeaderboardId:startTime:onlyFriends:page:completion: </a>
Get Ranking

\+ (void)fetchRankingWithLeaderboardId:(NSString *)leaderboardId
                             startTime:(NSDate *)startTime
                           onlyFriends:(BOOL)isOnlyFriends
                                  page:(NSUInteger)page
                            completion:(FASRankingCompletionHandler)completion;

* Parameters
	* leaderboardId
		* Leaderboard ID
	* startTime
		* Starting time of getting data.
	* onlyFriends
		* Select `YES` to only display friends on leaderboard.
	* page
		* Page number
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed
    }];
}
```

##### <a name="FASRank.fetchRankWithLeaderboardIduserIdstartTimeonlyFriendscompletion"> fetchRankWithLeaderboardId:userId:startTime:onlyFriends:completion: </a>
Get rank information of a specific user.

\+ (void)fetchRankWithLeaderboardId:(NSString *)leaderboardId
                             userId:(NSString *)userId
                          startTime:(NSDate *)startTime
                        onlyFriends:(BOOL)isOnlyFriends
                         completion:(FASRankCompletionHandler)completion;

* Parameters
	* leaderboardId
		* Leaderboard ID
	* userId
		* User ID
	* startTime
		* Starting time of getting data.
	* onlyFriends
		* Select `YES` to only display friends on leaderboard.
	* completion
		* Block object to be executed when the process is completed.

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
        // It will be called when the process is completed.
    }];
}
```

### <a name="FASSortOptions"> FASSortOptions </a>
Used when aggregating ranking on leaderboard.

#### Properties

|Properties|Description|
|------|-----|
|[timeZone](#FASSortOptions.timeZone)|Timezone |
|[date](#FASSortOptions.date)|Date/time |

##### <a name="FASSortOptions.timeZone"> timeZone </a>
Timezone

@property (nonatomic, readonly) NSTimeZone *timeZone;

##### <a name="FASSortOptions.date"> date </a>
Date/time

@property (nonatomic, readonly) NSDate *date;


#### Class Method

|Method|Description|
|------|-----|
|[dailyWithMinute:hour:](#FASSortOptions.dailyWithMinutehour) |Used for daily aggregation. |
|[dailyWithMinute:hour:timeZone:](#FASSortOptions.dailyWithMinutehourtimeZone) |Used for daily aggregation. |
|[weeklyWithMinute:hour:weekday:](#FASSortOptions.weeklyWithMinutehourweekday) |Used for weekly aggregation. |
|[weeklyWithMinute:hour:weekday:timeZone:](#FASSortOptions.weeklyWithMinutehourweekdaytimeZone) |Used for weekly aggregation. |
|[total](#FASSortOptions.total) |Used for total aggregation. |

##### <a name="FASSortOptions.dailyWithMinutehour"> dailyWithMinute:hour: </a>
Used for daily aggregation. Set a starting time (hour and minute) for aggregation. System timezone will be the default setting for timezone.

\+ (instancetype)dailyWithMinute:(NSUInteger)minute
                            hour:(NSUInteger)hour;

* Parameters
	* minute
		* Select minute
	* hour
		* Select hour

Sample

```
#import <AppSteroid/FASSortOptions.h>

	…
	…

- (IBAction)pushedShowLeaderboardButton:(id)sender
{
    // Aggregate ranking data everyday at 19:00.
    FASSortOptions *dailyOption = [FASSortOptions dailyWithMinute:0 hour:19];

    FASLeaderboardNavigationController *leaderboardNavigationController = [FASLeaderboardNavigationController leaderboardNavigationController];
    leaderboardNavigationController.dailySortOptions = dailyOption;

    [self presentViewController:leaderboardNavigationController animated:YES completion:nil];
}
```

##### <a name="FASSortOptions.dailyWithMinutehourtimeZone"> dailyWithMinute:hour:timeZone: </a>
Used for daily aggregation. Set a starting time (hour and minute) and timezone.

\+ (instancetype)dailyWithMinute:(NSUInteger)minute
                            hour:(NSUInteger)hour
                        timeZone:(NSTimeZone *)timeZone;

* Parameters
	* minute
		* Select minute
	* hour
		* Select hour
	* timeZone
		* Select timezone

Sample

```
#import <AppSteroid/FASLeaderboardNavigationController.h>
#import <AppSteroid/FASSortOptions.h>

	…
	…

- (IBAction)pushedShowLeaderboardButton:(id)sender
{
    // Aggregate ranking data everyday at GMT 19:00.
    NSTimeZone *timeZone = [NSTimeZone timeZoneWithAbbreviation:@"GMT"];
    FASSortOptions *dailyOption = [FASSortOptions dailyWithMinute:0 hour:19 timeZone:timeZone];

    FASLeaderboardNavigationController *leaderboardNavigationController = [FASLeaderboardNavigationController leaderboardNavigationController];
    leaderboardNavigationController.dailySortOptions = dailyOption;

    [self presentViewController:leaderboardNavigationController animated:YES completion:nil];
}
```

##### <a name="FASSortOptions.weeklyWithMinutehourweekday"> weeklyWithMinute:hour:weekday: </a>
Used for weekly aggregation. Set a starting week, hour and minute for aggregation. System timezone will be the default setting for timezone.

\+ (instancetype)weeklyWithMinute:(NSUInteger)minute
                             hour:(NSUInteger)hour
                          weekday:(NSUInteger)weekday;

* Parameters
	* minute
		* Select minute between 0 to 59.
	* hour
		* Select hour between 0 to 23.
	* weekday
		* Select week between 1 to 7. 1:Sunday, 2:Monday, 3:Tuesday, 4:Wednesday, 5:Thursday, 6:Friday, 7:Saturday.

Sample

```
#import <AppSteroid/FASSortOptions.h>

	…
	…

- (IBAction)pushedShowLeaderboardButton:(id)sender
{
    // Aggregate ranking data every Monday at 19:00.
    FASSortOptions *weeklyOption = [FASSortOptions weeklyWithMinute:0 hour:19 weekday:2];

    FASLeaderboardNavigationController *leaderboardNavigationController = [FASLeaderboardNavigationController leaderboardNavigationController];
    leaderboardNavigationController.weeklySortOptions = weeklyOption;

    [self presentViewController:leaderboardNavigationController animated:YES completion:nil];
}
```

##### <a name="FASSortOptions.weeklyWithMinutehourweekdaytimeZone"> weeklyWithMinute:hour:weekday:timeZone: </a>
Used for weekly aggregation. Set a starting week, hour, minute and timezone for aggregation.

\+ (instancetype)weeklyWithMinute:(NSUInteger)minute
                             hour:(NSUInteger)hour
                          weekday:(NSUInteger)weekday
                         timeZone:(NSTimeZone *)timeZone;;

* Parameters
	* minute
		* Select minute between 0 to 59.
	* hour
		* Select hour between 0 to 23.
	* weekday
		* Select week between 1 to 7. 1:Sunday, 2:Monday, 3:Tuesday, 4:Wednesday, 5:Thursday, 6:Friday, 7:Saturday.
	* timeZone
		* Select timezone.

Sample

```
#import <AppSteroid/FASSortOptions.h>

	…
	…

- (IBAction)pushedShowLeaderboardButton:(id)sender
{
    // Aggregate ranking data every Monday at GMT 19:00.
    NSTimeZone *timeZone = [NSTimeZone timeZoneWithAbbreviation:@"GMT"];
    FASSortOptions *weeklyOption = [FASSortOptions weeklyWithMinute:0 hour:19 weekday:2 timeZone:timeZone];

    FASLeaderboardNavigationController *leaderboardNavigationController = [FASLeaderboardNavigationController leaderboardNavigationController];
    leaderboardNavigationController.weeklySortOptions = weeklyOption;

    [self presentViewController:leaderboardNavigationController animated:YES completion:nil];
}
```

##### <a name="FASSortOptions.total"> total </a>
Used for total aggregation

\+ (instancetype)total;

Sample

```
#import <AppSteroid/FASSortOptions.h>

	…
	…

- (IBAction)pushedShowLeaderboardButton:(id)sender
{
    // Aggregate all the ranking data up to
    FASSortOptions *totalOption = [FASSortOptions total];

    FASLeaderboardNavigationController *leaderboardNavigationController = [FASLeaderboardNavigationController leaderboardNavigationController];
    leaderboardNavigationController.totalSortOptions = totalOption;

    [self presentViewController:leaderboardNavigationController animated:YES completion:nil];
}
```

### <a name="FASLeaderboardNavigationController"> FASLeaderboardNavigationController </a>
NavigationController, which is a base of leaderboard view.

#### Properties

|Properties|Description|
|------|-----|
|[leaderboardId](#FASLeaderboardNavigationController.leaderboardId)|Leaderboard ID |
|[onlyFriends](#FASLeaderboardNavigationController.onlyFriends)|Select `YES` to only display friends on leaderboard. |
|[animated](#FASLeaderboardNavigationController.animated)|With or without animation when closing he view. |
|[dailySortOptions](#FASLeaderboardNavigationController.todaySortOptions)|Choose sort option for `today` section on leaderboard. |
|[weeklySortOptions](#FASLeaderboardNavigationController.weeklySortOptions)|Choose sort option for `weekly` section on leaderboard. |
|[totalSortOptions](#FASLeaderboardNavigationController.totalSortOptions)|Choose sort option for `total` section on leaderboard. |

##### <a name="FASLeaderboardNavigationController.leaderboardId"> leaderboardId </a>
Specify the ID of the leaderboard you want to display.

@property (nonatomic, copy) NSString *leaderboardId;

##### <a name="FASLeaderboardNavigationController.onlyFriends"> onlyFriends </a>
Select `YES` to only display friends on leaderboard. Default setting is `NO`.

@property (nonatomic, assign) BOOL onlyFriends;

##### <a name="FASLeaderboardNavigationController.animated"> animated </a>
A setting to close the view with or without an animation. Default setting is `YES`.

@property (nonatomic, assign) BOOL animated;

##### <a name="FASLeaderboardNavigationController.todaySortOptions"> dailySortOptions </a>
Select sort option for `today` section on leaderboard. Specify the return value for [dailyWithMinute:hour:](#FASSortOptions.dailyWithMinutehour) under [FASSortOptions](#FASSortOptions).

@property (nonatomic, strong) FASSortOptions *dailySortOptions;

##### <a name="FASLeaderboardNavigationController.weeklySortOptions"> weeklySortOptions </a>
Select sort option for `weekly` section on leaderboard. Specify the return value for [weeklyWithMinute:hour:weekday:](#FASSortOptions.weeklyWithMinutehourweekday) under [FASSortOptions](#FASSortOptions).

@property (nonatomic, strong) FASSortOptions *weeklySortOptions;

##### <a name="FASLeaderboardNavigationController.totalSortOptions"> totalSortOptions </a>
Select sort option for `total` section on leaderboard. Specify the return value for [total](#FASSortOptions.total) under [FASSortOptions](#FASSortOptions).

@property (nonatomic, strong) FASSortOptions *totalSortOptions;

#### Class Method

|Method|Description|
|------|-----|
|[leaderboardNavigationController](#FASLeaderboardNavigationController.leaderboardNavigationController) |Return [FASLeaderboardNavigationController](#FASLeaderboardNavigationController), which is a base of leaderboard view |
|[presentLeaderboardWithTarget:animated:](#FASLeaderboardNavigationController.presentLeaderboardWithTargetanimated) |Display leaderboard view |

##### <a name="FASLeaderboardNavigationController.leaderboardNavigationController"> leaderboardNavigationController </a>
Return [FASLeaderboardNavigationController](#FASLeaderboardNavigationController), which is a base of leaderboard view.

\+ (FASLeaderboardNavigationController *)leaderboardNavigationController;

##### <a name="FASLeaderboardNavigationController.presentLeaderboardWithTargetanimated"> presentLeaderboardWithTarget:animated: </a>
Display the latest leaderboard view.

\+ (void)presentLeaderboardWithTarget:(UIViewController *)target
                             animated:(BOOL)animated;

* Parameters
	* target
		* Select the base ViewController to display the view.
	* animated
		* Yes will transit with animation.

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
You can change layout related to Group View

#### Properties

|Properties|Description|
|------|-----|
|[leaderboardLayoutBlocks](#FASLeaderboardLayout.leaderboardLayoutBlocks)|Block object used to change layout of leaderboard view |

##### <a name="FASLeaderboardLayout.leaderboardLayoutBlocks"> leaderboardLayoutBlocks </a>
Block object used to change layout of leaderboard view

@property (nonatomic, copy) FASLeaderboardViewController *(^leaderboardLayoutBlocks)(FASLeaderboardViewController *leaderboardViewController);

Sample - Changing background color

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
|[sharedInstance](#FASLeaderboardLayout.sharedInstance) |Return the object |

##### <a name="FASLeaderboardLayout.sharedInstance"> sharedInstance </a>
Return the object

\+ (instancetype)sharedInstance;
