# Getting Started - User

last update at 2014/10/7

---

- [Signup And Login](#SignupAndLogin)

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