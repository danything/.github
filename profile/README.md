<div align="center">

# Doa（ドゥエー）

自宅のk3sクラスタと、その上で動かしているものの置き場。

[![Website](https://img.shields.io/badge/doany.io-000000?style=for-the-badge&logo=astro&logoColor=white)](https://doany.io)
[![Blog](https://img.shields.io/badge/Blog-FF5D01?style=for-the-badge&logo=rss&logoColor=white)](https://doany.io/archive/)
[![Contact](https://img.shields.io/badge/info@doany.io-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:info@doany.io)

📍 Japan

</div>

---

## About

個人で運用している自宅のk3sクラスタと、そこで動かしているアプリを公開しています。

構成はArgoCDのGitOpsに寄せていて、マニフェストをpushすればクラスタに反映されます。ハマったことや調べたことは[doany.io](https://doany.io)に書いています。

- k3s + ArgoCD + Traefik + Infisical
- 古い業務システムもDocker / Helm chartにして載せる
- GitHub ActionsでビルドしてGHCRにpush、ArgoCDがデプロイ
- 記事はインフラ・Web・決済・車など

## Products

### worklog（[w.doany.io](https://w.doany.io)）

先月の稼働表を、今から作れます。

普段使っているSlack・GitHub・GitLab・Backlog・Jira・OpenProject・Redmineの記録から、日別の稼働開始・終了・休憩・実働を組み立てます。

- PCに常駐ツールを入れません
- 過去の月にさかのぼって作れます
- 使っているサービスを連携して、月を選ぶだけです
- ログインはGitHubアカウントです

> 早期利用期間中は全機能を無料で開放しています。正式リリース後も今月と先月の分は無料で、全期間さかのぼれるProが月額1,200円（税別）です。

[今すぐ試す](https://w.doany.io)・お問い合わせは[info@doany.io](mailto:info@doany.io)

### 新規サービス（準備中）

中古車を型式から探せるサービスを考えています。まずは土台になる車両マスター（型式→通称名・製作者・諸元・販売期間）を、燃費一覧・官報の型式指定・リコール届出などの公的データから作っているところです。

続報は[doany.io](https://doany.io)に書きます。

## Repositories

### インフラ/ホームラボ

| Repository | 概要 |
| --- | --- |
| [**k3s-gitops**](https://github.com/danything/k3s-gitops) | k3s上のセルフホストアプリ（AdGuard Home、Cloudflare DDNS、ERPNext、Mattermost、Portainer、WireGuard、3proxy）のマニフェスト。ArgoCDで同期 |
| [**helm-mosp**](https://github.com/danything/helm-mosp) | 勤怠管理[MosP](https://github.com/es-mind/MosP)のDockerイメージとHelm chart。毎月、最新コミットを自動でビルドしてGHCRに置く |
| [**genkan**](https://github.com/danything/genkan) | compose.yml 1枚のリバースプロキシ。ローカルの`*.localhost`も本番のドメインも同じ設定で振り分ける |
| [**infisical-push-bridge**](https://github.com/danything/infisical-push-bridge) | セルフホストのInfisical（無料版）で、Webhookを受けて`InfisicalSecret`をその場で同期させる。Helm chartあり |

> [!NOTE]
> クラスタの初期構築（k3s、Traefik、ArgoCD、Infisical、認証、StorageClass、バックアップ）は非公開のリポジトリにあります。ここに並べたのはその上に載せるアプリ側のマニフェストで、各リポジトリの`k3s/argocd.yaml`をApplicationSetが拾ってApplicationを作ります。

### アプリケーション

| Repository | 概要 |
| --- | --- |
| [**denpa**](https://github.com/danything/denpa) | 自宅に置くテレビ録画サーバ。番組表から予約して、録ったものも放送中のものもブラウザで観る。チューナー側はエージェントに分けてあり、Docker / Kubernetes用のイメージをGHCRで配布 |
| [**denpa-agent-windows**](https://github.com/danything/denpa-agent-windows) | denpaのチューナーエージェントのWindows版。BonDriverで選局して、Linux版と同じHTTPでTSを返す。C#のNative AOT |
| [**blog**](https://github.com/danything/blog) | [doany.io](https://doany.io)のソース。[Fuwari](https://github.com/saicaca/fuwari)ベースのAstro製ブログ。検索はPagefind、コメントはyosegaki |
| [**yosegaki**](https://github.com/danything/yosegaki) | SvelteKit + Bun + SQLiteのコメントサーバ。scriptタグ1つで埋め込めて、管理画面は無い |
| [**aizuchi**](https://github.com/danything/aizuchi) | Slackで相槌を打つAIボット。コネクタとLLMプロバイダを差し替えられる.NET Native AOTの器で、Helm chart付き |
| [**xool**](https://github.com/danything/xool) | [x.doany.io](https://x.doany.io)。𝕏の前日のポストを集計して、通信簿として自動でポストする |
| [**lgtm**](https://github.com/danything/lgtm) | [l.doany.io](https://l.doany.io)。画像を放り込むとLGTMを敷き詰めたwebpにして、貼り付け用のMarkdownを返す |
| [**yuzuriha**](https://github.com/danything/yuzuriha) | [y.doany.io](https://y.doany.io)。0円物件を掲載サイトから集めて、衛星写真の地図に載せる |

## Tech Stack

<div align="center">

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![k3s](https://img.shields.io/badge/k3s-FFC61C?style=flat-square&logo=k3s&logoColor=black)
![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?style=flat-square&logo=argo&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=flat-square&logo=helm&logoColor=white)
![Traefik](https://img.shields.io/badge/Traefik-24A1C1?style=flat-square&logo=traefikproxy&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Renovate](https://img.shields.io/badge/Renovate-1A1F6C?style=flat-square&logo=renovate&logoColor=white)

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Svelte](https://img.shields.io/badge/Svelte-FF3E00?style=flat-square&logo=svelte&logoColor=white)
![Astro](https://img.shields.io/badge/Astro-BC52EE?style=flat-square&logo=astro&logoColor=white)
![Bun](https://img.shields.io/badge/Bun-000000?style=flat-square&logo=bun&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![Biome](https://img.shields.io/badge/Biome-60A5FA?style=flat-square&logo=biome&logoColor=white)
![C#](https://img.shields.io/badge/C%23-512BD4?style=flat-square&logo=dotnet&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)
![Caddy](https://img.shields.io/badge/Caddy-1F88C0?style=flat-square&logo=caddy&logoColor=white)
![Shell](https://img.shields.io/badge/Shell-4EAA25?style=flat-square&logo=gnubash&logoColor=white)

</div>

---

<div align="center">

**[doany.io](https://doany.io)**・[info@doany.io](mailto:info@doany.io)

</div>
