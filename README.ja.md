<div align="center">
  <img src="./docs/static/img/logo.png" alt="Logo" width="200">
  <h1 align="center">OpenHands: コードを書く量を減らし、より多くを作り出す</h1>
</div>


<div align="center">
  <a href="https://github.com/All-Hands-AI/OpenHands/graphs/contributors"><img src="https://img.shields.io/github/contributors/All-Hands-AI/OpenHands?style=for-the-badge&color=blue" alt="Contributors"></a>
  <a href="https://github.com/All-Hands-AI/OpenHands/stargazers"><img src="https://img.shields.io/github/stars/All-Hands-AI/OpenHands?style=for-the-badge&color=blue" alt="Stargazers"></a>
  <a href="https://codecov.io/github/All-Hands-AI/OpenHands?branch=main"><img alt="CodeCov" src="https://img.shields.io/codecov/c/github/All-Hands-AI/OpenHands?style=for-the-badge&color=blue"></a>
  <a href="https://github.com/All-Hands-AI/OpenHands/blob/main/LICENSE"><img src="https://img.shields.io/github/license/All-Hands-AI/OpenHands?style=for-the-badge&color=blue" alt="MIT License"></a>
  <br/>
  <a href="https://join.slack.com/t/openhands-ai/shared_invite/zt-2ypg5jweb-d~6hObZDbXi_HEL8PDrbHg"><img src="https://img.shields.io/badge/Slack-Join%20Us-red?logo=slack&logoColor=white&style=for-the-badge" alt="Join our Slack community"></a>
  <a href="https://discord.gg/ESHStjSjD4"><img src="https://img.shields.io/badge/Discord-Join%20Us-purple?logo=discord&logoColor=white&style=for-the-badge" alt="Join our Discord community"></a>
  <a href="https://github.com/All-Hands-AI/OpenHands/blob/main/CREDITS.md"><img src="https://img.shields.io/badge/Project-Credits-blue?style=for-the-badge&color=FFE165&logo=github&logoColor=white" alt="Credits"></a>
  <br/>
  <a href="https://docs.all-hands.dev/modules/usage/getting-started"><img src="https://img.shields.io/badge/Documentation-000?logo=googledocs&logoColor=FFE165&style=for-the-badge" alt="Check out the documentation"></a>
  <a href="https://arxiv.org/abs/2407.16741"><img src="https://img.shields.io/badge/Paper%20on%20Arxiv-000?logoColor=FFE165&logo=arxiv&style=for-the-badge" alt="Paper on Arxiv"></a>
  <a href="https://huggingface.co/spaces/OpenHands/evaluation"><img src="https://img.shields.io/badge/Benchmark%20score-000?logoColor=FFE165&logo=huggingface&style=for-the-badge" alt="Evaluation Benchmark Score"></a>
  <hr>
</div>

OpenHands（旧OpenDevin）へようこそ。AIを活用したソフトウェア開発エージェントのためのプラットフォームです。

OpenHandsのエージェントは、人間の開発者ができることは何でもできます：コードの修正、コマンドの実行、Webの閲覧、
APIの呼び出し、そしてもちろん—StackOverflowからコードスニペットをコピーすることもできます。

