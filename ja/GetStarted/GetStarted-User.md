# Getting Started - User

last update at 2014/10/7

---

- [ユーザーの作成とログイン](#SignupAndLogin)

---

## <a name="SignupAndLogin"> ユーザーの作成とログイン </a>

AppSteroidのほとんどの機能を利用するにはユーザーを作成してログインする必要があります。
[AppSteroid#start](../7_Spec.md#AppSteroid.startWithAppIdentifiersecretToken)関数を利用することで自動的にユーザー作成からログインまで行うことができるので、特別に実装が必要なことはありません。

既にユーザーが作成されているかどうか、ログイン状態が切れていないかどうかは以下の関数で知ることが出来ます。

```
// ユーザーが作成されているかどうか
if ([FASAccount currentLoggedInUser].isSignedUp)
{
    // 既にユーザーが作成されています
}

// ログイン状態が切れているかどうか
if ([FASAccount currentLoggedInUser].isExpiredSession)
{
    // ログイン状態が切れています
}
```
