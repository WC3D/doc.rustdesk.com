---
title: ウェブコンソール
weight: 10
---

ウェブコンソールはRustDesk Server Proに統合されており、`21114`ポートで提供されます。

機能：

- デバイスの参照
- ユーザーとユーザーグループの追加/変更
- デバイスアクセス権限の変更
- デバイス接続ログと他のログの参照
- 設定の更新
- クライアント設定同期戦略の管理
- 共有アドレス帳の管理
- カスタムクライアントビルドの生成

## ログイン

ウェブコンソールのデフォルトポートは21114です。ブラウザで`http://<サーバーIP>:21114`を入力してコンソールページにアクセスします。下図に示すように、デフォルトの管理者ユーザー名/パスワードは`admin`/`test1234`です：

![](/docs/en/self-host/rustdesk-server-pro/console/images/console-login.png)

HTTPSサポートが必要な場合は、`Nginx`などのウェブサーバーをインストールするか、WindowsでIISを使用してください。

ログイン後は必ずパスワードを変更してください。右上隅のアカウントメニューで`設定`を選択してパスワード変更ページに移動します（下図参照）。別の管理者アカウントを作成してこのアカウントを削除することもできます。メールログイン認証を有効にすることをお勧めします。

<a name=console-home></a>
![](/docs/en/self-host/rustdesk-server-pro/console/images/console-home.png?v2)

管理者以外のユーザーもログインして自分のデバイスとログを参照し、ユーザー設定を変更できます。

## 自動設定
`Windows EXE`をクリックすると、独自のRustDesk Server Proの設定を取得でき、クライアントの設定に役立ちます。

Windowsクライアントの場合、カスタムサーバー設定を省略して、代わりに`rustdesk.exe`ファイル名に設定情報を入れることができます。上図に示すように、コンソールのウェルカムページに移動して`Windows EXE`をクリックしてください。**クライアント ≥ 1.1.9が必要です。**

これを[クライアント設定](https://rustdesk.com/docs/en/self-host/client-configuration/)と[デプロイメントスクリプト](https://rustdesk.com/docs/en/self-host/client-deployment/)と組み合わせて使用し、クライアントを設定できます。

## デフォルトの`admin`ユーザー以外の新しいユーザーの作成

{{% notice note %}}
`Individual`プランにはこの機能がありません。
{{% /notice %}}

1. 左側のメニューで`ユーザー`をクリックします。
2. `管理者`を有効にして別のアカウントを作成します。
3. 新しい管理アカウントでログインします。
4. `ユーザー`ページで`admin`を削除します。

## 新しいユーザーの作成
1. 左側のメニューで`ユーザー`をクリックします。
2. 新しいユーザーを作成します。
3. 所属するグループを選択します（新しいグループを追加する必要がある場合は、続きをお読みください）。

## 新しいグループの追加
1. 左側のメニューで`グループ`をクリックします。
2. 新しいグループを作成します。
3. 作成後、グループ間のアクセスを許可できます。`編集`をクリックします。
4. アクセスを希望する関連グループを選択します（対応するグループに自動的に追加されます）。

## 複数のリレーサーバーの設定
1. 左側のメニューで`設定`に移動します。
2. サブメニューで`リレー`をクリックします。
3. `リレーサーバー`の横の`+`をクリックします。
4. 表示されたボックスにリレーサーバーのDNSアドレスまたはIPアドレスを入力し、<kbd>Enter</kbd>を押します。
5. 複数のリレーサーバーがある場合は、`+`をクリックし続けて、必要に応じて地理的設定を調整できます（キーを他のサーバーにコピーすることを忘れないでください）。

## ライセンスの設定または変更
1. 左側のメニューで`設定`に移動します。
2. サブメニューで`ライセンス`をクリックします。
3. `編集`をクリックしてライセンスコードを貼り付けます。
4. `OK`をクリックします。

## ログの表示
左側で`ログ`をクリックします。

## メール設定
この例ではGmail

1. 左側のメニューで`設定`に移動します。
2. サブメニューで`SMTP`をクリックします。
3. SMTPアドレス`smtp.gmail.com`を入力します。
4. `SMTPポート`にポート587を入力します。
5. `メールアカウント`にGmailアカウント（例：`myrustdeskserver@gmail.com`）を入力します。
6. パスワードを入力します（アプリパスワードが必要な場合があります）。
7. `送信者`にGmailアカウント（例：`myrustdeskserver@gmail.com`）を入力します。
8. `確認`をクリックして保存します。

## デバイスユーザー/グループ/戦略/デバイスグループをデバイスに割り当て
ユーザーは、デバイスにログインしているRustDeskユーザー、またはデバイスの横の`編集`をクリックしてデバイスに割り当てられたユーザーです。`ユーザー`ボックスをクリックしてドロップダウンからユーザーを選択すると、ユーザーが割り当てられたグループに基づいてグループが自動的に割り当てられます。

これは、デプロイ時または後でRustDesk実行可能ファイルに続いて`--assign --token <生成されたトークン> --user_name <ユーザー名>`を呼び出すことで、コマンドラインでAPIを介して行うこともできます。これを行うには、まず`設定 → トークン → 作成`に移動してデバイス権限を持つトークンを作成する必要があります。Windowsでの例は`"C:\Program Files\RustDesk\rustdesk.exe" --assign --token <生成されたトークン> --user_name <新しいユーザー>`です。

この方法で戦略を割り当てることもできます。例：`--assign --token <生成されたトークン> --strategy_name <戦略名>`。

この方法でアドレス帳を割り当てることもできます。例：`--assign --token <生成されたトークン> --address_book_name <アドレス帳名>`または`--assign --token <生成されたトークン> --address_book_name <アドレス帳名> --address_book_tag <アドレス帳タグ> --address_book_alias <エイリアス>`。`--address_book_alias`にはRustDesk Server Pro ≥1.5.8とクライアント ≥1.4.1が必要です。

この方法でデバイスグループ名を割り当てることもできます。例：`--assign --token <生成されたトークン> --device_group_name <デバイスグループ名>`。

Windowsのコマンドラインはデフォルトで出力がありません。出力を得るには、`"C:\Program Files\RustDesk\rustdesk.exe" <arg1> <arg2> ... | more`または`"C:\Program Files\RustDesk\rustdesk.exe" <arg1> <arg2> ... | Out-String`のように実行してください。[こちら](https://github.com/rustdesk/rustdesk/discussions/6377#discussioncomment-8094952)を参照してください。

## デバイスの検索
1. デバイスに移動します。
2. デバイス名検索フィールドに名前を入力し、`クエリ`をクリックするか<kbd>Enter</kbd>を押します。
3. ワイルドカードを使用するには、検索語の開始、終了、または両方に`%`を追加します。