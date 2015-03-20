# Play Movie Specifications

last update at 2015/02/02

---

## Introduction

Specifications for play movie capture.

---

## Classes

|Class|Description|
|------|-----|
|[FASMovieMaker](#FASMovieMaker)|Class for handling functions to recored game screen. |
|[FASVideo](#FASVideo)|Class to operate recorded play movie |

---

## APIs
### <a name="FASMovieMaker"> FASMovieMaker </a>
Class for handling functions to recored game screen.
Maximum recording time is 30 second.

#### Delegates

|Delegate|Description|
|------|-----|
|[FASMovieMakerDelegate](#FASMovieMaker.FASMovieMakerDelegate)|Handle the notification for ending recording. |

##### <a name="FASMovieMaker.FASMovieMakerDelegate"> FASMovieMakerDelegate </a>

|Method|Description|
|------|-----|
|[recordingWillFinish](#FASMovieMaker.FASMovieMakerDelegate.recordingWillFinish)|Call back right before the recording finish. |
|[recordingDidFinish:](#FASMovieMaker.FASMovieMakerDelegate.recordingDidFinish)|Call back when the video data is created after the recording completes. |

##### <a name="FASMovieMaker.FASMovieMakerDelegate.recordingWillFinish"> recordingWillFinish </a>
Called right before the recording finish.

\- (void)recordingWillFinish;

##### <a name="FASMovieMaker.FASMovieMakerDelegate.recordingDidFinish"> recordingDidFinish </a>
Call back when the video data is created after the recording completes.

\- (void)recordingDidFinish:(NSData *)videoData;

#### Constants

|Constant|Description|
|------|-----|
|[FASMovieMakerFPS](#FASMovieMaker.FASMovieMakerFPS)|List of FPS that can be used. |

##### <a name="FASMovieMaker.FASMovieMakerFPS"> FASMovieMakerFPS </a>
List of FPS that can be used.

```
typedef NS_ENUM(NSInteger, FASMovieMakerFPS)
{
	FASMovieMaker60FPS = 1,
	FASMovieMaker30FPS,
	FASMovieMaker20FPS,
	FASMovieMaker15FPS,
	FASMovieMaker12FPS,
	FASMovieMaker10FPS
};
```

###### Constants
###### FASMovieMaker60FPS
60fps

###### FASMovieMaker30FPS
30fps

###### FASMovieMaker20FPS
20fps

###### FASMovieMaker15FPS
15fps

###### FASMovieMaker12FPS
12fps

###### FASMovieMaker10FPS
10fps

#### Properties

|Properties|Description|
|------|-----|
|[bitRate](#FASMovieMaker.bitRate)|Select a bit rate |
|[fps](#FASMovieMaker.fps)|Select a FPS value on `FASPlayMovieRecorderFPS` to decide which FPS to use for recording. |
|[videoData](#FASMovieMaker.videoData)|Recorded videos are stored |
|[delegate](#FASMovieMaker.delegate)|Handle the notification for ending recording. |

##### <a name="FASMovieMaker.bitRate"> bitRate </a>
Select a bit rate. Default value is `1Mb`.

@property (nonatomic, setter = setBitRate:) float bitRate;

##### <a name="FASMovieMaker.bitRate"> fps </a>
Select a FPS value on `FASMovieMakerFPS` to decide which FPS to use for recording. Default value is `FASMovieMaker30FPS`.

@property (nonatomic) FASMovieMakerFPS fps;

##### <a name="FASMovieMaker.videoData"> videoData </a>
Recorded videos are stored

@property (nonatomic, readonly) NSData *videoData;

##### <a name="FASMovieMaker.delegate"> delegate </a>
Handle the notification for ending recording.

@property (weak, nonatomic) id <FASMovieMakerDelegate> delegate;

#### Instance Methods

|Method|Description|
|------|-----|
|[initWithCaptureView:withAudio:](#FASMovieMaker.initWithCaptureViewwithAudio) |Initialize `FASMovieMaker` Class and return the object |
|[startRecording](#FASMovieMaker.startRecording) |Start recording |
|[stopRecording](#FASMovieMaker.stopRecording) |Stop recording |
|[isRecording](#FASMovieMaker.isRecording) |Return whether if it is recording or not |
|[presentShareView](#FASMovieMaker.presentShareView) |Show share view for uploading videos to SNS |

##### <a name="FASMovieMaker.initWithCaptureViewwithAudio"> initWithCaptureView:withAudio: </a>
Initialize `FASMovieMaker` Class and return the object

\- (instancetype)initWithCaptureView:(UIView*)view
                           withAudio:(bool)withAudio;

##### <a name="FASMovieMaker.startRecording"> startRecording </a>
Start recording.

\- (void)startRecording;

##### <a name="FASMovieMaker.stopRecording"> stopRecording </a>
End recording.

\- (void)stopRecording;

##### <a name="FASMovieMaker.isRecording"> isRecording </a>
Return whether if it is recording or not

\- (bool)isRecording;

##### <a name="FASPlayMovieRecorder.presentShareView"> presentShareView </a>
Show share view for uploading videos to SNS. Process [stopRecording](#FASMovieMaker.stopRecording) and use it after completing recording a video.

\- (void)presentShareView;

### <a name="FASVideo"> FASVideo </a>
Class to operate recorded play movie.

#### Constants

|Constant|Description|
|------|-----|
|[FASVideoStatus](#FASVideo.FASVideoStatus)|Video status |

##### <a name="FASVideo.FASVideoStatus"> FASVideoStatus </a>
Video status

```
typedef NS_ENUM(NSInteger, FASVideoStatus)
{
    FASVideoStatusInvalid,
    FASVideoStatusRemoved,
    FASVideoStatusNa,
    FASVideoStatusReady,
};
```

###### Constants
###### FASVideoStatusInvalid
Status is invalid

###### FASVideoStatusRemoved
Status showing that video was removed

###### FASVideoStatusNa
Status showing that video does not exist

###### FASVideoStatusReady
Status showing that video is ready to play

#### Constants

|Constant|Description|
|------|-----|
|[FASVideoCompletionHandler](#FASVideo.FASVideoCompletionHandler)|Block object used when carrying out the process to get video upload. |
|[FASVideosCompletionHandler](#FASVideo.FASVideosCompletionHandler)|Block object used when carrying out the process to get multiple videos. |

##### <a name="FASVideo.FASVideoCompletionHandler"> (^FASVideoCompletionHandler)(FASVideo *video, NSError *error) </a>
Block object used when carrying out the process to get video upload.

typedef void (^FASVideoCompletionHandler)(FASVideo *video, NSError *error);

* Parameters
	* video
		* [FASVideo](#FASVideo) is stored.
	* error
		* Error detail is stored. It will be nil if there is no error.

##### <a name="FASVideo.FASVideosCompletionHandler"> (^FASVideosCompletionHandler)(NSArray/*<FASVideo>*/ *videos, FASPagingMeta *meta, NSError *error) </a>
Block object used when carrying out the process to get multiple videos.

typedef void (^FASVideosCompletionHandler)(NSArray/*<FASVideo>*/ *videos, FASPagingMeta *meta, NSError *error);

* Parameters
	* videos
		* Multiple [FASVideo](#FASVideo) are stored in NSArray.
	* meta
		* You can refer meta-information such as total number of list or current page number. Check [FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta) for more information.
	* error
		* Error detail is stored. It will be nil if there is no error.

#### Properties

|Properties|Description|
|------|-----|
|[videoId](#FASVideo.videoId)|Uploaded VideoID |
|[title](#FASVideo.title)|Video title |
|[bytesize](#FASVideo.bytesize)|Video byte size |
|[videoUrl](#FASVideo.videoUrl)|Video URL |
|[thumbnailUrl](#FASVideo.thumbnailUrl)|Video thumbnail URL |
|[duration](#FASVideo.duration)|Playback time of the video |
|[playbackCount](#FASVideo.playbackCount)|Playback count |
|[likesCount](#FASVideo.likesCount)|Favorite count |
|[liked](#FASVideo.liked)|Whether the logged in user add the video to their favorite or not |
|[updatedAt](#FASVideo.updatedAt)|Date/time when the video was updated |
|[createdAt](#FASVideo.createdAt)|Uploaded time of video |
|[user](#FASVideo.user)|[FASUser](Spec-User.md#FASUser) object of user who uploaded the video |

##### <a name="FASVideo.videoId"> videoId </a>
Uploaded VideoID

@property (nonatomic, readonly) NSString *videoId;

##### <a name="FASVideo.title"> title </a>
Video title

@property (nonatomic, readonly) NSString *title;

##### <a name="FASVideo.bytesize"> bytesize </a>
Video byte size

@property (nonatomic, readonly) unsigned long bytesize;

##### <a name="FASVideo.videoUrl"> videoUrl </a>
Video URL

@property (nonatomic, readonly) NSString *videoUrl;

##### <a name="FASVideo.thumbnailUrl"> thumbnailUrl </a>
Video thumbnail URL

@property (nonatomic, readonly) NSString *thumbnailUrl;

##### <a name="FASVideo.duration"> duration </a>
Playback time of the video

@property (nonatomic, readonly) float duration;

##### <a name="FASVideo.playbackCount"> playbackCount </a>
Playback count

@property (nonatomic, readonly) NSUInteger playbackCount;

##### <a name="FASVideo.likesCount"> likesCount </a>
Favorite count

@property (nonatomic, readonly) NSUInteger likesCount;

##### <a name="FASVideo.liked"> liked </a>
Whether the logged in user add the video to their favorite or not

@property (nonatomic, readonly) BOOL liked;

##### <a name="FASVideo.updatedAt"> updatedAt </a>
Date/time when the video was updated

@property (nonatomic, readonly) NSDate *updatedAt;

##### <a name="FASVideo.createdAt"> createdAt </a>
Uploaded time of video

@property (nonatomic, readonly) NSDate *createdAt;

##### <a name="FASVideo.user"> user </a>
[FASUser](Spec-User.md#FASUser) object of user who uploaded the video

@property (nonatomic, readonly) FASUser *user;

#### Class Methods

|Method|Description|
|------|-----|
|[uploadVideoWithData:completion:](#FASVideo.uploadVideoWithDatacompletion)|Upload video and return [FASVideo](#FASVideo) |
|[uploadVideoWithData:title:completion:](#FASVideo.uploadVideoWithDatatitlecompletion)|Upload video and title then return [FASVideo](#FASVideo) |
|[fetchAllVideosWithPage:completion:](#FASVideo.fetchAllVideosWithPagecompletion)|All users will get uploaded video |
|[fetchMyVideosWithPage:completion:](#FASVideo.fetchMyVideosWithPagecompletion)|Logged in user will get uploaded video |
|[deleteVideoWithVideoId:completion:](#FASVideo.deleteVideoWithVideoIdcompletion)|Delete video |
|[likeVideoWithVideoId:completion:](#FASVideo.likeVideoWithVideoIdcompletion)|Add video to favorite |
|[unlikeVideoWithVideoId:completion:](#FASVideo.unlikeVideoWithVideoIdcompletion)|Remove video from favorite |
|[incrementPlaybackCountWithVideoId:completion:](#FASVideo.incrementPlaybackCountWithVideoIdcompletion)|Increment playback count for the video |

##### <a name="FASVideo.uploadVideoWithDatacompletion"> uploadVideoWithData:completion: </a>
Upload video and return [FASVideo](#FASVideo)

\+ (void)uploadVideoWithData:(NSData *)videoData
                  completion:(FASVideoCompletionHandler)completion;

Sample

```
#import <AppSteroid/FASVideo.h>

	…
	…

- (IBAction)pushedUploadButton:(id)sender
{
    [FASVideo uploadVideoWithData:_videoData
                       completion:^(FASVideo *video, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASVideo.uploadVideoWithDatatitlecompletion"> uploadVideWithData:title:completion: </a>
Upload video and title then return [FASVideo](#FASVideo)

\+ (void)uploadVideoWithData:(NSData *)videoData
                       title:(NSString *)title
                  completion:(FASVideoCompletionHandler)completion;

Sample

```
#import <AppSteroid/FASVideo.h>

	…
	…

- (IBAction)pushedUploadButton:(id)sender
{
    [FASVideo uploadVideoWithData:_videoData
                            title:@"video title"
                       completion:^(FASVideo *video, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```
##### <a name="FASVideo.fetchAllVideosWithPagecompletion"> fetchAllVideosWithPage:completion: </a>
All users will get uploaded video

\+ (void)fetchAllVideosWithPage:(NSUInteger)page
                     completion:(FASVideosCompletionHandler)completion;

Sample

```
#import <AppSteroid/FASVideo.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASVideo fetchAllVideosWithPage:_page
                          completion:^(NSArray *videos, FASPagingMeta *meta, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASVideo.fetchMyVideosWithPagecompletion"> fetchMyVideosWithPage:completion: </a>
Logged in user will get uploaded video

\+ (void)fetchMyVideosWithPage:(NSUInteger)page
                    completion:(FASVideosCompletionHandler)completion;

Sample

```
#import <AppSteroid/FASVideo.h>

	…
	…

- (IBAction)pushedFetchButton:(id)sender
{
    [FASVideo fetchMyVideosWithPage:_page
                         completion:^(NSArray *videos, FASPagingMeta *meta, NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASVideo.deleteVideoWithVideoIdcompletion"> deleteVideoWithVideoId:completion: </a>
Delete Video

\+ (void)deleteVideoWithVideoId:(NSString *)videoId
                     completion:(FASCompletionHandler)completion;

Sample

```
#import <AppSteroid/FASVideo.h>

	…
	…

- (IBAction)pushedDeleteButton:(id)sender
{
    [FASVideo deleteVideoWithVideoId:_videoData
                          completion:^(NSError *error)
    {
        // It will be called when the process is completed.
    }];
}
```

##### <a name="FASVideo.likeVideoWithVideoIdcompletion"> likeVideoWithVideoId:completion: </a>
Add video to favorite

\+ (void)likeVideoWithVideoId:(NSString *)videoId
                   completion:(FASVideoCompletionHandler)completion;
                     
##### <a name="FASVideo.unlikeVideoWithVideoIdcompletion"> unlikeVideoWithVideoId:completion: </a>
Remove video from favorite

\+ (void)unlikeVideoWithVideoId:(NSString *)videoId
                     completion:(FASVideoCompletionHandler)completion;
                     
##### <a name="FASVideo.incrementPlaybackCountWithVideoIdcompletion"> incrementPlaybackCountWithVideoId:completion: </a>
Increment playback count for the video

\+ (void)incrementPlaybackCountWithVideoId:(NSString *)videoId
                                completion:(FASVideoCompletionHandler)completion;