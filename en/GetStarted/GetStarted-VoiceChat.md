# Getting Started - Voice Chat

last update at 2014/10/08

---

- [How to Use Voice Chat API](#HowToUseAPI)
- [How to display Voice Chat View](#HowToDisplayView)
- [Change Layout](#Layout)
- [Important Notes](#ImportantNotes)

---

## <a name="HowToUseAPI"> How to Use Voice Chat API </a>

### Introduction
Download `flamework with voice chat feature` from Fresvii's website.
Check [AppSteroid Get Started](../AppSteroidGetStarted.md) for instructions to implement the flamework.

Also, add `libc++.dylib` to the library like the sample below.

![profile](Images/voicechat_01.png "Profile")

### Using [FASConference](../Specs/Spec-VoiceChat.md)

Voice Chat can be used by using [FASConference](../Specs/Spec-VoiceChat.md).

#### Start Voice Chat

A group needs to be created before starting a voice chat.
Check [GetStarted-GroupChat](GetStarted-GroupChat.md#HowToCreateGroup) for creating a group.
Start a voice chat by selecting a group ID in [setupConferenceWithGroupId:completion:](../Specs/Spec-VoiceChat.md#FASConference.setupConferenceWithGroupIdcompletion) on [FASConference](../Specs/Spec-VoiceChat.md).

Sample

```
- (void)startVoiceChat
{
    NSString *groupId = @"xxxxxxxxxxxxxxxxxxx";
    [FASConference setupConferenceWithGroupId:groupId
                                   completion:^(id response, NSError *error)
     {
         if (error)
         {
             // Error
             return;
         }
         // Start voice chat
     }];
}
```

#### Join Voice Chat

Player can not join a voice chat that hasn't started yet.
Join a voice chat by selecting a group ID in [joinConferenceWithGroupId:completion:](../Specs/Spec-VoiceChat.md#FASConference.joinConferenceWithGroupIdcompletion) on [FASConference](../Specs/Spec-VoiceChat.md).

Sample

```
- (void)joinVoiceChat
{
    NSString *groupId = @"xxxxxxxxxxxxxxxxxxx";
    [FASConference joinConferenceWithGroupId:groupId
                                  completion:^(id response, NSError *error)
    {
        if (error)
        {
            // Error
            return;
        }
        // Join voice chat completed
    }];
}
```

#### Leave Voice Chat

Leave from a voice chat group.
Leave a voice chat by selecting a group ID in [leaveConferenceWithCompletion:](../Specs/Spec-VoiceChat.md#FASConference.leaveConferenceWithCompletion) on  [FASConference](../Specs/Spec-VoiceChat.md).

Sample

```
- (void)leaveVoiceChat
{
    [FASConference leaveConferenceWithCompletion:^(id response, NSError *error)
    {
        if (error)
        {
            // Error
            return;
        }
        // Leave voice chat completed
    }];
}
```

## <a name="HowToDisplayView"> How to display Voice Chat View </a>

Voice chat can be used using the GUI provided by AppSteroid.
Tapping the green call button on the profile screen will start a 1:1 voice chat.

![profile](Images/voicechat_02.png "Profile")

Tap the Call button on the top right menu to start a voice chat in a group chat screen.  4 person in maximum can be in the same voice chat call.

![group](Images/voicechat_03.png "Group")

### <a name="Layout"> Change Layout </a>

You can change layout using [FASVoiceChatLayout](../Specs/Spec-VoiceChat.md#FASVoiceChatLayout) Class.
Check the sample code listed on the Specification as an example changing layout for each view.

- [Voice Chat View](../Specs/Spec-VoiceChat.md#FASVoiceChatLayout.voiceChatayoutBlocks)

## <a name="ImportantNotes"> Important Notes </a>
### Sleep mode and Voice Chat

Going into sleep mode during voice chat session will result loosing communication to that group. However, as long as that particular session exists, any devices that recovers from sleep mode will automatically participate to that group. If the group dose not exist, those device will automatically end the call.

While the host device is in sleep mode during any Voice Chat session, all members in that group will lose connection for the call. If the host recovers from sleep mode, the session will automatically resume.

To avoid sleep mode ending Voice Chat, please turn off sleep mode within your app's settings.