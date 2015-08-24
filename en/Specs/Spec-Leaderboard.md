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
|[FASGameEvent](#FASGameEvent)|Game event model class |
|[FASEventboard](#FASEventboard)|Eventboard model class |


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
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../7_Spec.md#FASPagingMeta) for more information.
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
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../7_Spec.md#FASPagingMeta) for more information.
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
User information. [FASUser](Spec-User.md#FASUser) Object.

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
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../7_Spec.md#FASPagingMeta) for more information.
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
### <a name="FASGameEvent"> FASGameEvent </a>
Game event model class. Game event can be created from Web Console.

#### Constants

|Constant|Description|
|------|-----|
|[FASGameEventStatus](#FASGameEvent.FASGameEventStatus)|Constants of game event state is defined. |
|[FASGameEventCompletionHandler](#FASGameEvent.FASGameEventCompletionHandler)|Block object used when carrying out the process to get game event |
|[FASGameEventsCompletionHandler](#FASGameEvent.FASGameEventsCompletionHandler)|Block object used when carrying out the process to get multiple game events |

##### <a name="FASGameEvent.FASGameEventStatus"> FASGameEventStatus </a>
Constant of game event state is defined. This constant is used to get game event.

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
Not started state of game event.

###### FASGameEventStatusOngoing
Ongoing state of game event.

###### FASGameEventStatusPast
Ended state of game event.

##### <a name="FASGameEvent.FASGameEventCompletionHandler"> (^FASGameEventCompletionHandler)(FASGameEvent *event, NSError *error) </a>
Block object used when carrying out the process to get game event.

typedef void (^FASGameEventCompletionHandler)(FASGameEvent *event, NSError *error);

* Parameters
	* event
		* [FASGameEvent](#FASGameEvent) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASGameEvent.FASGameEventsCompletionHandler"> (^FASRankingCompletionHandler)(NSArray *ranking, NSError *error) </a>
Block object used when carrying out the process to get multiple game events.

typedef void (^FASGameEventsCompletionHandler)(NSArray *events, FASPagingMeta *meta, NSError *error);

* Parameters
	* events
		* Multiple [FASGameEvent](#FASGameEvent) are stored in NSArray.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../7_Spec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[eventId](#FASGameEvent.eventId)|game event ID |
|[eventName](#FASGameEvent.eventName)|Game event name |
|[eventDescription](#FASGameEvent.eventDescription)|Description of game event |
|[imageUrl](#FASGameEvent.imageUrl)|Image URL of game event |
|[webSiteUrl](#FASGameEvent.webSiteUrl)|Web site URL of game event |
|[startAt](#FASGameEvent.startAt)|Game event start date & time |
|[endAt](#FASGameEvent.endAt)|Game event end date & time |
|[createdAt](#FASGameEvent.createdAt)|Game event creation date & time |

##### <a name="FASGameEvent.eventId"> eventId </a>
game event ID.

@property (nonatomic, readonly) NSString *eventId;

##### <a name="FASGameEvent.eventName"> eventName </a>
Game event name.

@property (nonatomic, readonly) NSString *eventName;

##### <a name="FASGameEvent.eventDescription"> eventDescription </a>
Description of game event.

@property (nonatomic, readonly) NSString *eventDescription;

##### <a name="FASGameEvent.imageUrl"> imageUrl </a>
Image URL of game event.

@property (nonatomic, readonly) NSString *imageUrl;

##### <a name="FASGameEvent.webSiteUrl"> webSiteUrl </a>
Web site URL of game event.

@property (nonatomic, readonly) NSString *webSiteUrl;

##### <a name="FASGameEvent.startAt"> startAt </a>
Game event start date & time.

@property (nonatomic, readonly) NSDate *startAt;

##### <a name="FASGameEvent.endAt"> endAt </a>
Game event end date & time.

@property (nonatomic, readonly) NSDate *endAt;

##### <a name="FASGameEvent.createdAt"> createdAt </a>
Game event creation date & time.

@property (nonatomic, readonly) NSDate *createdAt;


#### Class Method

|Method|Description|
|------|-----|
|[fetchGameEventsWithStatus:page:completion:](#FASGameEvent.fetchGameEventsWithStatuspagecompletion) |Get list of game event |
|[fetchGameEventWithEventId:completion:](#FASGameEvent.fetchGameEventWithEventIdcompletion) |Get a game event |

##### <a name="FASGameEvent.fetchGameEventsWithStatuspagecompletion"> fetchGameEventsWithStatus:page:completion: </a>
Get list of game event.

\+ (void)fetchGameEventsWithStatus:(FASGameEventStatus)status
                             page:(NSUInteger)page
                       completion:(FASGameEventsCompletionHandler)completion;

* Parameters
	* status
		* Status of game event. Please refer to [FASGameEventStatus](#FASGameEvent.FASGameEventStatus).
	* page
		* Page number.
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASGameEvent.fetchGameEventWithEventIdcompletion"> fetchGameEventWithEventId:completion: </a>
Get a game event.

\+ (void)fetchGameEventWithEventId:(NSString *)eventId
                       completion:(FASGameEventCompletionHandler)completion;

* Parameters
	* eventId
		* Game event id
	* completion
		* Block object to be executed when the process is completed.

### <a name="FASEventboard"> FASEventboard </a>
Leaderboard model registered to a game event.

#### Constants

|Constant|Description|
|------|-----|
|[FASEventboardCompletionHandler](#FASEventboard.FASEventboardCompletionHandler)|Block object used when carrying out the process to get Eventboard |
|[FASEventboardsCompletionHandler](#FASEventboard.FASEventboardsCompletionHandler)|Block object used when carrying out the process to get multiple Eventboards |

##### <a name="FASEventboard.FASEventboardCompletionHandler"> (^FASEventboardCompletionHandler)(FASEventboard *eventboard, NSError *error) </a>
Block object used when carrying out the process to get Eventboard.

typedef void (^FASEventboardCompletionHandler)(FASEventboard *eventboard, NSError *error);

* Parameters
	* eventboard
		* [FASEventboard](#FASEventboard) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASEventboard.FASEventboardsCompletionHandler"> (^FASEventboardsCompletionHandler)(NSArray *eventboards, FASPagingMeta *meta, NSError *error) </a>
Block object used when carrying out the process to get multiple Eventboards.

typedef void (^FASEventboardsCompletionHandler)(NSArray *eventboards, FASPagingMeta *meta, NSError *error);

* Parameters
	* eventboards
		* Multiple [FASEventboard](#FASEventboard) are stored inNSArray.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../7_Spec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[eventboardId](#FASEventboard.eventboardId)|Eventboard id |
|[leaderboard](#FASEventboard.leaderboard)|Game object registered to a game event |
|[gameEvent](#FASEventboard.gameEvent)|Game event |

##### <a name="FASEventboard.eventboardId"> eventboardId </a>
Eventboard id.

@property (nonatomic, readonly) NSString *eventboardId;

##### <a name="FASEventboard.leaderboard"> leaderboard </a>
[FASLeaderboard](#FASLeaderboard) object registered to a game event.

@property (nonatomic, readonly) FASLeaderboard *leaderboard;

##### <a name="FASEventboard.gameEvent"> gameEvent </a>
[FASGameEvent](#FASGameEvent) object.

@property (nonatomic, readonly) FASGameEvent *gameEvent;

#### Class Method

|Method|Description|
|------|-----|
|[fetchEventboardsWithPage:completion:](#FASEventboard.fetchEventboardsWithPagecompletion) |Get eventboard list |
|[fetchEventboardsWithEventId:page:completion:](#FASEventboard.fetchEventboardsWithEventIdpagecompletion) |Get eventboard list of an event id |
|[fetchEventboardWithEventboardId:completion:](#FASEventboard.fetchEventboardWithEventboardIdcompletion) |Get an eventboard |

##### <a name="FASEventboard.fetchEventboardsWithPagecompletion"> fetchEventboardsWithPage:completion: </a>
Get eventboard list.

\+ (void)fetchEventboardsWithPage:(NSUInteger)page
                      completion:(FASEventboardsCompletionHandler)completion;

* Parameters
	* page
		* Page number.
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASEventboard.fetchEventboardsWithEventIdpagecompletion"> fetchEventboardsWithEventId:page:completion: </a>
Get eventboard list of an event id.

\+ (void)fetchEventboardsWithEventId:(NSString *)eventId
                               page:(NSUInteger)page
                         completion:(FASEventboardsCompletionHandler)completion;

* Parameters
	* eventId
		* Game event id
	* page
		* Page number
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASEventboard.fetchEventboardWithEventboardIdcompletion"> fetchEventboardWithEventboardId:completion: </a>
Get an eventboard.

\+ (void)fetchEventboardWithEventboardId:(NSString *)eventboardId
                             completion:(FASEventboardCompletionHandler)completion;

* Parameters
	* eventboardId
		* Eventboard Id
	* completion
		* Block object to be executed when the process is completed.
