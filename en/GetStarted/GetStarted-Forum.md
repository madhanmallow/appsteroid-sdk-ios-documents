# Getting Started - Forum

last update at 2014/10/07

---

- [Overview](#HowToDisplayForumView)
	- [Simple Setup](#EasyWay)
	- [Setting Parameters](#SettingParameters)
	- [Insert Forum in Tab](#WithTab)
	- [Change Layout](#Layout)

---

## <a name="HowToDisplayForumView"> Overview </a>

This document describes the process of configuring and building the Forum GUI into your app.
In the Forum, all users including the developer can create a thread, post comments and images to communicate with other users.

### <a name="EasyWay"> Simple Setup </a>

This is the simplest way to display the Forum with the default settings.

Sample

```
#import <AppSteroid/FASForumNavigationController.h>

	…
	…

- (IBAction)pushedForumButton:(id)sender
{
    [FASForumNavigationController presentForumWithTarget:self
                                                animated:YES];
}
```

### <a name="SettingParameters"> Setting Parameters </a>

Specifically select a parameter to show the Forum.

Sample

```
#import <AppSteroid/FASForumNavigationController.h>

	…
	…

- (IBAction)pushedForumButton:(id)sender
{
    FASForumNavigationController *forumNavigationController = [FASForumNavigationController forumNavigationController];
    forumNavigationController.animated = YES;
    [self presentViewController:forumNavigationController
                       animated:YES
                     completion:nil];
}
```

### <a name="WithTab"> Insert Forum in Tab </a>

Check out `Show Tab Screen` in [AppSteroidGetStarted](../AppSteroidGetStarted.md) for more information.

### <a name="Layout"> Change Layout </a>

You can change layout using [FASForumLayout](../Specs/Spec-Forum.md#FASForumLayout) Class.
Check the sample code listed on the Specification as an example changing layout for each view.

- [Forum View](../Specs/Spec-Forum.md#FASForumLayout.forumLayoutBlocks)
- [Thread View](../Specs/Spec-Forum.md#FASForumLayout.forumThreadLayoutBlocks)
- [Thread Creation View](../Specs/Spec-Forum.md#FASForumLayout.forumCreateThreadLayoutBlocks)
