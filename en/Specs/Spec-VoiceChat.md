# Voice Chat Specifications

last update at 2014/10/24

---

## Introduction

Specification for functions on Voice Chat.
Functions to create/join conference, which are required for Voice Chat is provided.
Please check [VoiceChatGetStarted](../GetStarted/GetStarted-VoiceChat.md) for implementation.

---

## Classes

|Class|Description|
|------|-----|
|[FASConference](#FASConference)|Voice Chat model class |
|[FASConferenceParticipant](#FASConferenceParticipant)|Conference Participant model class |
|[FASVoiceChatLayout](#FASVoiceChatLayout)|Class to change layout of voice chat view |

---

## APIs
### <a name="FASConference"> FASConference </a>
Voice Chat model class.
You can create a conference group for voice chat or participate to a existing conference using this Class.

#### Constants

|Constant|Description|
|------|-----|
|[FASConferenceIncomingBehavior](#FASConference.FASConferenceIncomingBehavior)|Behavior of when receiving an incoming voice chat call. |
|[FASConferenceViewVisibility](#FASConference.FASConferenceViewVisibility)|Show call screen when receiving an incoming voice chat call. |
|[FASConferenceIncomingHandler](#FASConference.FASConferenceIncomingHandler)|Black object called when receiving a call.|
|[FASParticipantsCompletionHandler](#FASConference.FASParticipantsCompletionHandler)|Block object used when carrying out the process to get participants for voice chat. |

##### <a name="FASConference.FASConferenceIncomingBehavior"> FASConferenceIncomingBehavior </a>
Behavior of when receiving an incoming voice chat call.

```obj-c
typedef NS_ENUM(NSInteger, FASConferenceIncomingBehavior)
{
    FASConferenceIncomingBehaviorAsk        = 0,
    FASConferenceIncomingBehaviorAutoAccept = 1,
    FASConferenceIncomingBehaviorCallback   = 2
};
```

##### <a name="FASConference.FASConferenceViewVisibility"> FASConferenceViewVisibility </a>
Show call screen when receiving an incoming voice chat call. Default is ```OnlyInFAS```. Select```Never``` or ```OnlyInFAS``` to have a call on the game screen.

 ```obj-c
 typedef NS_ENUM(NSInteger, FASConferenceIncomingBehavior)
 {
     FASConferenceViewVisibilityNever = -1,
     FASConferenceViewVisibilityOnlyInFAS,
     FASConferenceViewVisibilityAnyTime,
 };
 ```

 - Never: Do not show call screen
 - OnlyInFAS: Only show call screen within the GUI provided by the SDK
 - AnyTime: Always show call screen

##### <a name="FASConference.FASConferenceIncomingHandler"> (^FASConferenceIncomingHandler)(NSString *groupId) </a>
Black object called when receiving a call. Accept the call by returning YES.

typedef BOOL (^FASConferenceIncomingHandler)(NSString *groupId);

##### <a name="FASConference.FASParticipantsCompletionHandler"> (^FASParticipantsCompletionHandler)(NSString *groupId) </a>
Block object used when carrying out the process to get participants for voice chat.

typedef void (^FASParticipantsCompletionHandler)(NSArray *participants, NSError *error);


#### Properties

|Properties|Description|
|------|-----|
|[callStates](#FASConference.callStates)| |

##### <a name="FASConference.callStates"> callStates </a>

@property (readonly) NSDictionary *callStates;

#### Class Methods

|Method|Description|
|------|-----|
|[sharedInstance](#FASConference.sharedInstance) |Return singleton object of `FASConference` Class. |
|[hostConferenceWithGroupId:completion:](#FASConference.hostConferenceWithGroupIdcompletion) |Create a conference. |
|[fetchConferenceWithGroupId:completion:](#FASConference.fetchConferenceWithGroupIdcompletion) |Get the current conference. |
|[fetchConferenceParticipantsWithGroupId:completion:](#FASConference.fetchConferenceParticipantsWithGroupIdcompletion) |Get participants in the conference. |
|[joinConferenceWithGroupId:completion:](#FASConference.joinConferenceWithGroupIdcompletion) |Participate to conference. |
|[setMicrophoneVolume:speakerVolume:completion:](#FASConference.setMicrophoneVolumespeakerVolumecompletion) |Set mic volume and speaker volume. |

##### <a name="FASConference.sharedInstance"> sharedInstance </a>
Return singleton object of `FASConference` Class.

\+ (instancetype)sharedInstance;

##### <a name="FASConference.hostConferenceWithGroupIdcompletion"> hostConferenceWithGroupId:completion: </a>
Create a conference.

\+ (void)hostConferenceWithGroupId:(NSString *)groupId
                         completion:(FASResponseCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASConference.fetchConferenceWithGroupIdcompletion"> fetchConferenceWithGroupId:completion: </a>
Get current conference.

\+ (void)fetchConferenceWithGroupId:(NSString *)groupId
                         completion:(FASResponseCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASConference.fetchConferenceParticipantsWithGroupIdcompletion"> fetchConferenceParticipantsWithGroupId:completion: </a>
Get participants in the conference.

\+ (void)fetchConferenceParticipantsWithGroupId:(NSString *)groupId
                                    completion:(FASParticipantsCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* completion
		* Get participants in the conference.

##### <a name="FASConference.joinConferenceWithGroupIdcompletion"> joinConferenceWithGroupId:completion: </a>
Participate to conference.

\+ (void)joinConferenceWithGroupId:(NSString *)groupId
                        completion:(FASResponseCompletionHandler)completion;

* Parameters
	* groupId
		* Group ID
	* completion
		* Get participants in the conference.

##### <a name="FASConference.setMicrophoneVolumespeakerVolumecompletion"> setMicrophoneVolume:speakerVolume:completion: </a>
Set mic volume and speaker volume.
This is a function to adjust the volume on the device it self using the SDK.

\+ (void)setMicrophoneVolume:(float)microphoneVolume
               speakerVolume:(float)speakerVolume
                  completion:(FASResponseCompletionHandler)completion;

* Parameters
	* microphoneVolume
		* Specify a value for mic volume.
	* speakerVolume
		* Specify a value for speaker volume.
	* completion
		* Block object to be executed when the process is completed.

#### Instance Methods

|Method|Description|
|------|-----|
|[humanizedRole](#FASConference.humanizedRole) |Get role name for the current conference. |
|[addDelegate:](#FASConference.addDelegate) |Specify a delegate to receive notification about status changes of conference. |
|[removeDelegate:](#FASConference.removeDelegate) |Delete delegate. |
|[setIncomingHandler:](#FASConference.setIncomingHandler) |Block object to receive notification when there is a incoming call. |
|[currentGroup](#FASConference.currentGroup) |Get current group ID. |
|[isMute](#FASConference.isMute) |Get whether it is mute or not. |
|[muteWithCompletion:](#FASConference.muteWithCompletion) |Mute |
|[unmuteWithCompletion:](#FASConference.unmuteWithCompletion) |Unmute |
|[leaveWithCompletion:](#FASConference.leaveWithCompletion) |Leave conference. |
|[elapsedTime](#FASConference.elapsedTime) |Get duration time of the conference. |

##### <a name="FASConference.humanizedRole"> humanizedRole </a>
Get role name for the current conference.

\- (NSString *)humanizedRole;

##### <a name="FASConference.addDelegate"> addDelegate: </a>
Specify a delegate to receive notification about status changes of conference.

\- (void)addDelegate:(id<FASConferenceDelegate>)delegate;

* Parameters
	* delegate
		* Specify a object.

##### <a name="FASConference.removeDelegate"> removeDelegate: </a>
Delete delegate.

\- (void)removeDelegate:(id<FASConferenceDelegate>)delegate;

* Parameters
	* delegate
		* Specify a object

##### <a name="FASConference.setIncomingHandler"> setIncomingHandler: </a>
Block object to receive notification when there is a incoming call.

\- (void)setIncomingHandler:(FASConferenceIncomingHandler)handler;

* Parameters
	* handler
		* Specify a `FASConferenceIncomingHandler`.

##### <a name="FASConference.currentGroup"> currentGroup </a>
Get current group ID.

\-(NSString *)currentGroup;

##### <a name="FASConference.isMute"> isMute </a>
Get whether it is mute or not.

\-(BOOL)isMute;

##### <a name="FASConference.muteWithCompletion"> muteWithCompletion: </a>
Mute

\+ (void)muteWithCompletion:(FASResponseCompletionHandler)completion;

* Parameters
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASConference.unmuteWithCompletion"> unmuteWithCompletion: </a>
Unmute

\+ (void)unmuteWithCompletion:(FASResponseCompletionHandler)completion;

* Parameters
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASConference.leaveWithCompletion"> leaveWithCompletion:completion </a>
Leave conference

\+ (void)leaveWithCompletion:(FASResponseCompletionHandler)completion;

* Parameters
	* completion
		* Block object to be executed when the process is completed.

##### <a name="FASConference.elapsedTime"> elapsedTime </a>
Get duration time of the conference.

\-(NSTimeInterval)elapsedTime;

#### <a name="FASConferenceDelegate"> FASConferenceDelegate </a>
A delegate method to be called when there was status change on the observing [FASConference](#FASConference) object.

|Method|Description|
|------|-----|
|[didConferenceStart:](#FASConferenceDelegate.didConferenceStart) |It is called when the conference begins. |
|[didConferenceFinish](#FASConferenceDelegate.didConferenceFinish) |It is called when the conference ends. |
|[didCallStateChange:](#FASConferenceDelegate.didCallStateChange) |It is called when changes made in participants in the conference. |

##### <a name="FASConferenceDelegate.didConferenceStart"> didConferenceStart: </a>
It is called when the conference begins.

\- (void)didConferenceStart:(NSString *)groupId;

* Parameters
	* groupId
		* Group ID

##### <a name="FASConferenceDelegate.didConferenceFinish"> didConferenceFinish </a>
It is called when the conference ends.

\- (void)didConferenceFinish;

##### <a name="FASConferenceDelegate.didCallStateChange"> didCallStateChange: </a>
It is called when changes made in participants in the conference.

\- (void)didCallStateChange:(NSArray *)participants;

* Parameters
	* participants
		* Participants list

### <a name="FASConferenceParticipant"> FASConferenceParticipant </a>
Conference participants model class

#### Properties

|Method|Description|
|------|-----|
|[user](#FASConferenceParticipant.user) |User who is participating to the conference. |

##### <a name="FASConferenceParticipant.user"> user </a>
User who is participating to the conference is stored as [FASUser](../Specs/Spec-User.md#FASUser) object.

@property (nonatomic, readonly) FASUser *user;

#### Instance Methods

|Method|Description|
|------|-----|
|[humanizedCallStatus](#FASConferenceParticipant.humanizedCallStatus) |Get calling status of participants. |

##### <a name="FASConferenceParticipant.humanizedCallStatus"> humanizedCallStatus: </a>
Get calling status of participants.

-(NSString *)humanizedCallStatus;


### <a name="FASVoiceChatLayout"> FASVoiceChatLayout </a>
You can change layout related to voice chat.

#### Properties

|Properties|Description|
|------|-----|
|[voiceChatayoutBlocks](#FASVoiceChatLayout.voiceChatayoutBlocks)|Block object used to change layout of voice chat view |

##### <a name="FASVoiceChatLayout.voiceChatayoutBlocks"> voiceChatayoutBlocks </a>
Block object used to change layout of voice chat view

@property (nonatomic, copy) FASVoiceChatViewController *(^voiceChatayoutBlocks)(FASVoiceChatViewController *voiceChatViewController);

Sample - Changing background color

```
    [FASVoiceChatLayout sharedInstance].voiceChatayoutBlocks = ^FASVoiceChatViewController *(FASVoiceChatViewController *voiceChatViewController)
    {
        voiceChatViewController.view.backgroundColor = [UIColor whiteColor];
        voiceChatViewController.endLabel.textColor = [UIColor blackColor];
        voiceChatViewController.messageLabel.textColor = [UIColor blackColor];
        voiceChatViewController.timeLabel.textColor = [UIColor blackColor];
        if ([voiceChatViewController.navigationController.navigationBar respondsToSelector:@selector(barTintColor)])
        {
            voiceChatViewController.navigationController.navigationBar.tintColor = [UIColor greenColor];
            voiceChatViewController.navigationController.navigationBar.barTintColor = [UIColor whiteColor];
        }
        voiceChatViewController.navigationController.navigationBar.barStyle = UIBarStyleDefault;
        voiceChatViewController.navigationController.navigationBar.titleTextAttributes = @{NSForegroundColorAttributeName: [UIColor blackColor]};
        return voiceChatViewController;
    };
```

#### Class Method

|Method|Description|
|------|-----|
|[sharedInstance](#FASVoiceChatLayout.sharedInstance) |Return the object |

##### <a name="FASVoiceChatLayout.sharedInstance"> sharedInstance </a>
Return the object

\+ (instancetype)sharedInstance;
