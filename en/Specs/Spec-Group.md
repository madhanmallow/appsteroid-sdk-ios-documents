# Group Specifications

last update at 2014/7/7

---

## Introduction

This document is a specification for Group Chat features, creating Group, adding Member and sending Messages.
You can also implement the Group Chat GUI provided by AppSteroid SDK. Check [GroupGetStarted](../GetStarted/GetStarted-GroupChat.md) to see, how to display the GUI on your app.


---

## Classes

|Class|Description|
|------|-----|
|[FASGroup](#FASGroup)|Group model class |
|[FASGroupMember](#FASGroupMember)|GroupMember model class |
|[FASGroupMessage](#FASGroupMessage)|GroupMessage model class |
|[FASSticker](#FASSticker)|Sticker model class for group message |
|[FASStickerSet](#FASStickerSet)|Sticker set model class for group message |

---

## APIs
### <a name="FASGroup"> FASGroup </a>
Group model class, also provides class method to access group feature.

#### Constants

|Constant|Description|
|------|-----|
|[FASGroupCompletionHandler](#FASGroup.FASGroupCompletionHandler)|Block object used when carrying out the process of creating a group, getting group information, updating group information. |
|[FASGroupsCompletionHandler](#FASGroup.FASGroupsCompletionHandler)|Block object used when carrying out the process of getting multiple groups. |


##### <a name="FASGroup.FASGroupCompletionHandler"> (^FASGroupCompletionHandler)(FASGroup *group, NSError *error) </a>
Block object used when carrying out the process of creating a group, getting group information, updating group information.

typedef void (^FASGroupCompletionHandler)(FASGroup *group, NSError *error);

* Parameters
	* group
		* [FASGroup](#FASGroup) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASGroup.FASGroupsCompletionHandler"> (^FASGroupsCompletionHandler)(NSArray *groups, FASPagingMeta *meta, NSError *error) </a>
Block object used when carrying out the process of getting multiple groups.

typedef void (^FASGroupsCompletionHandler)(NSArray *groups, FASPagingMeta *meta, NSError *error);

* Parameters
	* groups
		* Multiple [FASGroup](#FASGroup) are stored in NSArray.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[groupId](#FASGroup.groupId)|Group ID |
|[lastReadMessageId](#FASGroup.lastReadMessageId)|Message ID that was last read |
|[name](#FASGroup.name)|Group Name |
|[membersCount](#FASGroup.membersCount)|Number of members joining the group |
|[subscribed](#FASGroup.subscribed)|Subscribed status |
|[pair](#FASGroup.pair)|Pair Group status |
|[createdAt](#FASGroup.createdAt)|Group creation date and time |
|[updatedAt](#FASGroup.updatedAt)|Group updated date and time |

##### <a name="FASGroup.groupId"> groupId </a>
Group ID

@property (nonatomic, readonly) NSString *groupId;

##### <a name="FASGroup.lastReadMessageId"> lastReadMessageId </a>
Message ID that was last read

@property (nonatomic, readonly) NSString *lastReadMessageId;

##### <a name="FASGroup.name"> name </a>
Group Name

@property (nonatomic, readonly) NSString *name;

##### <a name="FASGroup.membersCount"> membersCount </a>
Number of members joining the group

@property (nonatomic, readonly) NSUInteger membersCount;

##### <a name="FASGroup.subscribed"> subscribed </a>
Subscribed status

@property (nonatomic, readonly) BOOL subscribed;

##### <a name="FASGroup.pair"> pair </a>
Pair Group status

@property (nonatomic, readonly) BOOL pair;

##### <a name="FASGroup.createdAt"> createdAt </a>
Group creation date and time

@property (nonatomic, readonly) NSDate *createdAt;

##### <a name="FASGroup.updatedAt"> updatedAt </a>
Group updated date and time

@property (nonatomic, readonly) NSDate *updatedAt;


#### Class Method

|Method|Description|
|------|-----|
|[createGroupWithCompletion:](#FASGroup.createGroupWithCompletion) |Create a new group |
|[createGroupWithGroupName:completion:](#FASGroup.createGroupWithGroupNamecompletion) |Create a new group with group name |
|[createGroupWithUserIds:completion:](#FASGroup.createGroupWithUserIdscompletion) |Create a new group by selecting user ID array |
|[createGroupWithGroupName:userIds:completion:](#FASGroup.createGroupWithGroupNameuserIdscompletion) |Create a new group by selecting group name and group member. |
|[updateGroupWithGroupId:groupName:completion:](#FASGroup.updateGroupWithGroupIdgroupNamecompletion) |Update the name of the group |
|[deleteGroupWithGroupId:completion:](#FASGroup.deleteGroupWithGroupIdcompletion) |Delete the group |
|[fetchGroupsWithPage:completion:](#FASGroup.fetchGroupsWithPagecompletion) |Get the data of the group |
|[subscribeGroupWithGroupId:completion:](#FASGroup.subscribeGroupWithGroupIdcompletion) |Subscribe to a group |
|[unsubscribeGroupWithGroupId:completion:](#FASGroup.unsubscribeGroupWithGroupIdcompletion) |Unsubscribe from a group |
|[createPairWithUserId:completion:](#FASGroup.createPairWithUserIdcompletion) |Create a new pair group |

##### <a name="FASGroup.createGroupWithCompletion"> createGroupWithCompletion: </a>
Create an empty group.

\+ (void)createGroupWithCompletion:(FASGroupCompletionHandler)completion;

* Parameters
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreationButton:(id)sender
{
    [FASGroup createGroupWithCompletion:^(FASGroup *group, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroup.createGroupWithGroupNamecompletion"> createGroupWithGroupName:completion: </a>
Create a new group with group name

\+ (void)createGroupWithGroupName:(NSString *)groupName
                       completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupName
		* Group Name
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreationButton:(id)sender
{
    [FASGroup createGroupWithGroupName:@"GroupName"
                            completion:^(FASGroup *group, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroup.createGroupWithUserIdscompletion"> createGroupWithUserIds:completion: </a>
Create a new group by selecting user ID array

\+ (void)createGroupWithUserIds:(NSArray *)userIds
                     completion:(FASGroupCompletionHandler)completion;

* Parameters
	* userIds
		* Array with user ID stored.
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreationButton:(id)sender
{
    NSArray *userIds = @[
                        @"xxxxxxxxxxxxxxxxx",
                        @"yyyyyyyyyyyyyyyyy"
                        ];
    [FASGroup createGroupWithUserIds:userIds
                          completion:^(FASGroup *group, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroup.createGroupWithGroupNameuserIdscompletion"> createGroupWithGroupName:userIds:completion: </a>
Create a new group by selecting group name and group member with array.

\+ (void)createGroupWithGroupName:(NSString *)groupName
                          userIds:(NSArray *)userIds
                       completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupName
		* Group name
	* userIds
		* Array with user ID stored.
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreationButton:(id)sender
{
    NSArray *userIds = @[
                        @"xxxxxxxxxxxxxxxxx",
                        @"yyyyyyyyyyyyyyyyy"
                        ];
    [FASGroup createGroupWithGroupName:@"GroupName"
                               userIds:userIds
                            completion:^(FASGroup *group, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroup.updateGroupWithGroupIdgroupNamecompletion"> updateGroupWithGroupId:groupName:completion: </a>
Update the name of the group

\+ (void)updateGroupWithGroupId:(NSString *)groupId
                      groupName:(NSString *)groupName
                     completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* groupName
		* Group name
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedUpdateButton:(id)sender
{
    [FASGroup updateGroupWithGroupId:@"xxxxxxxxxxxxxxxxx"
                           groupName:@"NewGroupName"
                          completion:^(FASGroup *group, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroup.deleteGroupWithGroupIdcompletion"> deleteGroupWithGroupId:completion: </a>
Delete a group

\+ (void)deleteGroupWithGroupId:(NSString *)groupId
                     completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASGroup deleteGroupWithGroupId:@"xxxxxxxxxxxxxxxxx"
                          completion:^(NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroup.fetchGroupsWithPagecompletion"> fetchGroupsWithPage:completion: </a>
Get group list

\+ (void)fetchGroupsWithPage:(NSUInteger)page
                  completion:(FASGroupCompletionHandler)completion;

* Parameters
	* page
		* Page number
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASGroup fetchGroupsWithPage:1
                       completion:^(NSArray *groups, FASPagingMeta *meta, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroup.subscribeGroupWithGroupIdcompletion"> subscribeGroupWithGroupId:completion: </a>
Subscribe to a Group

\+ (void)subscribeGroupWithGroupId:(NSString *)groupId
                        completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedSubscribeButton:(id)sender
{
    [FASGroup subscribeGroupWithGroupId:@"xxxxxxxxxx"
                             completion:^(FASGroup *group, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroup.unsubscribeGroupWithGroupIdcompletion"> unsubscribeGroupWithGroupId:completion: </a>
Unsubscribe from a Group

\+ (void)unsubscribeGroupWithGroupId:(NSString *)groupId
                          completion:(FASGroupCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedUnsubscribeButton:(id)sender
{
    [FASGroup unsubscribeGroupWithGroupId:@"xxxxxxxxxx"
                               completion:^(FASGroup *group, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroup.createPairWithUserIdcompletion"> createPairWithUserId:completion: </a>
Create a pair group. The existing group will be returned when a duplicate pair group was created.

\+ (void)createPairWithUserId:(NSString *)userId
                   completion:(FASGroupCompletionHandler)completion;

* Parameters
	* userId
		* User ID
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroup.h>

	…
	…

- (IBAction)pushedCreatePairButton:(id)sender
{
    [FASGroup createPairWithUserId:@"xxxxxxxxxx"
                        completion:^(FASGroup *group, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

### <a name="FASGroupMember"> FASGroupMember </a>
Group member model class. Also provides class method to access group features.

#### Constants

|Constant|Description|
|------|-----|
|[FASGroupMemberCompletionHandler](#FASGroupMember.FASGroupMemberCompletionHandler)|Block object used when carrying out the process of adding group member. |
|[FASGroupMembersCompletionHandler](#FASGroupMember.FASGroupMembersCompletionHandler)|Block object used when carrying out the process of getting group member. |


##### <a name="FASGroupMember.FASGroupMemberCompletionHandler"> (^FASGroupMemberCompletionHandler)(FASGroupMember *member, NSError *error) </a>
Block object used when carrying out the process of adding group member.

typedef void (^FASGroupMemberCompletionHandler)(FASGroupMember *member, NSError *error);

* Parameters
	* member
		* [FASGroupMember](#FASGroupMember) is stored
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASGroupMember.FASGroupMembersCompletionHandler"> (^FASGroupMembersCompletionHandler)(NSArray *members, FASPagingMeta *meta, NSError *error) </a>
Block object used when carrying out the process of getting group member.

typedef void (^FASGroupMembersCompletionHandler)(NSArray *members, FASPagingMeta *meta, NSError *error);

* Parameters
	* members
		* Multiple [FASGroupMember](#FASGroupMember) are stored in NSArray.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[groupId](#FASGroupMember.groupId)|Group ID |
|[user](#FASGroupMember.user)|User who's in the group |

##### <a name="FASGroupMember.groupId"> groupId </a>
Group ID

@property (nonatomic, readonly) NSString *groupId;

##### <a name="FASGroupMember.user"> user </a>
User who's in the group. [FASUser](#FASUser) Object.

@property (nonatomic, readonly) FASUser *user;

#### Class Method

|Method|Description|
|------|-----|
|[addGroupMemberWithGroupId:userId:completion:](#FASGroupMember.addGroupMemberWithGroupIduserIdcompletion) |Add member to a specific group |
|[deleteGroupMemberWithGroupId:userId:completion:](#FASGroupMember.deleteGroupMemberWithGroupIduserIdcompletion) |Delete member from a specific group |
|[fetchGroupMembersWithGroupId:page:completion:](#FASGroupMember.fetchGroupMembersWithGroupIdpagecompletion) |Get member list from a specific group |

##### <a name="FASGroupMember.addGroupMemberWithGroupIduserIdcompletion"> addGroupMemberWithGroupId:userId:completion: </a>
Add member to a specific group

\+ (void)addGroupMemberWithGroupId:(NSString *)groupId
                            userId:(NSString *)userId
                        completion:(FASGroupMemberCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* userId
		* User ID
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroupMember.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    [FASGroupMember addGroupMemberWithGroupId:@"xxxxxxxxxxxxx"
                                       userId:@"yyyyyyyyyyyyyyy"
                                   completion:(FASGroupMember *member, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroupMember.deleteGroupMemberWithGroupIduserIdcompletion"> deleteGroupMemberWithGroupId:userId:completion: </a>
Delete member from a specific group

\+ (void)deleteGroupMemberWithGroupId:(NSString *)groupId
                               userId:(NSString *)userId
                           completion:(FASGroupMemberCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* userId
		* User ID
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroupMember.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASGroupMember deleteGroupMemberWithGroupId:@"xxxxxxxxxxxxx"
                                          userId:@"yyyyyyyyyyyyyyy"
                                      completion:(NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroupMember.fetchGroupMembersWithGroupIdpagecompletion"> fetchGroupMembersWithGroupId:page:completion: </a>
Get member list from a specific group

\+ (void)fetchGroupMembersWithGroupId:(NSString *)groupId
                                 page:(NSUInteger)page
                           completion:(FASGroupMemberCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* page
		* User ID
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroupMember.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASGroupMember fetchGroupMembersWithGroupId:@"xxxxxxxxxxxxx"
                                            page:1
                                      completion:(NSArray *members, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

### <a name="FASGroupMessage"> FASGroupMessage </a>
Group message model class. Also provides class method to access group message features.

#### Constants

|Constant|Description|
|------|-----|
|[FASGroupMessageCompletionHandler](#FASGroupMessage.FASGroupMessageCompletionHandler)|Block object used when carrying out the process of adding group message and getting group message. |
|[FASGroupMessagesCompletionHandler](#FASGroupMessage.FASGroupMessagesCompletionHandler)|Block object used when carrying out the process of getting group message list. |


##### <a name="FASGroupMessage.FASGroupMessageCompletionHandler"> (^FASGroupMessageCompletionHandler)(FASGroupMessage *message, NSError *error) </a>
Block object used when carrying out the process of adding group message and getting group message.

typedef void (^FASGroupMessageCompletionHandler)(FASGroupMessage *message, NSError *error);

* Parameters
	* message
		* [FASGroupMessage](#FASGroupMessage) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASGroupMessage.FASGroupMessagesCompletionHandler"> (^FASGroupMessagesCompletionHandler)(NSArray *messages, FASPagingMeta *meta, NSError *error) </a>
Block object used when carrying out the process of getting group message list.

typedef void (^FASGroupMessagesCompletionHandler)(NSArray *message, FASPagingMeta *meta, NSError *error);

* Parameters
	* messages
		* Multiple [FASGroupMessage](#FASGroupMessage) are stored in NSArray.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[groupMessageId](#FASGroupMessage.groupMessageId)|Group message ID |
|[groupId](#FASGroupMessage.groupId)|Group ID |
|[text](#FASGroupMessage.text)|Text message |
|[imageUrl](#FASGroupMessage.imageUrl)|URL of image message |
|[imageThumbnailUrl](#FASGroupMessage.imageThumbnailUrl)|URL of thumb nailed image message |
|[createdAt](#FASGroupMessage.createdAt)|Group message creation date and time |
|[updatedAt](#FASGroupMessage.updatedAt)|Group message updated date and time |
|[user](#FASGroupMessage.user)|User who is a sender of the message |
|[video](#FASGroupMessage.video)|Video object |
|[videoStatus](#FASGroupMessage.videoStatus)|Video status |
|[image](#FASGroupMessage.image)|Image message data. Only stored when it is sending |


##### <a name="FASGroupMessage.groupMessageId"> groupMessageId </a>
Group message ID

@property (nonatomic, readonly) NSString *groupMessageId;

##### <a name="FASGroupMessage.groupId"> groupId </a>
Group ID

@property (nonatomic, readonly) NSString *groupId;

##### <a name="FASGroupMessage.text"> text </a>
Text message

@property (nonatomic, readonly) NSString *text;

##### <a name="FASGroupMessage.imageUrl"> imageUrl </a>
URL of image message

@property (nonatomic, readonly) NSString *imageUrl;

##### <a name="FASGroupMessage.imageThumbnailUrl"> imageThumbnailUrl </a>
URL of thumb nailed image message

@property (nonatomic, readonly) NSString *imageThumbnailUrl;

##### <a name="FASGroupMessage.createdAt"> createdAt </a>
Group message creation date and time

@property (nonatomic, readonly) NSDate *createdAt;

##### <a name="FASGroupMessage.updatedAt"> updatedAt </a>
Group message updated date and time

@property (nonatomic, readonly) NSDate *updatedAt;

##### <a name="FASGroupMessage.user"> user </a>
User who send a message.[FASUser](Spec-User.md#FASUser)Object.

@property (nonatomic, readonly) FASUser *user;

##### <a name="FASGroupMessage.video"> video </a>
[FASVideo](Spec-PlayMovie.md#FASVideo)Object.

@property (nonatomic, readonly) FASVideo *video;

##### <a name="FASGroupMessage.videoStatus"> videoStatus </a>
[FASVideoStatus](Spec-PlayMovie.md#FASVideo.FASVideoStatus)の値

@property (nonatomic, readonly) FASVideoStatus videoStatus;

##### <a name="FASGroupMessage.image"> image </a>
Image message data. Only stored when it is sending

@property (nonatomic, readonly) UIImage *image;

#### Class Method

|Method|Description|
|------|-----|
|[addMessageWithGroupId:text:completion:](#FASGroupMessage.addMessageWithGroupIdtextcompletion) |Send text message |
|[addMessageWithGroupId:image:completion:](#FASGroupMessage.addMessageWithGroupIdimagecompletion) |Send image message |
|[addMessageWithGroupId:videoId:completion:](#FASGroupMessage.addMessageWithGroupIdimagecompletion) |Send video message using VideoID |
|[addMessageForInGameWithGroupId:text:completion:](#FASGroupMessage.addMessageForInGameWithGroupIdtextcompletion) |Send text message used for in-game chat |
|[deleteMessageWithGroupId:messageId:completion:](#FASGroupMessage.deleteMessageWithGroupIdmessageIdcompletion) |Delete message of a specified group ID and group message ID |
|[fetchMessageWithGroupId:messageId:completion:](#FASGroupMessage.fetchMessageWithGroupIdmessageIdcompletion) |Get message of a specified group ID and group message ID |
|[fetchMessagesWithGroupId:page:completion:](#FASGroupMessage.fetchMessagesWithGroupIdpagecompletion) |Get message list of a specified group ID |

##### <a name="FASGroupMessage.addMessageWithGroupIdtextcompletion"> addMessageWithGroupId:text:completion: </a>
Send text message

\+ (void)addMessageWithGroupId:(NSString *)groupId
                          text:(NSString *)text
                    completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* text
		* Text message
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    [FASGroupMessage addMessageWithGroupId:@"xxxxxxxxxxxxx"
	                                  text:@"message"
                                completion:(FASGroupMessage *message, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroupMessage.addMessageWithGroupIdimagecompletion"> addMessageWithGroupId:image:completion: </a>
Send image message

\+ (void)addMessageWithGroupId:(NSString *)groupId
                         image:(UIImage *)image
                    completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* image
		* Text message
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    UIImage *image = [UIImage imageNamed:@"image"];
    [FASGroupMessage addMessageWithGroupId:@"xxxxxxxxxxxxx"
	                                 image:image
                                completion:(FASGroupMessage *message, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```
##### <a name="FASGroupMessage.addMessageWithGroupIdvideoIdcompletion"> addMessageWithGroupId:videoId:completion: </a>
Send video message using VideoID

\+ (void)addMessageWithGroupId:(NSString *)groupId
                       videoId:(NSString *)videoId
                    completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* GroupID
	* videoId
		* VideoID
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    UIImage *image = [UIImage imageNamed:@"image"];
    [FASGroupMessage addMessageWithGroupId:@"xxxxxxxxxxxxx"
	                               videoId:@"yyyyyyyyyyyyy"
                                completion:(FASGroupMessage *message, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroupMessage.addMessageForInGameWithGroupIdtextcompletion"> addMessageForInGameWithGroupId:text:completion: </a>
Send text message used for in-game chat

\+ (void)addMessageForInGameWithGroupId:(NSString *)groupId
                                   text:(NSString *)text
                             completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* text
		* Text message
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedAddButton:(id)sender
{
    [FASGroupMessage addMessageForInGameWithGroupId:@"xxxxxxxxxxxxx"
                                               text:@"message"
                                         completion:(FASGroupMessage *message, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroupMessage.deleteMessageWithGroupIdmessageIdcompletion"> deleteMessageWithGroupId:messageId:completion: </a>
Delete message of a specified group ID and group message ID

\+ (void)deleteMessageWithGroupId:(NSString *)groupId
                        messageId:(NSString *)messageId
                       completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* messageId
		* Group message ID
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASGroupMessage deleteMessageWithGroupId:@"xxxxxxxxxxxxx"
                                    messageId:@"yyyyyyyyyyyyyy"
                                   completion:(NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroupMessage.fetchMessageWithGroupIdmessageIdcompletion"> fetchMessageWithGroupId:messageId:completion: </a>
Get message of a specified group ID and group message ID

\+ (void)fetchMessageWithGroupId:(NSString *)groupId
                       messageId:(NSString *)messageId
                      completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* messageId
		* Group message ID
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASGroupMessage fetchMessageWithGroupId:@"xxxxxxxxxxxxx"
                                   messageId:@"yyyyyyyyyyyyyy"
                                  completion:(FASGroupMessage *message, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASGroupMessage.fetchMessagesWithGroupIdpagecompletion"> fetchMessagesWithGroupId:page:completion: </a>
Get message list of a specified group ID

\+ (void)fetchMessagesWithGroupId:(NSString *)groupId
                             page:(NSUInteger)page
                       completion:(FASGroupMessageCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* page
		* Page number
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASGroupMessage.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASGroupMessage fetchMessagesWithGroupId:@"xxxxxxxxxxxxx"
                                         page:1
                                   completion:(NSArray *messages, FASPagingMeta *meta, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

### <a name="FASSticker"> FASSticker </a>
Sticker model Class

#### Constants

|Constant|Description|
|------|-----|
|[FASStickerCompletionHandler](#FASSticker.FASStickerCompletionHandler)|Block object used when carrying out the process of getting sticker. |


##### <a name="FASSticker.FASStickerCompletionHandler"> (^FASStickerCompletionHandler)(FASSticker *sticker, NSError *error) </a>
Block object used when carrying out the process of getting sticker.

typedef void (^FASStickerCompletionHandler)(FASSticker *sticker, NSError *error);

* Parameters
	* sticker
		* [FASSticker](#FASSticker) is stored
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[stickerId](#FASSticker.stickerId)|Sticker ID |
|[stickerSetId](#FASSticker.stickerSetId)|Sticker set ID |
|[stickerName](#FASSticker.stickerName)|Sticker name |
|[url](#FASSticker.url)|Sticker URL |

##### <a name="FASSticker.stickerId"> stickerId </a>
Sticker ID

@property (nonatomic, readonly) NSString *stickerId;

##### <a name="FASSticker.stickerSetId"> stickerSetId </a>
Sticker set ID

@property (nonatomic, readonly) NSString *stickerSetId;

##### <a name="FASSticker.stickerName"> stickerName </a>
Sticker name

@property (nonatomic, readonly) NSString *stickerName;

##### <a name="FASSticker.url"> url </a>
Sticker URL

@property (nonatomic, readonly) NSString *url;

#### Class Method

|Method|Description|
|------|-----|
|[fetchStickerWithId:completion:](#FASSticker.fetchStickerWithIdcompletion) |Get Sticker |

##### <a name="FASSticker.fetchStickerWithIdcompletion"> fetchStickerWithId:completion: </a>
Get Stciker

\+ (void)fetchStickerWithId:(NSString *)stickerId
                completion:(FASStickerCompletionHandler)completion;

* Parameters
	* stickerId
		* Sticker ID
	* completion
		* Block object to be executed when the process is completed.

### <a name="FASStickerSet"> FASStickerSet </a>
Sticker set model class

#### Constants

|Constant|Description|
|------|-----|
|[FASStickerSetCompletionHandler](#FASStickerSet.FASStickerSetCompletionHandler)|Block object used when carrying out the process to get sticker set |
|[FASStickerSetsCompletionHandler](#FASStickerSet.FASStickerSetsCompletionHandler)|Block object used when carrying out the process to get multiple sticker set |

##### <a name="FASStickerSet.FASStickerSetCompletionHandler"> (^FASStickerSetCompletionHandler)(FASStickerSet *stickerSet, NSError *error) </a>
Block object used when carrying out the process to get sticker set

typedef void (^FASStickerSetCompletionHandler)(FASStickerSet *stickerSet, NSError *error);

* Parameters
	* stickerSet
		* [FASStickerSet](#FASStickerSet) is stored
	* error
		* Error detail is stored. It will be nil if there is no error.
		
##### <a name="FASStickerSet.FASStickerSetsCompletionHandler"> (^FASStickerSetsCompletionHandler)(NSArray *stickerSets, FASPagingMeta *meta, NSError *error) </a>
Block object used when carrying out the process to get multiple sticker set

typedef void (^FASStickerSetsCompletionHandler)(NSArray *stickerSets, FASPagingMeta *meta, NSError *error);

* Parameters
	* stickerSet
		* [FASStickerSet](#FASStickerSet) is stored
	* meta
		* meta info can be checked. See [FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta) for detail.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[stickerSetId](#FASStickerSet.stickerSetId)|Sticker set ID |
|[stickerSetName](#FASStickerSet.stickerSetName)|Sticker set name |
|[url](#FASStickerSet.url)|Sticker set image URL |
|[stickers](#FASStickerSet.stickers)|[FASSticker](#FASSticker) groups which are included in sticker set is stored |
|[createdAt](#FASStickerSet.createdAt)|Date sticker set was created |
|[updatedAt](#FASStickerSet.updatedAt)|Date Sticker set was updated |

##### <a name="FASStickerSet.stickerSetId"> stickerSetId </a>
Sticker set ID

@property (nonatomic, readonly) NSString *stickerSetId;

##### <a name="FASStickerSet.stickerSetName"> stickerSetName </a>
Sticker set name

@property (nonatomic, readonly) NSString *stickerSetName;

##### <a name="FASStickerSet.url"> url </a>
Sticker set image URL

@property (nonatomic, readonly) NSString *url;

##### <a name="FASStickerSet.stickers"> stickers </a>
[FASSticker](#FASSticker) groups which are included in sticker set is stored

@property (nonatomic, readonly) NSArray *stickers;

##### <a name="FASStickerSet.createdAt"> createdAt </a>
Date sticker set was created

@property (nonatomic, readonly) NSString *url;

##### <a name="FASStickerSet.createdAt"> updatedAt </a>
Date sticker set was updated

@property (nonatomic, readonly) NSDate *updatedAt;

#### Class Method

|Method|Description|
|------|-----|
|[fetchStickerSetsWithPage:completion:](#FASStickerSet.fetchStickerSetsWithPagecompletion) |Get list of sticker set |
|[fetchStickerSetWithId:completion:](#FASStickerSet.fetchStickerSetWithIdcompletion) |Get sticker set |

##### <a name="FASStickerSet.fetchStickerSetsWithPagecompletion"> fetchStickerSetsWithPage:completion: </a>
Get list of sticker set

\+ (void)fetchStickerSetsWithPage:(NSUInteger)page
                      completion:(FASStickerSetsCompletionHandler)completion;

* Parameters
	* page
		* page number
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASStickerSet.fetchStickerSetWithIdcompletion"> fetchStickerSetWithId:completion: </a>
Get sticker set

\+ (void)fetchStickerSetWithId:(NSString *)stickerSetId
                   completion:(FASStickerSetCompletionHandler)completion;

* Parameters
	* stickerSetId
		* Sticker set ID
	* completion
		* Block object to be executed when the process is completed.