# Getting Started - Leaderboard

last update at 2014/07/08

---

- [How To Use Leaderboard API](#HowToUseAPI)
	- [Submitting Score](#SubmitScore)

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
