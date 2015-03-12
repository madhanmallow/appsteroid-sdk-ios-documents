# Getting Started - Matchmaking

last update at 2014/10/07

---

- [Overview](#HowToDisplayView)
	- [Simple Setup](#EasyWay)
	- [Setting Parameters](#SettingParameters)
	- [Change Layout](#Layout)

---

## <a name="HowToDisplayView"> Overview </a>

This document describes the process of configuring and building the Matchmaking GUI into your app.
When a player send a match join request through the Matchmake UI, AppSteroid will automatically find opponents with the proper conditions. Developers can setup and combine filtering conditions to create an ideal matchmaking system for their games. Delegate method will be called after the matching is completed.

### <a name="EasyWay"> Simple Setup </a>

This is the simplest way to display the Matchmaking with the default settings.

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

Specifically select a parameter to show the Matchmaking.
Setup `matchmakingDelegate` and implement delegate method, `FASMatchmakingNavigationControllerDelegate`, to enable players to receive a notification when a matching was completed.
Check out [FASMatchmakingNavigationController](../Specs/Spec-Matchmaking.md#FASMatchmakingNavigationController) for setting other parameters.

Sample

```
#import <AppSteroid/FASGroupNavigationController.h>

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
    matchmakingNavigationController.minNumberOfPlayers = 2;
    matchmakingNavigationController.matchmakingDelegate = self;
    [self presentViewController:matchmakingNavigationController animated:YES completion:nil];
}

#pragma mark - FASMatchmakingNavigationControllerDelegate method

- (void)FASMatchmakingNavigationController:(FASMatchmakingNavigationController *)FASMatchmakingNavigationController
                      matchingWasCompleted:(FASMatch *)match
{
    [FASMatchmakingNavigationController dismissViewControllerAnimated:NO
                                                           completion:^
    {
        [self performSegueWithIdentifier:@"GameSegue" sender:match];
    }];
}

```

### <a name="Layout"> Change Layout </a>

You can change layout using [FASLeaderboardLayout](../Specs/Spec-Matchmaking.md#FASMatchmakingLayout) Class.
Check the sample code listed on the Specification as an example changing layout for each view.

- [Matchmaking View](../Specs/Spec-Matchmaking.md#FASMatchmakingLayout.matchmakingLayoutBlocks)
