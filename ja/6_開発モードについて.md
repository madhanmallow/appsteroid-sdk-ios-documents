# 開発モードについて

---

## <a name="Introduction"></a>概要
AppSteroid上の全てのアプリケーションは開発用と本番用の２つのデータ領域を保有します。
開発モードで動作した場合、投稿など全てのデータは本番用とは別のデータベースに格納され、ユーザに見えません。
使い分けることで本番データを汚すことなく開発を行うことが可能です。


### <a name="development_mode"></a>開発モードの実行 (コード例)

起動時に startWithAppIdentifier:secretToken:development: を呼び出す事で開発モードとして実行できます。
典型的な使い方としては、シミュレーターや開発端末での動作させる場合は開発モードとしてビルドし、配布用ビルド時は本番モードとしてビルドすることです。
これをマクロを利用して実現した場合のコード例を以下に示します。

```obj-c
// AppDeletegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  …

#ifdef DEBUG
  [AppSteroid startWithAppIdentifier:"$YOUR_APP_ID"
                         secretToken:"$YOUR_APP_SECRET"
                         development:YES];
#else
  [AppSteroid startWithAppIdentifier:"$YOUR_APP_ID"
                         secretToken:"$YOUR_APP_SECRET"
                         development:NO];
#endif

  …

}

```

Build ConfigurationをDebugにすると開発モードとして実行し、Release/AdHoc にすると本番モードとして実行されます。

またモード毎にユーザを保存している為、一つの端末で開発モード・本番モードの両方で動作させた場合でも実行時のモードにあわせたユーザ情報を復元します。
これにより素早く本番データと開発データを切り替えて開発を行うことが可能となります。

**※注意** Webコンソールから行うデータ管理は本番用のデータとなります。


## APNs証明書の種類について

APNs証明書には Development および Production の２種類が存在します。（詳しくはiOS Dev Centerを参照）  

Webコンソールから本番用、開発用に個別に任意の種類の証明書を登録することが可能です。 この登録された証明書の種類とビルドに用いる Provisioning Profile の種類は必ず一致させる必要があります。 つまり、Webコンソールで登録したAPNs証明書が Developmentの場合、ビルドに用いるProvisioning ProfileもDevelopmentでないといけません。

Webコンソールに登録済みの証明書の種類とデバイストークン登録時の証明書の種類が一致しない場合はエラーとなり、デバイストークン登録処理時にエラーログが出力されます。  

AppSteroid SDK内部でProvisioning Profileの種類を特定しているので、デベロッパーは`AppDelegate.m`に以下のコードを記述するだけでデバイストークンをFresviiサーバーに登録することが可能です。

```obj-c
// AppDelegate.m
- (void)application:(UIApplication *)application
didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    [FASNotification addDeviceToken:deviceToken
                         completion:nil];
}

```


## 証明書登録時の注意点

Webコンソールより開発モード環境向けにProduction APNs証明書を登録し、XcodeからDebug設定で起動した場合（つまりProvisioning ProfileはDevelopmentを使用）、SDKは自動的にDevelopmentとしてデバイストークンを登録しようとします。この時、サーバ側で登録されている証明書(Production)とデバイストークン登録時に通知される環境(Development)が一致しない為、エラーとなりプッシュ通知を受けられません。

最もシンプルな方法は以下のように設定する事です。

1. Webコンソールより本番用にAPNs証明書(Production)、開発用にAPNs証明書(Development)をそれぞれ設定する。
2. 開発中は Provisioning Profile(Development) を用いてビルド、`[AppSteroid startWithAppIdentifier:appId secretToken:secretToken development:YES];` として実行。
3. 配布用は Provisioning Profile(Distribution) を用いてビルド、`[AppSteroid startWithAppIdentifier:appId secretToken:secretToken development:NO];` として実行。

以上のように設定する事を強く推奨します。