詳しくは[docs.all-hands.dev](https://docs.all-hands.dev)をご覧いただくか、[クイックスタート](#-クイックスタート)へ進んでください。

> [!IMPORTANT]
> OpenHandsを仕事で使用していますか？ぜひお話を伺いたいです！
> [この短いフォーム](https://docs.google.com/forms/d/e/1FAIpQLSet3VbGaz8z32gW9Wm-Grl4jpt5WgMXPgJ4EDPVmCETCBpJtQ/viewform)
> に記入して、デザインパートナープログラムにご参加ください。商用機能への早期アクセスと、製品ロードマップへの意見提供の機会が得られます。

![アプリのスクリーンショット](./docs/static/img/screenshot.png)

## ⚡ クイックスタート

OpenHandsを実行する最も簡単な方法は、Dockerを使用することです。
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
が最も適していますが、[他にも多くの選択肢](https://docs.all-hands.dev/modules/usage/llms)があります。

---

また、[OpenHandsをローカルファイルシステムに接続](https://docs.all-hands.dev/modules/usage/runtimes#connecting-to-your-filesystem)したり、
[ヘッドレスモード](https://docs.all-hands.dev/modules/usage/how-to/headless-mode)でスクリプト実行したり、
[使いやすいCLI](https://docs.all-hands.dev/modules/usage/how-to/cli-mode)で操作したり、
[GitHubアクション](https://docs.all-hands.dev/modules/usage/how-to/github-action)でタグ付けされたissueに対して実行したりすることもできます。

詳細な情報とセットアップ手順については[OpenHandsの実行](https://docs.all-hands.dev/modules/usage/installation)をご覧ください。

> [!CAUTION]
> OpenHandsは、ローカルワークステーションで単一ユーザーが実行することを想定しています。
> 複数のユーザーが同じインスタンスを共有するマルチテナント環境での使用には適していません。組み込みの分離機能やスケーラビリティはありません。
>
> マルチテナント環境でOpenHandsを実行することに興味がある場合は、
> 高度なデプロイメントオプションについて[お問い合わせください](https://docs.google.com/forms/d/e/1FAIpQLSet3VbGaz8z32gW9Wm-Grl4jpt5WgMXPgJ4EDPVmCETCBpJtQ/viewform)。

OpenHandsのソースコードを修正したい場合は、[Development.md](https://github.com/All-Hands-AI/OpenHands/blob/main/Development.md)をご確認ください。

問題が発生した場合は、[トラブルシューティングガイド](https://docs.all-hands.dev/modules/usage/troubleshooting)が役立ちます。

## 📖 ドキュメント

プロジェクトの詳細やOpenHandsの使用に関するヒントについては、
[ドキュメント](https://docs.all-hands.dev/modules/usage/getting-started)をご覧ください。

そこでは、異なるLLMプロバイダーの使用方法、トラブルシューティングリソース、高度な設定オプションなどを見つけることができます。

## 🤝 コミュニティへの参加方法

OpenHandsはコミュニティ主導のプロジェクトで、誰からの貢献も歓迎します。主なコミュニケーションは
Slackで行っていますので、まずはそこから始めることをお勧めしますが、DiscordやGithubでのご連絡も歓迎します：

- [Slackワークスペースに参加](https://join.slack.com/t/openhands-ai/shared_invite/zt-2ypg5jweb-d~6hObZDbXi_HEL8PDrbHg) - 研究、アーキテクチャ、今後の開発について話し合います。
- [Discordサーバーに参加](https://discord.gg/ESHStjSjD4) - 一般的な議論、質問、フィードバックのためのコミュニティ運営サーバーです。
- [Github Issuesの閲覧・投稿](https://github.com/All-Hands-AI/OpenHands/issues) - 取り組んでいる課題を確認したり、自分のアイデアを追加したりできます。

コミュニティについての詳細は[COMMUNITY.md](./COMMUNITY.md)を、貢献に関する詳細は[CONTRIBUTING.md](./CONTRIBUTING.md)をご覧ください。

## 📈 進捗

OpenHandsの月次ロードマップは[こちら](https://github.com/orgs/All-Hands-AI/projects/1)でご確認いただけます（毎月末のメンテナー会議で更新されます）。

<p align="center">
  <a href="https://star-history.com/#All-Hands-AI/OpenHands&Date">
    <img src="https://api.star-history.com/svg?repos=All-Hands-AI/OpenHands&type=Date" width="500" alt="Star History Chart">
  </a>
</p>

## 📜 ライセンス

MITライセンスの下で配布されています。詳細は[`LICENSE`](./LICENSE)をご覧ください。

## 🙏 謝辞

OpenHandsは多くの貢献者によって構築されており、すべての貢献に深く感謝しています！また、他のオープンソースプロジェクトの上に構築されており、それらの作業に深く感謝しています。

OpenHandsで使用されているオープンソースプロジェクトとライセンスのリストについては、[CREDITS.md](./CREDITS.md)ファイルをご覧ください。

## 📚 引用

```
@misc{openhands,
      title={{OpenHands: An Open Platform for AI Software Developers as Generalist Agents}},
      author={Xingyao Wang and Boxuan Li and Yufan Song and Frank F. Xu and Xiangru Tang and Mingchen Zhuge and Jiayi Pan and Yueqi Song and Bowen Li and Jaskirat Singh and Hoang H. Tran and Fuqiang Li and Ren Ma and Mingzhang Zheng and Bill Qian and Yanjun Shao and Niklas Muennighoff and Yizhe Zhang and Binyuan Hui and Junyang Lin and Robert Brennan and Hao Peng and Heng Ji and Graham Neubig},
      year={2024},
      eprint={2407.16741},
      archivePrefix={arXiv},
      primaryClass={cs.SE},
      url={https://arxiv.org/abs/2407.16741},
}
```