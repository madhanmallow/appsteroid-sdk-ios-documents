# Matchmaking Specifications

last update at 2015/8/25

---

## Introduction

This document is a specification for function related to Messages.
Classes used to operate direct and push messages send from the Fresvii web console are described on this page.

---

## Classes

|Class|Description|
|------|-----|
|[FASDirectMessage](#FASDirectMessage)|Class to operate direct messages send from Fresvii web console. |
|[FASCustomMessage](#FASCustomMessage)|Class related to a function, sending custom push notification to a specific user. |

---

### <a name="FASDirectMessage"> FASDirectMessage </a>

#### Constants

|Constant|Description|
|------|-----|
|[FASDirectMessageCompletionHandler](#FASDirectMessage.FASDirectMessageCompletionHandler)|Block object used when carrying out the process to receive direct message. |
|[FASDirectMessagesCompletionHandler](#FASDirectMessage.FASDirectMessagesCompletionHandler)|Block object used when carrying out the process to receive multiple direct messages. |

##### <a name="FASDirectMessage.FASDirectMessageCompletionHandler"> FASDirectMessageCompletionHandler </a>
Block object used when carrying out the process to receive direct message

typedef void (^FASDirectMessageCompletionHandler)(FASDirectMessage *directMessage, NSError *error);

* Parameters
	* directMessage
		* [FASDirectMessage](#FASDirectMessage) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASDirectMessage.FASDirectMessagesCompletionHandler"> FASDirectMessagesCompletionHandler </a>
Block object used when carrying out the process to receive multiple direct messages

typedef void (^FASDirectMessagesCompletionHandler)(NSArray *directMessages, FASPagingMeta *meta, NSError *error);

* Parameters
	* directMessages
		* Multiple [FASDirectMessage](#FASDirectMessage) are stored in NSArray.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../7_Spec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[directMessageId](#FASDirectMessage.directMessageId)|Direct message ID |
|[subject](#FASDirectMessage.subject)|Title |
|[text](#FASDirectMessage.text)|Text |
|[createdAt](#FASDirectMessage.createdAt)|Time/date of when the direct message was created |

##### <a name="FASDirectMessage.directMessageId"> directMessageId </a>
Direct message ID

@property (nonatomic, readonly) NSString *directMessageId;

##### <a name="FASDirectMessage.subject"> subject </a>
Title

@property (nonatomic, readonly) NSString *subject;

##### <a name="FASDirectMessage.text"> text </a>
Text

@property (nonatomic, readonly) NSString *text;

##### <a name="FASDirectMessage.createdAt"> createdAt </a>
Time/date of when the direct message was created

@property (nonatomic, readonly) NSDate *createdAt;

#### Class Method

|Method|Description|
|------|-----|
|[fetchDirectMessagesWithPage:completion:](#FASDirectMessage.fetchDirectMessagesWithPage) |Get list of direct messages from a selected page. |
|[fetchDirectMessagesWithPage:onlyUnread:completion:](#FASDirectMessage.fetchDirectMessagesWithPage) |Get list of direct message from a selected page. By setting `unread` to `YES`, you can collect only unread messages.|
|[fetchDirectMessageWithId:completion:](#FASDirectMessage.fetchDirectMessagesWithPage) |Get direct message from a specific id. |

##### <a name="FASDirectMessage.fetchDirectMessagesWithPage"> fetchDirectMessagesWithPage:completion: </a>
Get list of direct messages from a selected page.

\+ (void)fetchDirectMessagesWithPage:(NSUInteger)page
                          completion:(FASDirectMessagesCompletionHandler)completion;

* Parameters
	* page
		* page number
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASDirectMessage.fetchDirectMessagesWithPage"> fetchDirectMessagesWithPage:onlyUnread:completion: </a>
Get list of direct message from a selected page. By setting `unread` to `YES`, you can collect only unread messages.

\+ (void)fetchDirectMessagesWithPage:(NSUInteger)page
                          onlyUnread:(BOOL)unread
                          completion:(FASDirectMessagesCompletionHandler)completion;

* Parameters
	* page
		* page number
	* unread
		* Only collect unread messages if you select `YES`.
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASDirectMessage.fetchDirectMessagesWithPage"> fetchDirectMessageWithId:completion: </a>
Get direct message from a specific id.

\+ (void)fetchDirectMessageWithId:(NSString *)messageId
                       completion:(FASDirectMessageCompletionHandler)completion;

* Parameters
	* messageId
		* ID of direct message
	* completion
		* Block object to be executed when the process is completed.

### <a name="FASCustomMessage"> FASCustomMessage </a>
Class related to a function, sending custom push notification to a specific user.

#### Constants

|Constant|Description|
|------|-----|
|[FASCustomMessageCompletionHandler](#FASCustomMessage.FASCustomMessageCompletionHandler)|Block object used when carrying out the process to send message. |
|[FASCustomMessagesCompletionHandler](#FASCustomMessage.FASCustomMessagesCompletionHandler)|Block object used when carrying out the process to send multiple message. |

##### <a name="FASCustomMessage.FASCustomMessageCompletionHandler"> FASCustomMessageCompletionHandler </a>
Block object used when carrying out the process to send message.

typedef void (^FASCustomMessageCompletionHandler)(FASCustomMessage *message, NSError *error);

* Parameters
	* message
		* [FASCustomMessage](#FASCustomMessage) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASCustomMessage.FASCustomMessagesCompletionHandler"> FASCustomMessagesCompletionHandler </a>
Block object used when carrying out the process to send multiple message.

typedef void (^FASCustomMessagesCompletionHandler)(NSArray *messages, FASPagingMeta *meta, NSError *error);

* Parameters
	* message
		* [FASCustomMessage](#FASCustomMessage) is stored.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../7_Spec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[messageId](#FASCustomMessage.messageId)|Message ID |
|[action](#FASCustomMessage.action)|Action name of message |
|[params](#FASCustomMessage.params)|Parameter of Message |
|[createdAt](#FASCustomMessage.createdAt)|Time and date of when the message was created. |

##### <a name="FASCustomMessage.messageId"> messageId </a>
Message ID

@property (nonatomic, readonly) NSString *messageId;

##### <a name="FASCustomMessage.action"> action </a>
Action name of message

@property (nonatomic, readonly) NSString *action;

##### <a name="FASCustomMessage.params"> params </a>
Parameter of Message

@property (nonatomic, readonly) NSDictionary *params;

##### <a name="FASCustomMessage.createdAt"> createdAt </a>
Time and date of when the message was created.

@property (nonatomic, readonly) NSDate *createdAt;

#### Class Method

|Method|Description|
|------|-----|
|[sendMessageWithChannelName:action:completion:](#FASCustomMessage.sendMessageWithChannelNameactioncompletion) |Send message by selecting channel name and action name. |
|[sendMessageWithChannelName:action:channelParams:params:subject:sound:apnsEnabled:gcmEnabled:completion:](#FASCustomMessage.sendMessageWithChannelNameactionchannelParamsparamssubjectsoundapnsEnabledgcmEnabledcompletion) |Send message by selecting channel name, action name and other parameter. |
|[fetchMessagesWithPage:completion:](#FASCustomMessage.fetchMessagesWithPagecompletion) |Get message list that already been sent. |
|[fetchMessagesWithPage:createdAt:completion:](#FASCustomMessage.fetchMessagesWithPagecreatedAtcompletion) |Get message list that already been sent after a selected date/time. |

##### <a name="FASCustomMessage.sendMessageWithChannelNameactioncompletion"> sendMessageWithChannelName:action:completion: </a>
Send message to both iOS and Android devices by selecting channel name and action name.

\+ (void)sendMessageWithChannelName:(NSString *)channelName
                             action:(NSString *)action
                         completion:(FASCustomMessageCompletionHandler)completion;

* Parameters
	* channelName
		* Channel Name
	* action
		* Action Name of Message
	* completion
		* Block object to be executed when the process is completed.


Sample

```
#import <AppSteroid/FASCustomMessage.h>

	…
	…

- (IBAction)pushedSendButton:(id)sender
{
    [FASCustomMessage sendMessageWithChannelName:@"level"
                                          action:@"created"
                                      completion:^(FASCustomMessage *message, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASCustomMessage.sendMessageWithChannelNameactionchannelParamsparamssubjectsoundapnsEnabledgcmEnabledcompletion"> sendMessageWithChannelName:action:channelParams:params:subject:sound:apnsEnabled:gcmEnabled:completion: </a>
Send message by selecting channel name, action name and other parameter.

\+ (void)sendMessageWithChannelName:(NSString *)channelName
                             action:(NSString *)action
                      channelParams:(id)channelParams
                             params:(id)params
                            subject:(NSString *)subject
                              sound:(NSString *)sound
                        apnsEnabled:(BOOL)apnsEnabled
                         gcmEnabled:(BOOL)gcmEnabled
                         completion:(FASCustomMessageCompletionHandler)completion;

* Parameters
	* channelName
		* Channel Name
	* action
		* Action Name of message
	* channelParams
		* Select `NSArray` type or `NSDictionary` type, so the bind variables specified in query under the channel will be JSON format.
	* params
		* Select `NSArray` type or `NSDictionary` type, so the custom data of push message will be JSON format.
	* subject
		* Subject of push message.
	* sound
		* Sound file of push message. It is silent when nothing is selected.
	* apnsEnabled
		* To decide sending push message to iOS devices or not. `YES` will result sending notification.
	* gcmEnabled
		* To decide sending push message to Android devices or not. `YES` will result sending notification.
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASCustomMessage.h>

	…
	…

- (IBAction)pushedSendButton:(id)sender
{
    [FASCustomMessage sendMessageWithChannelName:@"level"
                                          action:@"created"
                                   channelParams:channelParams
                                          params:params
                                         subject:_levelLabel.text
                                           sound:@"default"
                                     apnsEnabled:YES
                                      gcmEnabled:YES
                                      completion:^(FASCustomMessage *message, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASCustomMessage.fetchMessagesWithPagecompletion"> fetchMessagesWithPage:completion: </a>
Get message list that already been sent.

\+ (void)fetchMessagesWithPage:(NSUInteger)page
                    completion:(FASCustomMessagesCompletionHandler)completion;

* Parameters
	* page
		* Page number
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASCustomMessage.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASCustomMessage fetchMessagesWithPage:1
                                 completion:^(NSArray *messages, FASPagingMeta *meta, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASCustomMessage.fetchMessagesWithPagecreatedAtcompletion"> fetchMessagesWithPage:createdAt:completion: </a>
Get message list that already been sent after a selected date/time.

\+ (void)fetchMessagesWithPage:(NSUInteger)page
                     createdAt:(NSDate *)createdDate
                    completion:(FASCustomMessagesCompletionHandler)completion;

* Parameters
	* page
		* Page number
	* createdAt
		* Date/time when the message was created. Get messages that were created after the selected Date/time.
	* completion
		* Block object to be executed when the process is completed.

Sample

```
#import <AppSteroid/FASCustomMessage.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    // Get list of notification send in the past hour.
    NSDate *date = [[NSDate date] dateByAddingTimeInterval:-3600];
    [FASCustomMessage fetchMessagesWithPage:1
                                  createdAt:date
                                 completion:^(NSArray *messages, FASPagingMeta *meta, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```
