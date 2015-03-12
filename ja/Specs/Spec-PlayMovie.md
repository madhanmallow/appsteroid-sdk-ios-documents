# Play Movie Specifications

last update at 2015/2/2

---

## Introduction

プレイ動画の録画に関する機能の仕様書です。

---

## Classes

|Class|Description|
|------|-----|
|[FASMovieMaker](#FASMovieMaker)|ゲーム画面をレコーディングする機能を取り扱うためのクラス |
|[FASVideo](#FASVideo)|録画したプレイムービーの操作に関するクラス |

---

## APIs
### <a name="FASMovieMaker"> FASMovieMaker </a>
ゲーム画面をレコーディングする機能を取り扱うためのクラスです。
レコーディング時間は最大30秒までです。

#### Delegates

|Delegate|Description|
|------|-----|
|[FASMovieMakerDelegate](#FASMovieMaker.FASMovieMakerDelegate)|レコーディング終了の通知をハンドリングします。 |

##### <a name="FASMovieMaker.FASMovieMakerDelegate"> FASMovieMakerDelegate </a>

|Method|Description|
|------|-----|
|[recordingWillFinish](#FASMovieMaker.FASMovieMakerDelegate.recordingWillFinish)|レコーディングが終了した直前に呼ばれます。 |
|[recordingDidFinish:](#FASMovieMaker.FASMovieMakerDelegate.recordingDidFinish)|レコーディングが完全に終了し、ビデオデータが作成された時に呼ばれます。 |

##### <a name="FASMovieMaker.FASMovieMakerDelegate.recordingWillFinish"> recordingWillFinish </a>
レコーディングが終了した直前に呼ばれます。

\- (void)recordingWillFinish;

##### <a name="FASMovieMaker.FASMovieMakerDelegate.recordingDidFinish"> recordingDidFinish </a>
レコーディングが完全に終了し、ビデオデータが作成された時に呼ばれます。

\- (void)recordingDidFinish:(NSData *)videoData;

#### Constants

|Constant|Description|
|------|-----|
|[FASMovieMakerFPS](#FASMovieMaker.FASMovieMakerFPS)|利用可能なFPS一覧です。 |

##### <a name="FASMovieMaker.FASMovieMakerFPS"> FASMovieMakerFPS </a>
利用可能なFPS一覧です。

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

###### FASMovieMaker15FPS
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
|[bitRate](#FASMovieMaker.bitRate)|ビットレートを指定します。 |
|[fps](#FASMovieMaker.fps)|どのFPSでレコーディングを行うかを決定します。`FASMovieMakerFPS`の中から指定します。 |
|[videoData](#FASMovieMaker.videoData)|レコーディングされた動画が格納されています。 |
|[delegate](#FASMovieMaker.delegate)|レコーディング終了の通知をハンドリングします。 |

##### <a name="FASMovieMaker.bitRate"> bitRate </a>
ビットレートを指定します。デフォルト値は`1Mb`です。

@property (nonatomic, setter = setBitRate:) float bitRate;

##### <a name="FASMovieMaker.bitRate"> fps </a>
どのFPSでレコーディングを行うかを決定します。`FASMovieMakerFPS`の中から指定します。デフォルト値は`FASMovieMaker30FPS`です。

@property (nonatomic) FASMovieMakerFPS fps;

##### <a name="FASMovieMaker.videoData"> videoData </a>
レコーディングされた動画が格納されています。

@property (nonatomic, readonly) NSData *videoData;

##### <a name="FASMovieMaker.delegate"> delegate </a>
レコーディング終了の通知をハンドリングします。

@property (weak, nonatomic) id <FASMovieMakerDelegate> delegate;

#### Instance Methods

|Method|Description|
|------|-----|
|[initWithCaptureView:withAudio:](#FASMovieMaker.initWithCaptureViewwithAudio) |`FASMovieMaker`クラスを初期化してオブジェクトを返却します。 |
|[startRecording](#FASMovieMaker.startRecording) |レコーディングを開始します。 |
|[stopRecording](#FASMovieMaker.stopRecording) |レコーディングを終了します。 |
|[isRecording](#FASMovieMaker.isRecording) |レコーディング中かどうかを返却します。 |
|[presentShareView](#FASMovieMaker.presentShareView) |動画をアップロードしてSNSにシェアするためのビューを表示します。 |

##### <a name="FASMovieMaker.initWithCaptureViewwithAudio"> initWithCaptureView:withAudio: </a>
`FASMovieMaker`クラスを初期化してオブジェクトを返却します。

\- (instancetype)initWithCaptureView:(UIView*)view
                           withAudio:(bool)withAudio;

##### <a name="FASMovieMaker.startRecording"> startRecording </a>
レコーディングを開始します。

\- (void)startRecording;

##### <a name="FASMovieMaker.stopRecording"> stopRecording </a>
レコーディングを終了します。

\- (void)stopRecording;

##### <a name="FASMovieMaker.isRecording"> isRecording </a>
レコーディング中かどうかを返却します。

\- (bool)isRecording;

##### <a name="FASPlayMovieRecorder.presentShareView"> presentShareView </a>
動画をアップロードしてSNSにシェアするためのビューを表示します。[stopRecording](#FASMovieMaker.stopRecording)をして動画を作成した後に利用してください。

\- (void)presentShareView;

### <a name="FASVideo"> FASVideo </a>
録画したプレイムービーの操作に関するクラス

#### Constants

|Constant|Description|
|------|-----|
|[FASVideoCompletionHandler](#FASVideo.FASVideoCompletionHandler)|ビデオアップロードの取得処理を行った際に利用されるブロックオブジェクト |
|[FASVideosCompletionHandler](#FASVideo.FASVideosCompletionHandler)|複数のビデオ取得処理を行った際に利用されるブロックオブジェクト |

##### <a name="FASVideo.FASVideoCompletionHandler"> (^FASVideoCompletionHandler)(FASVideo *video, NSError *error) </a>
ビデオアップロードの取得処理を行った際に利用されるブロックオブジェクト

typedef void (^FASVideoCompletionHandler)(FASVideo *video, NSError *error);

* Parameters
	* video
		* [FASVideo](#FASVideo)が格納されています。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

##### <a name="FASVideo.FASVideosCompletionHandler"> (^FASVideosCompletionHandler)(NSArray/*<FASVideo>*/ *videos, FASPagingMeta *meta, NSError *error) </a>
複数のグループ取得処理を行った際に利用されるブロックオブジェクト。

typedef void (^FASVideosCompletionHandler)(NSArray/*<FASVideo>*/ *videos, FASPagingMeta *meta, NSError *error);

* Parameters
	* videos
		* 複数の[FASVideo](#FASVideo)がNSArrayに格納されています。
	* meta
		* リストの総数や、現在のページ番号等のメタ情報を参照することが出来ます。詳しくは[FASPagingMeta](../AppSteroidSpec.md#FASPagingMeta)を参照して下さい。
	* error
		* エラーの詳細が格納されています。エラーがない場合はnilになります。

#### Properties

|Properties|Description|
|------|-----|
|[videoId](#FASVideo.videoId)|アップロードしたビデオのID |
|[title](#FASVideo.title)|ビデオタイトル |
|[bytesize](#FASVideo.bytesize)|ビデオのバイトサイズ |
|[videoUrl](#FASVideo.videoUrl)|ビデオURL |
|[thumbnailUrl](#FASVideo.thumbnailUrl)|ビデオのサムネイル画像URL |
|[createdAt](#FASVideo.createdAt)|ビデオがアップロードされた時刻 |
|[user](#FASVideo.user)|ビデオをアップロードしたユーザーの[FASUser](Spec-User.md#FASUser)オブジェクト |

##### <a name="FASVideo.videoId"> videoId </a>
アップロードしたビデオのID

@property (nonatomic, readonly) NSString *videoId;

##### <a name="FASVideo.title"> title </a>
ビデオタイトル

@property (nonatomic, readonly) NSString *title;

##### <a name="FASVideo.bytesize"> bytesize </a>
ビデオのバイトサイズ

@property (nonatomic, readonly) unsigned long bytesize;

##### <a name="FASVideo.videoUrl"> videoUrl </a>
ビデオURL

@property (nonatomic, readonly) NSString *videoUrl;

##### <a name="FASVideo.thumbnailUrl"> thumbnailUrl </a>
ビデオのサムネイル画像URL

@property (nonatomic, readonly) NSString *thumbnailUrl;

##### <a name="FASVideo.createdAt"> createdAt </a>
ビデオがアップロードされた時刻

@property (nonatomic, readonly) NSDate *createdAt;

##### <a name="FASVideo.user"> user </a>
ビデオをアップロードしたユーザーの[FASUser](Spec-User.md#FASUser)オブジェクト

@property (nonatomic, readonly) FASUser *user;

#### Class Methods

|Method|Description|
|------|-----|
|[uploadVideoWithData:completion:](#FASVideo.uploadVideoWithDatacompletion)|ビデオをアップロードして[FASVideo](#FASVideo)を返却します。 |
|[uploadVideoWithData:title:completion:](#FASVideo.uploadVideoWithDatatitlecompletion)|ビデオとタイトルをアップロードして[FASVideo](#FASVideo)を返却します。 |
|[fetchAllVideosWithPage:completion:](#FASVideo.fetchAllVideosWithPagecompletion)|全ユーザーがアップロードしたビデオを取得します。 |
|[fetchMyVideosWithPage:completion:](#FASVideo.fetchMyVideosWithPagecompletion)|ログインユーザーがアップロードしたビデオを取得します。 |
|[deleteVideoWithVideoId:completion:](#FASVideo.deleteVideoWithVideoIdcompletion)|ビデオを削除します。 |

##### <a name="FASVideo.uploadVideoWithDatacompletion"> uploadVideoWithData:completion: </a>
ビデオをアップロードして[FASVideo](#FASVideo)を返却します。

\+ (void)uploadoVideWithData:(NSData *)videoData
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
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASVideo.uploadVideoWithDatatitlecompletion"> uploadVideWithData:title:completion: </a>
ビデオとタイトルをアップロードして[FASVideo](#FASVideo)を返却します。

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
        // 処理が完了したら呼ばれます。
    }];
}
```
##### <a name="FASVideo.fetchAllVideosWithPagecompletion"> fetchAllVideosWithPage:completion: </a>
全ユーザーがアップロードしたビデオを取得します。

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
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASVideo.fetchMyVideosWithPagecompletion"> fetchMyVideosWithPage:completion: </a>
ログインユーザーがアップロードしたビデオを取得します。

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
        // 処理が完了したら呼ばれます。
    }];
}
```

##### <a name="FASVideo.deleteVideoWithVideoIdcompletion"> deleteVideoWithVideoId:completion: </a>
ビデオを削除します。

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
        // 処理が完了したら呼ばれます。
    }];
}
```
