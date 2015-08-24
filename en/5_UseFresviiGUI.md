# Use Fresvii GUI

### Steps

- **Step 1.** Complete the initial setup by referring to [GetStarted](./3_GetStarted.md)
- **Step 2.** Login with an account that have already singed up.
  - **Case 1.** You do not have an account　→　Create a new account and login.
  - **Case 2.** You do have an account　→　Login with your account.
- **Step 3.** Show GUI

### Sample code
```obj-c
#import <AppSteroid/FASAccount.h>
#import <AppSteroid/FASTabBarController.h>

- (IBAction)pushedAppSteroidButton:(id)sender
{
	FASLoginUser *loginUser = [FASAccount currentLoggedInUser];	
    if (!loginUser || !loginUser.isSignedUp)
    {
		[FASAccount signUpUserCompletion:^(FASLoginUser *loginUser, NSError *error)
		{
			if (error)
			{
				NSLog(@"%@", error);
				return;
			}
			[FASTabBarController presentTabBarControllerWithTarget:self
												           animated:YES];
		}];
	}
	else
	{
		[FASTabBarController presentTabBarControllerWithTarget:self
									           	   animated:YES];
	}
}
```