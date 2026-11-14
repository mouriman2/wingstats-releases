# WingStats

星の翼の戦績を記録し、配信のオーバーレイに出す Windows アプリ（Rust 版）の配布場所です。
ソースコードは置いていません。インストーラと自動更新のファイルだけを Releases に置いています。

## ダウンロード

[最新の版](https://github.com/mouriman2/wingstats-releases/releases/latest) の `WingStats-win-Setup.exe` を開いてください。
入れたあとは、記録サービスが GitHub の Releases を見て自動で更新します。

## 入れ方と、Electron 版（WingStats Manager）からの乗り換え

### 1. 入れる

1. GitHub の Releases（https://github.com/mouriman2/wingstats-releases/releases/latest）から `WingStats-win-Setup.exe` をダウンロードして開く
   - 署名していないので「Windows によって PC が保護されました」と出たら、「詳細情報」→「実行」
   - 管理者の権限は要りません。`%LocalAppData%\WingStats` に入り、スタートメニューに「WingStats」ができます
2. 入れ終わると WingStats が開き、「インストールの仕上げ」が出ます。3 つ選んで「完了」
   - デスクトップにショートカットを作る
   - 記録サービスを常駐させる（Windows の起動時に立ち上げる。推奨）
   - 記録サービスをいま起動する
3. 初めて開いたときに、Electron 版のデータ（`%APPDATA%\streaming-overlay-manager`）を `%APPDATA%\WingStats` に写します

更新は Electron 版と同じく自動です。記録サービスが起動時と 6 時間ごとに GitHub の Releases を見て、新しい版があれば
ダウンロードし、トレイと通知で知らせます。記録サービスを終わるとき（またはトレイの行を押したとき）に入れ替わります。

### 2. Electron 版をアンインストールする

Electron 版が入っていると、「インストールの仕上げ」のあとに **記録と取得 › データ管理** の「Electron 版からの乗り換え」が開きます
（ホームの「次にやること」からも開けます）。

1. 「アンインストーラを開く」を押す（Electron 版のアンインストーラが開きます）
   - アンインストーラが Electron 版の画面・記録サービス（Recorder）・Viewer を止め、スタートメニューとデスクトップのショートカット、
     Windows の起動時の自動起動の登録を消します
   - **データは消えません**（`%APPDATA%\streaming-overlay-manager` は残ります）。「データも削除しますか」と聞かれたら、削除しないでください
2. アンインストールが終わると、カードが次の段に進みます（進まなければ「確かめ直す」）

カードを使わずに消すときは、Windows の **設定 › アプリ › インストールされているアプリ** で「WingStats Manager」の「…」→「アンインストール」。

### 3. 写したあとの試合を取り込む

「取り込む」を押すと、写したあとに Electron 版が記録した試合を、Electron 版のデータから足します（こちらに有る試合は飛ばします）。
Electron 版が入っている間は OBS の自動録画をこちらで止めていた（両方が OBS を操作しないため）ので、ここで元の設定に戻します。

### 4. 残ったデータ

乗り換えが済んだら、Electron 版のデータ（`%APPDATA%\streaming-overlay-manager`）は要りません。WingStats で戦績が見られるのを
確かめてから、カードの「フォルダを開く」で開いて、フォルダごと消してかまいません（消すと元に戻せません）。

### 変わらないもの・変わるもの

| | Electron 版 | WingStats（Rust 版） |
|---|---|---|
| スタートメニュー | WingStats フォルダの Manager・Recorder・Viewer | WingStats（1 つ。記録サービスはトレイ） |
| 入る場所 | `%LocalAppData%\Programs\...\WingStats Manager` | `%LocalAppData%\WingStats` |
| データ | `%APPDATA%\streaming-overlay-manager` | `%APPDATA%\WingStats` |
| 自動起動の登録 | WingStats Recorder | WingStats Service |
| 配布と更新 | GitHub（my-overlay-tool）の Releases | GitHub（wingstats-releases）の Releases |
| OBS のブラウザソースの URL | `http://127.0.0.1:<ポート>/overlay.html` | 同じ（設定のポートを引き継ぐ） |

### WingStats（Rust 版）をアンインストールする

Windows の **設定 › アプリ › インストールされているアプリ** で「WingStats」をアンインストール。自動起動の登録とデスクトップの
ショートカットも消えます。データ（`%APPDATA%\WingStats`）は残るので、要らなければ手で消してください。
