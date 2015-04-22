# AppSteroid for iOS Release Notes

---

### 0.6.3
- New Feature
	- CSR (Customer Service Representative) Chat. Users will be able to initiate a 1 to 1 chat with the CSR on the group chat page.

- Fixed
	- Score value 0 cannot be submitted to the leaderboard.
  - Creating a new thread or group cause crash on iOS8.3.


### 0.6.2
- Performance Improvements
	- Stabilized network and movements for Matchmaking.
- Fixed
	- Error appears when repeatably reporting a same comment on the forum.

### 0.6.1
- New Feature
	- Account suspension, to prevent user to use AppSteroid features.
	- EULA (end user license agreement), for first time AppSteroid GUI user, is now available. This can be setup from the Fresvii Web Console. 

- Performance Improvements
	- User can now browse other users video list.

- Fixed
	- Matchmaking feature bug.

### 0.6.0
- New Feature
	- Ability to aggregate game/player statistical information.
		
- Performance Improvements
	- Leaderboard now support date and time format.
	- New layout for matchmaking GUI.
    - Loading speed of image on Forum and GroupChat.

### 0.5.1
- Performance Improvements
	- Show play count, like count and playback time on the video list.

- Fixed
	- Thumbnail image and text overlaps if the text on the forum is too long.
	- Does not contain video URL when sharing the video to SNS from the playback screen. 
	- Deletion thumbnail does not show up after deleting the posted video.
	- Layout bug on iPad.
  
### 0.5.0
- New Feature
	- Violation report. Users can tap & hold an inappropriate comment on the forum to report it as a violation. 
	- Favorite button on video player. Also, play count and favorite count is now displayed.  
	- Friend invitation on matchmaking.

- Performance Improvements
	- If an user receives a friend request, direct message or group message on the AppSteroid GUI, it will now dynamically add count on the related badge.

- Fixed
	- Continuous sound play even after closing the video player.

### 0.4.1
- New Feature
	- Enable URL link on Forum and GroupChat.

- Performance improvements
	- Blue icon added to unread message on group chat and direct message.

- Fixed Issue
	- Crash issue on GroupChat list page with certain devices are fixed.

### 0.4.0
- New Feature
	- Page for list of received direct message and details. New pages can be checked on MyProfile.
	- Video Player UI.
	- Unread messages in group message page will be bold text. Also, badges showing the number of unread messages on the tab.
	- API to operate group message [FASDirectMessage](Specs/Spec-Message.md#FASDirectMessage).

- Fixed Issue
	- Contents to show on tab bar can be edit with [AppSteroid#setTabs:](AppSteroidSpec.md#AppSteroid.setTabs).
	- Display tab view when launching the AppSteroid GUI from the related push message.
	- Timeout can now be setup for matchmaking. Default value is 30 seconds.

### 0.3.1
- New Feature
	- Ability to select max/min number of players for Matchmaking on the Matchmake GUI

- Fixed Issue
	- Replaced call button for official user
	- Game title will automatically be added to the game video title when sharing them on Youtube
	- Show Popup alert if character limit goes over when sharing movies on Twitter


### 0.3.0
- New Feature
	- Development Mode
	- Video capturing
    - Reformed `FASPlayMovieRecorder` feature to [FASMovieMaker](Specs/Spec-PlayMovie.md#FASMovieMaker). `FASPlayMovieRecorder` is no longer be available.
    - Function to share recorded play video on Facebook, Twitter, Youtube, E-mail.
    - Function to share recorded play video to the AppSteroid community, such as Forum and Group.
	- Show direct message text on dialog after tapping the push notification.

- Fixed Issue
    - Disabled submit button on MyProfile when there weren't any changes made.

- Performance improvements
	- Add GroupChat tab, and delete the path from profile to group list.
	- Hide incoming dialog after a fixed period (20sec).
	- Changed default profile for Voice Chat to HighBandwidth. Improvements in sound quality.
	- New message for voice call error

### 0.2.3
- New Feature
	- Add ability to display "Not Now" list on the friend request page.

- Performance improvements
	- Add ability to delete pair group messages when unfriended.
	- The APNs setting documents are completely renovated.

### 0.2.2
- New Feature
	- Ability to change GUI layout provided by AppSteroid. Please check GetStarted for more information.

- Fixed Issue
	- Layout bug occurred in iPad2.

- Performance improvements
	- Show pair group on the screen, when creating a group with only two players.
	- Replaced member list button on the menu in pair group to profile button.

### 0.2.1
- New Feature
    - Add ability to directly go to Group list page from profile page.

- Performance improvements
    - Improved environment for Voice Chat to be more stable.

### 0.2.0
- New Feature
	- Match Making
	- Custom Message
	- Play Video Capturing

- Fixed Issue
	- FGCViewComponents Class is no longer supported.
	- Changed the structure to return meta information of the content, if the API response was array type.
	- `handleDidBecomeActive` function in `Fresvii` class became unusable, and will be performed automatically internally.

- Performance improvements
	- Ability to display group list horizontally.
	- Add an option to display the view of the related subject when an user launch an app from a push notification.

### 0.1.6
- New Feature
	- Add Group Chat
	- Add Leaderboard

- Fixed Issue
	- Change made in display method for view with our SDK. Please refer to FGCViewComponents in SDK doc for further information.

- Performance improvements
	- Fixed problem with app shutting down when using FGCEvent.
	- Fixed small bugs and problems.

### 0.1.5
- New Feature
	- Add friend management system.
	- Add new class and method to handle Push notification.  Please refer to FGCEvent and FGCNotification in SDK doc for further information.

- Fixed Issue
	- Change made for the use of API to register SNS accounts.  Please refer to FGCSNSAccount in SDK doc for further information.

- Performance Improvements
	- Fixed small bugs and problems.

### 0.1.4
- Fixed Issues
	- Add confirm alert to appear on the screen when deleting a thread or a comment.
	- Removed "Copy text" from the context menu that appears when tap and hold on a comment only with images.
	- Add action to login users automatically when they sign up.

- Performance Improvements
	- Fixed some problems.
	- Improved performance in Forum.

### 0.1.3

- Fixed Issues
	- Fixed thread to be listed in chronological order by posted date.
	- Fixed some text in SDK.

- Performance Improvements
	-Improved performance in Forum.

### 0.1.2

- Fixed Issues
	- Fixed some problems.

### 0.1.1

- New Features
	- Add the option to use animation when displaying view with FGCViewComponents.
	- Add method to get class "UINavigationController" for each view in "FGCViewComponents".
	- Add the ability to save images on comments.

- Fixed Issues
	- Add Profile as a replacement for MyProfile.
	- Replaced the argument "NSString" to "NSData" for the deviceToken in FGCNotification.

- Performance Improvements
	- Improved scrolling movement on the Forum.

### 0.1.0
First Release
