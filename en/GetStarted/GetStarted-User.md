# Getting Started - User

last update at 2014/10/7

---

- [Signup And Login](#SignupAndLogin)
- [Profile](#HowToDisplayView)
	- [Simple Setup](#EasyWay)
	- [Setting Parameters](#SettingParameters)
	- [Insert Profile in Tab](#WithTab)
	- [Change Layout](#Layout)

---

## <a name="SignupAndLogin"> Signup And Login </a>

Most of the features provided by AppSteroid require players to signup and login.
The sample below shows how to implement user signup.

Sample

```
#import <AppSteroid/FASAccount.h>

	…
	…

- (IBAction)pushedUserCreateButton:(id)sender
{
	[FASAccount signUpUserWithName:@"UserName"
						 completion:^(FASLoginUser *loginUser, NSError *error)
    {
        if (error)
        {
            // Error
            NSLog(@"%@", error);
            return;
        }
    }];
}
```

After creating a user, login can be done like the following sample.

Sample

```
#import <AppSteroid/FASAccount.h>

	…
	…

- (IBAction)pushedLoginButton:(id)sender
{
    [FASAccount loginUserWithCompletion:^(FASLoginUser *loginUser, NSError *error)
    {
        if (error)
        {
            // Error
            NSLog(@"%@", error);
            return;
        }
    }];
}
```

Login status can be checked, using the following functions.

```
// If a user already exist or not
if ([FASAccount currentLoggedInUser].isSignedUp)
{
    // User already exist
}

// If a user is logged in or logged out
if ([FASAccount currentLoggedInUser].isExpiredSession)
{
    // User is logged out
}
```

## <a name="HowToDisplayView"> Profile </a>

On profile, players can check/add/delete friends, start a chat or a call, and edit information on their own screen.

### <a name="EasyWay"> Simple Setup </a>

Simplest way to display the Profile with the default settings.

Sample

```
#import <AppSteroid/FASProfileNavigationController.h>

	…
	…

- (IBAction)pushedProfileButton:(id)sender
{
    [FASProfileNavigationController presentProfileWithTarget:self
                                                    animated:YES];
}
```

### <a name="SettingParameters"> Setting Parameters </a>

Specifically select a parameter to show the Profile.
Select a User ID on `userId` to show that users profile. If there wasn't any ID selected, it will show the users profile who is currently logged on.

Sample

```
#import <AppSteroid/FASProfileNavigationController.h>

	…
	…

- (IBAction)pushedProfileButton:(id)sender
{
    FASProfileNavigationController *profileNavigationController = [FASProfileNavigationController profileNavigationController];
    profileNavigationController.animated = YES;
    profileNavigationController.userId = @"xxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
    [self presentViewController:profileNavigationController animated:YES completion:nil];
}
```

### <a name="WithTab"> Insert Profile in Tab </a>

Check out `Show Tab Screen` on [AppSteroidGetStarted](../AppSteroidGetStarted.md) for more information.

### <a name="Layout"> Change Layout </a>

You can change layout using [FASProfileLayout](../Specs/Spec-User.md#FASProfileLayout) Class.
Check the sample code listed on the Specification as an example changing layout for each view.

- [Profile View](../Specs/Spec-User.md#FASProfileLayout.profileLayoutBlocks)
- [Profile Editor View](../Specs/Spec-User.md#FASProfileLayout.editProfileLayoutBlocks)
- [Friend List View](../Specs/Spec-User.md#FASProfileLayout.friendListLayoutBlocks)
- [Friend Request View](../Specs/Spec-User.md#FASProfileLayout.friendRequestLayoutBlocks)
