# Getting Started - Leaderboard

last update at 2014/10/07

---

- [Overview](#HowToDisplayView)
	- [Simple Setup](#EasyWay)
	- [Setting Parameters](#SettingParameters)
	- [Insert Leaderboard in Tab](#WithTab)
	- [Change Layout](#Layout)
- [How To Use Leaderboard API](#HowToUseAPI)
	- [Submitting Score](#SubmitScore)

---

## <a name="HowToDisplayView"> Overview </a>

This document describes the process of configuring and building the Leaderboard GUI into your app.  Players can browse the score and ranking on the leaderboard, which can be created on the Fresvii web console.



### <a name="EasyWay"> Simple Setup </a>

This is the simplest way to display the Leaderboard with the default settings.
Only the latest leaderboard will be shown on the screen.

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

### <a name="SettingParameters"> Setting Parameters </a>

Specifically select a parameter to show the Leaderboard.
Leaderboard ID can be found on the Fresvii web console.

Sample

```
#import <AppSteroid/FASLeaderboardNavigationController.h>

	…
	…

- (IBAction)pushedLeaderboardButton:(id)sender
{
    NSString *leaderboardId = @"xxxxxxxxxxxxxxxxxxxxxxxx";
    FASLeaderboardNavigationController *leaderboardNavigationController = [FASLeaderboardNavigationController leaderboardNavigationController];
    leaderboardNavigationController.leaderboardId = leaderboardId;
    leaderboardNavigationController.onlyFriends = NO;

    [self presentViewController:leaderboardNavigationController
                       animated:YES
                     completion:nil];
}
```

### <a name="WithTab"> Insert Leaderboard in Tab </a>

Check out `Show Tab Screen` in [AppSteroidGetStarted](../AppSteroidGetStarted.md) for more information.

### <a name="Layout"> Change Layout </a>

You can change layout using [FASLeaderboardLayout](../Specs/Spec-Leaderboard.md#FASLeaderboardLayout) Class.
Check the sample code listed on the Specification as an example changing layout for each view.

- [Leaderboard View](../Specs/Spec-Leaderboard.md#FASLeaderboardLayout.leaderboardLayoutBlocks)

---

## <a name="HowToUseAPI"> How To Use Leaderboard API </a>

### <a name="SubmitScore"> Submitting Score </a>

Use [submitScoreWithLeaderboardId:value:completion:](../Specs/Spec-Leaderboard.md#FASScore.submitScoreWithLeaderboardIdvaluecompletion) in [FASScore](../Specs/Spec-Leaderboard.md#FASScore) to submit score to the target leaderboard.

Sample
Submit a random value, 0 to 1000, as a score.

```
#import <AppSteroid/FASScore.h>

	…
	…

- (IBAction)pushedSubmitButton:(id)sender
{
    NSString *leaderboardId = @"xxxxxxxxxxxxxxxxxx";
    int score = arc4random() % 1000;
    [FASScore submitScoreWithLeaderboardId:leaderboardId
                                     value:score
                                completion:nil];
}
```
