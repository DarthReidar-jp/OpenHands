# 開発ガイド

このガイドは、OpenHandsのソースコードを編集して開発を行う人向けです。
変更を貢献したい場合は、まず[CONTRIBUTING.md](https://github.com/All-Hands-AI/OpenHands/blob/main/CONTRIBUTING.md)を確認して、プロジェクトのクローンと初期セットアップ方法を確認してください。
それ以外の場合は、OpenHandsプロジェクトを直接クローンすることができます。

## 開発用サーバーの起動

### 1. 要件
* Linux、Mac OS、または[Windows上のWSL](https://learn.microsoft.com/ja-jp/windows/wsl/install) [Ubuntu >= 22.04]
* [Docker](https://docs.docker.com/engine/install/)（MacOSの場合、詳細設定からデフォルトのDockerソケットの使用を許可してください！）
* [Python](https://www.python.org/downloads/) = 3.12
* [NodeJS](https://nodejs.org/en/download/package-manager) >= 20.x
* [Poetry](https://python-poetry.org/docs/#installing-with-the-official-installer) >= 1.8
* OS固有の依存関係:
  - Ubuntu: build-essential => `sudo apt-get install build-essential`
  - WSL: netcat => `sudo apt-get install netcat`

`make build`を実行する前に、これらの依存関係がすべてインストールされていることを確認してください。

#### sudo権限なしでの開発
システム管理者/sudo権限なしで`Python`や`NodeJs`をアップグレード/インストールしたい場合は、`conda`や`mamba`を使用してパッケージを管理できます：

```bash
# Mamba（condaの高速版）のダウンロードとインストール
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
bash Miniforge3-$(uname)-$(uname -m).sh

# Python 3.12、nodejs、poetryのインストール
mamba install python=3.12
mamba install conda-forge::nodejs
mamba install conda-forge::poetry
```

### 2. 環境のビルドとセットアップ
プロジェクトのビルドから始めます。これには環境のセットアップと依存関係のインストールが含まれます：

```bash
make build
```

### 3. 言語モデルの設定
OpenHandsは[litellm](https://docs.litellm.ai)ライブラリを通じて様々な言語モデルをサポートしています。
デフォルトではClaude Sonnet 3.5を使用していますが、他のモデルも使用可能です。

設定を行うには：

```bash
make setup-config
```

このコマンドは、LLM APIキー、モデル名、その他の変数の入力を求めます。モデル名はヘッドレスモードで実行する場合にのみ適用されます。UIを使用する場合は、UI内でモデルを設定してください。

注意：以前にdockerコマンドでOpenHandsを実行していた場合、ターミナルに環境変数が設定されている可能性があります。最終的な設定は以下の優先順位で適用されます：
環境変数 > config.toml変数 > デフォルト変数

### 4. アプリケーションの実行
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

### 6. LLMのデバッグ
言語モデルに問題が発生した場合や、単に動作を確認したい場合は、環境にDEBUG=1をエクスポートしてバックエンドを再起動してください。
OpenHandsはプロンプトとレスポンスをlogs/llm/CURRENT_DATEディレクトリに記録します。

### 8. テスト
#### ユニットテスト
```bash
poetry run pytest ./tests/unit/test_*.py
```

### 9. 依存関係の追加または更新
1. `pyproject.toml`に依存関係を追加するか、`poetry add xxx`を使用します。
2. `poetry lock --no-update`でpoetry.lockファイルを更新します。

## Dockerコンテナ内での開発

TL;DR

```bash
make docker-dev
```

詳細は[こちら](./containers/dev/README.md)をご覧ください。

ホストに必要なツールをすべてインストールせずに`OpenHands`を実行したい場合：

```bash
make docker-run
```

ホストに`make`がない場合は：

```bash
cd ./containers/dev
./dev.sh
```

ただし、ホストに[Docker](https://docs.docker.com/engine/install/)のインストールは必要です。