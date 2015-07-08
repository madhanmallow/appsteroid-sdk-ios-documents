# Getting Started - Leaderboard

last update at 2015/7/8

---

- [リーダーボードAPIの利用](#HowToUseAPI)
	- [スコアの登録](#SubmitScore)

---

## <a name="HowToUseAPI"> リーダーボードAPIの利用 </a>

### <a name="SubmitScore"> スコアの登録 </a>

[FASScore](../Specs/Spec-Leaderboard.md#FASScore)の[submitScoreWithLeaderboardId:value:completion:](../Specs/Spec-Leaderboard.md#FASScore.submitScoreWithLeaderboardIdvaluecompletion)を利用して対象のリーダーボードに対してスコアを登録します。

Sample
0〜1000のランダムな値をスコアとして登録する

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
