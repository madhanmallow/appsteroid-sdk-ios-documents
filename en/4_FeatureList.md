# Features

----------

- [AppSteroid Feature Introduction](#Features)
	- [Social Feature Service](#SocialFeatures)
		- [Game Forum](#GameForum)
		- [User Profile](#UserProfile)
		- [Friend Management](#FriendManagement)
		- [Group Message](#GroupMessage)
		- [In Game Chat](#InGameChat)
		- [Voice Chat/In Game Voice Chat](#VoiceChat)
		- [Play Video](#PlayVideo)
		- [Push Notification](#PushNotificationForSetting)
	- [App Promotion Service](#PromotionService)
		- [Official Forum](#OfficialForum)
		- [Push Notification](#PushNotificationForPromotion)
	- [Game Management Support Service](#SupportService)
		- [Leaderboard](#Leaderboard)
		- [Matchmake](#Matchmaking)
		- [Customer Support](#CSR)
		- [Turn Based Game Support](#Turn-BasedGame)
		- [3D Avatar Service](#3DAvator)
	- [Basic Backend as a Service](#BackendService)
		- [User Authentication](#UserCertification)
		- [Social Integration](#SocialIntegration)
		- [Cloud Storage](#CloudStrage)
		- [Game Data Migration](#DataTransfer)
	- [WEB Console Service](#WebConsole)
- [How to Implement AppSteroid SDK](#Install)

---

## <a name="Features">AppSteroid Feature Introduction</a>
To use these features in your application, you need to implement AppSteroid SDK in your App. Check [How to Implement AppSteroid SDK](#Install).

### <a name="SocialFeatures">Social Feature Service</a>
Features to boost user retention and engagement. We have a result of big raise in user retention with our clients App. Making mobile game social is our main field.

#### <a name="GameForum">- Game Forum</a>
A space for app user to freely share information with the community. User can post text, images and share their play-videos on the thread.  


- What can be done on the web console
	- Create, edit and modify the forum as a official user, or modify an inappropriate comment on the forum. These operation can be done on the `forum` tab on the web console.


#### <a name="UserProfile">- User Profile</a>
Manage users profile  

- [Use profile GUI](./GetStarted/GetStarted-User.md)
- What can be done on the web console
	- Developer can permanently suspend a bad user's account or for a certain period of time. Please check the `Users` tab on the web console.
- RelatedAPI
	- [FASUser](./Specs/Spec-User.md)

#### <a name="FriendManagement">- Friend Management</a>
Allow users to create their own community by inviting friends, and form their own groups to communicate/play together inside the app. Users will have ability to invite others to start a online match.

#### <a name="GroupMessage">- Group Message</a>
A chat space for app users to talk/chat with other users. App users can post text, images, play-video and stickers.

- [Use group message GUI](./GetStarted/GetStarted-GroupChat.md)
- Related API
	- [FASGroup](./Specs/Spec-Group.md)

#### <a name="InGameChat">- In Game Chat</a>
Chat system which works inside the game.  

- [How to use in-game text chat](./GetStarted/GetStarted-GroupChat.md#HowToUseInGameChat)
- Related API
	- [FASNotification](./Specs/Spec-Notification.md#FASNotification)
	- [FASGroup](./Specs/Spec-Group.md)

#### <a name="VoiceChat">- Voice Chat/In Game Voice Chat</a>
Fresvii voice chat will support up to 4 players to have a conversation at the same time. Players can talk with friends within the game, during their game play. (Useful for FPS games, Board games, MMO games, and more.)
Players can also start a voice session from the user profile inside AppSteroid GUI.

- [ボイスチャットの利用方法](./GetStarted/GetStarted-VoiceChat.md)
- Related API
	- [FASConference](./Specs/Spec-VoiceChat.md)
	- [FASNotification](./Specs/Spec-Notification.md)
	- [FASGroup](./Specs/Spec-Group.md)

#### <a name="PlayVideo">- Play Video</a>
Users can record their game play and share it with the AppSteroid community or other major social media (Facebook, Twitter, email). Users who watched the video can also share it with the community or other major social medias. Keep track of playback count and like count. 
 
Please check the related API for method to use video recording GUI or video share GUI.

- [How to show share screen](./Specs/Spec-PlayMovie.md#FASMovieMaker.presentShareView)
	- You can also show it only when there are video data after the recording.
- Related API
	- [FASPlayMovie](./Specs/Spec-PlayMovie.md)

#### <a name="PushNotificationForSetting">- Push Notification</a>
Push message will be distributed at the following conditions.

* Notify users when there is an update on a subscribed thread.
* Notify users when there is a new Group Message.
* Notify users with a new friend request/accept.
* Developers can deliver/schedule direct messages to a specific segment of users, which can also be automated.
* Notify users when their friend is requesting a match.
* Notification can also be trigger by a in-game Event.
* Working together with event can cause a synergy effect increasing user retention and engagement.

To use push notification, you must set it up specifically for iOS and Android.

- Settings
	- [Push Notification Settings](https://fresvii.zendesk.com/hc/en-us/articles/203512810-APNS-Certifiate-Tutorial)
- Send out push notification from the web console
	- Available from the `message` tab.
- [About custom message and channel](https://github.com/fresvii/appsteroid-documents/blob/master/en/ChannelTutorial.md)
	- [Use API](./Specs/Spec-Message.md#FASCustomMessage)
- Push Message Specification
	- [About Push Event](https://github.com/fresvii/appsteroid-documents/blob/master/en/EventList.md)

### <a name="PromotionService">App Promotion Service</a>
Features to promote applications. It increase user engagement and make a big user traffic between multiple apps.

#### <a name="OfficialForum">- Official Forum</a>
Open a new thread operated by the developer, and distribute app information to the user community. When the developer create a new thread, all users will receive a push message whether they are subscribed to the thread or not.

- What can be done on the web console
	- You can create the official forum from the `Forum` tab.

#### <a name="PushNotificationForPromotion">- Push Notification</a>
Developers can either target a specific player, segment players or address to the entire game community with their announcement.

- What can be done on the web console
	- You can shoot messages from the `Message` tab.


### <a name="SupportService">Game Management Support Service</a>
Features mainly used to manage/monetize the game. As same as the Backend features, it will significantly reduce the cost of development to manage the app.

#### <a name="Leaderboard">Leaderboard</a>
Score management feature. Developers can show scores for Today, Weekly and Total, or also have multiple leaderboards for a single game. (e.g. score, level, time, item count, etc. within a single game).

- [How to use leaderboard](./GetStarted/GetStarted-Leaderboard.md)
- What can be done on the web console
	- Creating, modifying and deleting the leaderboard can be done. Check the `Leaderboard` tab on the web console.
- Related API
	- [FASLeaderboard](./Specs/Spec-Leaderboard.md)

#### <a name="Matchmaking">Matchmake</a>
Matchmaker will automatically find the perfect opponents online with up to 16 players. “Play with friends” or “Play with the world” are provided as a default. A flexible filter settings can also be set up by the developer. “Play with same level”, “Play in the same region”, “Players with score under XX” and so on.

- [How to use Matchmake](./GetStarted/GetStarted-Matchmaking.md)
- Related API
	- [FASMatchmaking](./Specs/Spec-Matchmaking.md)
	- [FASStorage](./Specs/Spec-Storage.md)

#### <a name="CSR">Customer Support</a>
Feature to communicate/support app users through text. You can send messages to any users from the Web Console. All message logs between users and CSR can be checked on the Web Console as well.  
Once this feature is implemented into your app, Live Help button will appear on the top right corner of AppSteroid GUI in the message page. Users will be able to send message to the CSR through this Live Help button.

- [Use Customer Support](./Spec.md#AppSteroid.enableCSRChat)

#### <a name="Turn-BasedGame">Turn Based Game Support</a>
Support turn-based game such as chess, poker, monopoly and more. Ability to integrate with event for social use. Users can automatically send push message to opponents to notify their turn is coming up.

- [How to use Game Context](./GetStarted/GetStarted-Matchmaking.md#GameContext)
- Related API
	- [FASMatchmaking](./Specs/Spec-Matchmaking.md)
	- [GameContext](./Specs/Spec-Matchmaking.md#FASGameContext)
	- [FASNotification](./Specs/Spec-Notification.md)

### <a name="BackendService">Basic Backend as a Service</a>
AppSteroid will greatly reduces server side development cost from game developers.

#### <a name="UserCertification">User Authentication</a>
Automatically creates and maintains accounts with an 8 to 9 digit unique ID for all players without arduous UI. App users doesn't have to setup any user ID nor Password.

- Automated User Authentication
  - [Login and Show AppSteroid GUI](./5_UseFresviiGUI.md)
- Related API
	- [FASUser](./Specs/Spec-User.md)

#### <a name="SocialIntegration">Social Integration</a>
Store SNS (Facebook, Twitter) account ID and link information with app user. 
Check the related API for "how to use".

- Related API
	- [Setting SNSAccount](./Specs/Spec-User.md#FASSNSAccount.addUserSNSAccountuserIdsecretTokencompletion)
	- [Referring SNSAccount](./Specs/Spec-User.md#FASSNSAccount.fetchUserSNSAccounts)
	- [Deleting SNSAccount](./Specs/Spec-User.md#FASSNSAccount.deleteUserSNSAccount)

#### <a name="CloudStrage">Cloud Storage</a>
A Key-value-storage area mainly used to store game data.  
Check the related API for "how to use".

- Related API
	- [FASStorage](./Specs/Spec-Storage.md)

#### <a name="DataTransfer">Game Data Migration</a>
Enable data migration between devices with the same OS.

- Enable user data migration by using the same Apple account



### <a name="WebConsole">WEB Console Service</a>
Ability for your entire team to access and manage users, push message, app analytics, leaderboard, forum and many other data.


## <a name="Install">How to Implement AppSteroid SDK</a>
Please refer to [GetStarted](./3_GetStarted.md) for details.

