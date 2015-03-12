# Getting Started - Group Chat

last update at 2014/10/07

---

- [Overview](#HowToDisplayGroupChatView)
	- [Simple Setup](#EasyWay)
	- [Setting Parameters](#SettingParameters)
	- [Change Layout](#Layout)
- [Using Group API](#HowToUseAPI)
	- [Creating Croup](#HowToCreateGroup)
	- [Sending Message](#HowToSendMessage)
	- [Adding Member](#HowToAddMember)
- [Using In-Game Chat](#HowToUseInGameChat)
	- [Observing Chat Event](#ObserveEvent)
	- [Sending message to in-game chat](#HowToSendMessageForInGame)

---

## <a name="HowToDisplayGroupChatView"> Overview </a>

This document describes the process of configuring and building the GroupChat GUI into your app.  App users can create a group, send text messages and images in the chat screen, add and delete members to manage their group.


### <a name="EasyWay"> Simple Setup </a>

This is the simplest way to display the GroupChat Screen with the default settings.

Sample

```
#import <AppSteroid/FASGroupNavigationController.h>

	…
	…

- (IBAction)pushedGroupButton:(id)sender
{
    [FASGroupNavigationController presentGroupWithTarget:self
                                                animated:YES];
}
```

### <a name="SettingParameters"> Setting Parameters </a>

You can specifically select a parameter to show the GroupChat screen.

Sample

```
#import <AppSteroid/FASGroupNavigationController.h>

	…
	…

- (IBAction)pushedGroupButton:(id)sender
{
    FASGroupNavigationController *groupNavigationController = [FASGroupNavigationController groupNavigationController];
    groupNavigationController.animated = YES;
    [self presentViewController:groupNavigationController animated:YES completion:nil];
}
```

### <a name="Layout"> Change Layout </a>

You can change layout using [FASGroupLayout](../Specs/Spec-Group.md#FASGroupLayout) Class.
Check the sample code listed on the Specification as an example changing layout for each view.

- [Group List View](../Specs/Spec-Group.md#FASGroupLayout.groupListLayoutBlocks)
- [Group Creation View](../Specs/Spec-Group.md#FASGroupLayout.groupCreateLayoutBlocks)
- [Group Chat View](../Specs/Spec-Group.md#FASGroupLayout.groupChatLayoutBlocks)
- [Group Member View](../Specs/Spec-Group.md#FASGroupLayout.groupMemberLayoutBlocks)
- [Group Member Addition View](../Specs/Spec-Group.md#FASGroupLayout.groupMemberAdditionLayoutBlocks)

---

## <a name="HowToUseAPI"> Using Group API </a>

Create a group, send messages to a group, add or delete members using the Group API.  This API is necessary, if you are considering [Using In-Game Chat](#HowToUseInGameChat) or implementing a unique chat screen into your game.

### <a name="HowToCreateGroup"> Creating Croup </a>


Groups are categorized into two types, Multi Group and Pair Group.  Multi Group can be formed when there are more then two users, and several groups can be formed by the same members.  Pair Group is an 1:1 group which can only be formed by two users, and if the pair group with the same member already exist, the existing one will be returned.



Sample : MultiGroup

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreateMultiGroupButton:(id)sender
{
    NSArray *userIds = @[
                         @"xxxxxxxxxxxxxx",
                         @"yyyyyyyyyyyyyy",
                         @"zzzzzzzzzzzzzz"
                         ];
    [FASGroup createGroupWithUserIds:userIds
                          completion:^(FASGroup *group, NSError *error)
     {
         if (error)
         {
             // Error
             return;
         }

         // Sucess
         // New group will always be created
     }];

}
```

Sample : Pair Group

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreatePairGroupButton:(id)sender
{
    [FASGroup createPairWithUserId:@"xxxxxxxxxxxxxxxxxx"
                        completion:^(FASGroup *group, NSError *error)
     {
         if (error)
         {
             // Error
             return;
         }

         // Sucess
         // If the pair group already exist, the existing one will be returned
     }];

}
```

### <a name="HowToSendMessage"> Sending Message </a>

Send message to the target group ID.
Text messages and Image messages are supported by the current version.

Sample : Text Message

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddTextMessageButton:(id)sender
{
    [FASGroupMessage addMessageWithGroupId:@"xxxxxxxxxxxxxxx"
                                      text:@"text message"
                                completion:^(FASGroupMessage *message, NSError *error)
    {
         if (error)
         {
             // Error
             return;
         }

         // Sucess
     }];
}
```

Sample : Image Message

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddTextMessageButton:(id)sender
{
    UIImage *image = [UIImage imageNamed:@"image"];
    [FASGroupMessage addMessageWithGroupId:@"xxxxxxxxxxxxxxx"
                                     image:image
                                completion:^(FASGroupMessage *message, NSError *error)
    {
         if (error)
         {
             // Error
             return;
         }

         // Sucess
     }];
}
```

### <a name="HowToAddMember"> Adding Member </a>

Add member to the existing multi group.
Error will be returned when adding a member to a pair group.

Sample

```
#import <AppSteroid/FASGroupMember.h>

	…
	…

- (IBAction)pushedAddMemberButton:(id)sender
{
    [FASGroupMember addGroupMemberWithGroupId:@"xxxxxxxxxxxxxxx"
                                       userId:@"yyyyyyyyyyyyyyy"
                                   completion:^(FASGroupMember *member, NSError *error)
    {
        if (error)
        {
            // Error
            return;
        }

        // Sucess
    }];
}
```

---

## <a name="HowToUseInGameChat"> Using In-Game Chat </a>

In-Game Chat is a simple text chat you can use within your app.
Members who joined half way through the conversation can not see the past message, since the text message logs wont be saved.

### <a name="ObserveEvent"> Observing Chat Event </a>
It is required to observe the chat event to receive the notification, and to use this function.
Please check [Observing Push Notification Event](GetStarted-PushNotification.md#ObserveEvent) for setting up observation.
The path and action that should be observed are listed below.

```
path : group/message/in_game
action : created
```

### <a name="HowToSendMessageForInGame"> Sending message to in-game chat </a>

Send a message as a in-game chat to a selected Group.

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedSendButton:(id)sender
{
    [FASGroupMessage addMessageForInGameWithGroupId:@"xxxxxxxxxxxxxxxx"
                                               text:@"text message"
                                         completion:^(FASGroupMessage *message, NSError *error)
    {
        if (error)
        {
            // Error
            return;
        }
        // Success
    }];
}
```
