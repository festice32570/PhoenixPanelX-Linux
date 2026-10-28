# PhoenixPanelX — Linux edition (binary preview)

**公開リポジトリにはソースコードを置きません。** GitHubの自動生成するSource codeアーカイブにはREADME等の公開文書だけが入り、アプリケーションのPython/Cソースは含まれません。配布バイナリの逆解析を完全に防ぐものではありません。

## 日本語

PhoenixPanelXは、CPU/GPU使用率、温度、メモリ、ストレージ、電力（取得可能なGPU電力のみ）、冷却を表示するクラシックデザインの監視ガジェットです。温度警告、Beep／本体オーディオ、配色、日本語・英語切替、固定ガジェット／スクロールウィンドウを備えています。

### 検証したOSとハードウェア

| 項目 | 検証環境 |
|---|---|
| OS | **Zorin OS 18.1**（Ubuntu 24.04系列） |
| Linuxカーネル | **7.0.0-38-generic** |
| GUI | GNOME / X11 |
| CPU | Intel Core 2 Quad Q9650 |
| GPU | NVIDIA GeForce GTX 960（nvidia-smi） |
| RAM | DDR2、16GiBクラス |
| アーキテクチャ | x86_64 |

**この環境以外での実機検証はまだ完了していません。** AMD/Intel GPU、Wayland、その他ディストリビューションには未確認の点があります。GPUのW表示はPC全体の消費電力ではありません。温度保護の代用にしないでください。

### 実行方法

[Releases](../../releases) から `PhoenixPanelX-Linux-x86_64` を入手し、以下を実行します。対応するGTK 3等のライブラリが必要な場合があります。

```bash
chmod +x ./PhoenixPanelX-Linux-x86_64
./PhoenixPanelX-Linux-x86_64
```

### sudo、su、Beepの扱い

**通常の温度監視にはroot/su権限は不要で、PhoenixPanelX自体をroot実行しないでください。** 本体オーディオの警告も一般ユーザーで再生します。物理マザーボードBeepにはスピーカー・ドライバー・アクセス権が必要です。

任意の `phoenixpanelx-beep-permissions_amd64.deb` は、root所有の「固定0.5秒Beep」補助処理を導入します。パッケージを入れただけではユーザーへの追加sudo権限は発生しません。設定画面の「Beep専用の権限を許可」からPolkit管理者認証後、特定コマンドだけのsudoers権限が永続化され、再起動後も有効です。「許可を取り消す」で解除でき、パッケージ削除時にも専用ルールを解除します。同じアカウントの他の処理もこの限定Beep処理を呼べるため、**GUIだけへの厳密な権限隔離ではありません。**

開発PCには以前から **`NOPASSWD: ALL`** の設定があり、権限のない別PCでのPolkit許可や再起動後の動作は未検証です。これを一般ユーザーに付与する必要はなく、推奨もしません。補助パッケージはDebian/Ubuntu系列の**amd64専用**です。

**公開状態：開発プレビュー。Linux全般での動作保証・正式な商標確認は未完了です。**

## English

PhoenixPanelX is a Linux hardware monitoring gadget with CPU/GPU load, actual available temperatures, memory, storage, GPU power, thermal alerts, bilingual settings and color themes.

**Tested only on Zorin OS 18.1, kernel 7.0.0-38-generic, GNOME/X11, Core 2 Quad Q9650, GTX 960 and DDR2 RAM on x86_64.** Other distributions, AMD/Intel GPUs and Wayland have not been verified. Run the monitor as an ordinary user; root/su is not required. The optional fixed-duration motherboard Beep authorization add-on grants only a specific command after administrator authentication; that permission survives reboot and is revocable. The development PC previously had blanket passwordless sudo, which is neither required nor recommended.

**Application source remains private. Experimental binary preview only.**
