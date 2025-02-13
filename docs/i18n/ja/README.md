# OpenHands: コードを書く量を減らし、より多くを実現

OpenHands（旧OpenDevin）へようこそ。AIを活用したソフトウェア開発エージェントのためのプラットフォームです。

OpenHandsのエージェントは、人間の開発者ができることは何でもできます：コードの修正、コマンドの実行、Webの閲覧、
APIの呼び出し、そしてもちろん—StackOverflowからコードスニペットをコピーすることもできます。

詳しくは[docs.all-hands.dev](https://docs.all-hands.dev)をご覧ください。

## ⚡ クイックスタート

OpenHandsを実行する最も簡単な方法はDockerを使用することです。
システム要件や詳細については[OpenHandsの実行](https://docs.all-hands.dev/modules/usage/installation)ガイドをご覧ください。

```bash
docker pull docker.all-hands.dev/all-hands-ai/runtime:0.23-nikolaik

docker run -it --rm --pull=always \
    -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.23-nikolaik \
    -e LOG_ALL_EVENTS=true \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v ~/.openhands-state:/.openhands-state \
    -p 3000:3000 \
    --add-host host.docker.internal:host-gateway \
    --name openhands-app \
    docker.all-hands.dev/all-hands-ai/openhands:0.23
```

OpenHandsは[http://localhost:3000](http://localhost:3000)で実行されます！

最後に、モデルプロバイダーとAPIキーが必要です。
[Anthropicのクロード3.5 Sonnet](https://www.anthropic.com/api) (`anthropic/claude-3-5-sonnet-20241022`)
が最も適していますが、[他の選択肢](https://docs.all-hands.dev/modules/usage/llms)もあります。

> [!注意]
> OpenHandsは、ローカルワークステーションで単一のユーザーが実行することを想定しています。
> 複数のユーザーが同じインスタンスを共有するマルチテナント環境での使用には適していません。
> 組み込みの分離機能やスケーラビリティはありません。

## 開発者向けガイド

### 要件
* Linux、Mac OS、または[Windows上のWSL](https://learn.microsoft.com/ja-jp/windows/wsl/install) [Ubuntu >= 22.04]
* [Docker](https://docs.docker.com/engine/install/)（MacOSの場合、詳細設定からデフォルトのDockerソケットの使用を許可してください！）
* [Python](https://www.python.org/downloads/) = 3.12
* [NodeJS](https://nodejs.org/en/download/package-manager) >= 20.x
* [Poetry](https://python-poetry.org/docs/#installing-with-the-official-installer) >= 1.8
* OS固有の依存関係:
  - Ubuntu: build-essential => `sudo apt-get install build-essential`
  - WSL: netcat => `sudo apt-get install netcat`

### 環境のビルドとセットアップ
プロジェクトをビルドし、環境をセットアップするには：

```bash
make build
```

### 言語モデルの設定
OpenHandsは[litellm](https://docs.litellm.ai)ライブラリを通じて様々な言語モデルをサポートしています。
デフォルトではClaude Sonnet 3.5を使用していますが、他のモデルも使用可能です。

設定を行うには：

```bash
make setup-config
```

### アプリケーションの実行
#### オプションA：完全なアプリケーションの実行
```bash
make run
```

#### オプションB：個別のサーバー起動
- バックエンドサーバーの起動：
    ```bash
    make start-backend
    ```

- フロントエンドサーバーの起動：
    ```bash
    make start-frontend
    ```

## 🤝 コミュニティへの参加方法

OpenHandsはコミュニティ主導のプロジェクトで、誰からの貢献も歓迎します。主なコミュニケーションはSlackで行われていますが、DiscordやGithubでも連絡を取ることができます：

- [Slackワークスペースに参加](https://join.slack.com/t/openhands-ai/shared_invite/zt-2ypg5jweb-d~6hObZDbXi_HEL8PDrbHg) - 研究、アーキテクチャ、今後の開発について話し合います。
- [Discordサーバーに参加](https://discord.gg/ESHStjSjD4) - 一般的な議論、質問、フィードバックのためのコミュニティ運営サーバーです。
- [Github Issuesの閲覧や投稿](https://github.com/All-Hands-AI/OpenHands/issues) - 取り組んでいる課題を確認したり、自分のアイデアを追加したりできます。

## 📜 ライセンス

MITライセンスの下で配布されています。詳細は[`LICENSE`](./LICENSE)をご覧ください。