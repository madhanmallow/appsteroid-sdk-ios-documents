# Getting Started - Matchmaking

last update at 2014/10/07

---

- [Overview](#Abstruct)
- [Show matchmaking page](#HowToDisplayView)
	- [Simple Setup](#EasyWay)
	- [Setting Parameters](#SettingParameters)
	- [Create Match Conditions](#Segment)
	- [Change Layout](#Layout)
- [Handle Match Completion](#HandlingMatchCompletion)
- [Support turn based game](#GameContext)
  - [Add and delete Event](#GameContextEvent)
  - [Update Game Context](#GameContextUpdate)

---

## <a name="Abstruct"> Overview </a>
- Matchmaking is for finding opponents within the game.
- There are 3 different ways to join a matchmake.

  - **Create a Request:**
  Create a request by specifying conditions for the match. A new match object will be generated when a player select a specific user to invite.  If a player did not specify a user to invite and found a existing match that coincide the specified conditions, it will automatically join to that Match. If there weren't any matches that coincide the conditions, it will generate a new match object and wait for other players to join.

  - **Accept Invitation:**
  Join a match by accepting a matchmake request invitation. It will mainly be used between friends.
    Use the invitation ID (=request ID) to process canceling the invitation once after accepting it.

  - **Join a Match:**
  Select a match ID to join a specific Match.
    If all the players participating to that existing match cancels it, the player can not join to the match.

- After the matchmake was approved, data listed below will be generated for every match.

  - **Group for Matchmake**
  Used for in-game chat and voice chat.

  - **Game Context**
  Used as a shared data for turn basis game.  Check [Support turn based game](#GameContext) for more detail.

## <a name="HowToDisplayView"> Show matchmaking page </a>

This document describes the process of configuring and building the Matchmaking GUI into your app.
When a player send a match join request through the Matchmake UI, AppSteroid will automatically find opponents with the proper conditions. Developers can setup and combine filtering conditions to create an ideal matchmaking system for their games. Delegate method will be called after the matching is completed.

### <a name="EasyWay"> Simple Setup </a>

This is the most simple way to display the Matchmaking with the default settings.

Sample

```

#import <AppSteroid/FASGroupNavigationController.h>

	…
	…

- (IBAction)pushedMatchmakingButton:(id)sender
{
    [FASGroupNavigationController presentMatchmakingWithTarget:self
                                                      animated:YES];
}
```

### <a name="SettingParameters"> Setting Parameters </a>

Select a parameter and show matchmaking page.  
Check the [FASMatchmakingViewController](../Specs/Spec-Matchmaking.md#FASMatchmakingNavigationController) document for available parameter types.

Sample

```
 #import <AppSteroid/FASMatchmakingNavigationController.h>
 
 @interface ViewController ()
 <
     FASMatchmakingNavigationControllerDelegate
 >
 
 @end
 
 	…
 	…
 
 - (IBAction)pushedMatchmakingButton:(id)sender
 {
     FASMatchmakingNavigationController *matchmakingNavigationController = [FASMatchmakingNavigationController matchmakingNavigationController];
    FASMatchmakingViewController *matchmakingViewController = matchmakingNavigationController.matchmakingViewController;
    matchmakingViewController.minNumberOfPlayers = 3;
    matchmakingViewController.maxNumberOfPlayers = 6;
     [self presentViewController:matchmakingNavigationController animated:YES completion:nil];
 }
  ```

### <a name="Segment"> Create Match Conditions </a>

We allow developers to create an unique match condition, like matching users in the same region or users with the same level.  Parameters to use for this function are described in [FASMatchmakingViewController#segment](../Specs/Spec-Matchmaking.md#FASMatchmakingNavigationController.segment).  
Users with the same string name in `segment` can be matched. If you want to add a filter to match users with the same region;

```
matchmakingViewController.segment = @"Japan";
```

will simply work. This will only match users who has a `segment`, `Japan`, in their condition.  With this example, users with `USA` in their `segment` will never be matched.

### <a name="Layout"> Change Layout </a>

You can change layout using [FASLeaderboardLayout](../Specs/Spec-Matchmaking.md#FASMatchmakingLayout) Class.
Check the sample code listed on the Specification as an example changing layout for each view.

- [Matchmaking View](../Specs/Spec-Matchmaking.md#FASMatchmakingLayout.matchmakingLayoutBlocks)

## <a name="HandlingMatchCompletion"> Handle Match Completion </a>
To transit to game screen from matchmaking view after the match completion, additional coding is required by the developer.  
First, register the notification by using `NSNotificationCenter` to setup ability to receive match completion. We recommend to add code in `- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions`. This is to receive match completion when launching the app from match invitation.

```
#import <AppSteroid/FASMatchmakingViewController.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
	// Register match completion event
	[[NSNotificationCenter defaultCenter] addObserver:self
	                                         selector:@selector(matchmakingCompleted:)
	                                             name:kFASMatchmakingCompleted
	                                           object:nil];
	                                           
}

#pragma mark - FASMatchmakigViewController Notification methods

- (void)matchmakingCompleted:(NSNotification *)notification
{
	// Called on match completion
}

```

## <a name="GameContext"> Support turn based game </a>
[FASGameContext](../Specs/Spec-Matchmaking.md#FASGameContext) must be used to start a turn based game after match completion.  
 **Game Context** is an object ([FASGameContext](../Specs/Spec-Matchmaking.md#FASGameContext)) that can be send to participants (opponents) in a match.

### <a name="GameContextEvent"> Add and delete Event </a>
 Notification of path:`match_making/context`action:`created` will be sent to the opponent when sending the game context. Please check the following sample code, or refer to the [GetStarted-PushNotification](./GetStarted-PushNotification.md#ObserveEvent) to see steps to register game context.

1. Add event to receive context.
2. Delete the event when leaving the view.
3. Get game context
4. Process receiving the game context.

```
#import <AppSteroid/FASGameContext.h>
#import <AppSteroid/FASEvent.h>

@implementation TurnBasedGameViewController
{
   FASObserver *_observer;
}

- (void)viewWillAppear:(BOOL)animated
{
   [super viewWillAppear:animated];
   
   // 1. Register event of receiving context.
   _observer = [FASEvent observeEventWithPath:@"match_making/context"
                                       action:@"created"
                                 eventHandler:^(NSDictionary *params)
   {
       [self _fetchGameContext];
   }];
}

- (void)viewDidDisappear:(BOOL)animated
 {
     [super viewDidDisappear:animated];
     
     // 2. Delete the event when leaving the view.
     [FASEvent unobserve:_observer];
 }
 
- (void)_fetchGameContext
{
	// 3. Get game context
   [FASGameContext fetchGameContextWithMatchId:@"match_id"
                                    completion:^(FASGameContext *gameContext, NSError *error)
  {
        // 4. Process the receive of game context.
    }];
}

```

### <a name="GameContextUpdate"> Update Game Context </a>
Update the game context when the turn is over. A push notice can be sent to opponents by updating the game context.

1. Update game context.
2. Process completion of updating game context.

```
- (IBAction)pushedSubmitButton:(id)sender
{
	// 1. Update game context.
	[FASGameContext updateGameContextWithMatchId:@"match_id"
	                                       value:@{@"score" : @"100"}
                                     completion:^(FASGameContext *gameContext, NSError *error)
       {
            // 2. Process completion of updating game context.
        }];
   }
}
```