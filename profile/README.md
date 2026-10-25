<div align="center">

# Doa（ドゥエー）

自宅のKubernetesクラスタ（Talos Linux）と、その上で動かしているものの置き場。

[![Website](https://img.shields.io/badge/doany.io-000000?style=for-the-badge&logo=astro&logoColor=white)](https://doany.io)
[![Blog](https://img.shields.io/badge/Blog-FF5D01?style=for-the-badge&logo=rss&logoColor=white)](https://b.doany.io)
[![Contact](https://img.shields.io/badge/Contact-EA4335?style=for-the-badge)](https://doany.io/contact/)

📍 Japan

</div>

---

## About

Doaは個人事業の屋号です。事業内容・自社サービス・実績は[doany.io](https://doany.io)に、ハマったことや調べたことは[ブログ](https://b.doany.io)に書いています。ここには、そのソースと自宅のクラスタを公開しています。

構成はArgo CDのGitOpsに寄せていて、マニフェストをpushすればクラスタに反映されます。

- Talos Linux（1ノード）+ Argo CD + Cilium（Gateway API）+ Infisical。ノードの設定もgitで持ち、Cloudflare・Entra ID・NetBirdの設定はPulumiで持つ
- 古い業務システムもDocker / Helm chartにして載せる
- 公開リポジトリはGitHub ActionsでビルドしてGHCRへ、非公開のものは自宅の[Forgejo](https://forgejo.org/)のActionsでビルドして同じForgejoのレジストリへ。どちらもArgo CDがデプロイ

## Services

| | |
| --- | --- |
| [**トドロク**](https://tk.doany.io) | 中古車店の台帳と帳簿と書類。車検証の2次元コードを読めば1台が登録され、期限のお知らせ・原価と利益・古物台帳・請求書・登録手続きの書類まで出せる |
| [**worklog**](https://w.doany.io) | 書かなくていい日報と稼働表。Slack・GitHub・Backlog・Jiraなどの活動ログから、日報と月末の稼働表の下書きを作る |
| [**tama 車両カタログ**](https://ts.doany.io) | 日本で型式指定を受けた自動車2万型式超のカタログ。諸元・燃費・販売期間・官報の型式指定・リコール届出を横断検索。トドロクの車両マスターでもある |

> [!NOTE]
> これらのソースは、自宅の[Forgejo](https://forgejo.org/)にある非公開のリポジトリです。Argo CDのApplicationSetがGitHubとForgejoの両方のリポジトリを走査し、各リポジトリの`deploy/argocd.yaml`を見つけてApplicationを作ります。

## Repositories

### インフラ/ホームラボ

| Repository | 概要 |
| --- | --- |
| [**gitops**](https://github.com/danything/gitops) | 自宅のクラスタのマニフェスト。セルフホストのアプリ（Forgejo、Matrix、AdGuard Home、NetBird、Headlamp、Infisical、Rybbit、Renovate、k8up、external-dns、Cloudflare DDNS、SMTPリレー、3proxy）と、クラスタを組む層（Talosのmachine config、Argo CD、Cilium Gateway、cert-manager、Entra IDの認証）。PulumiのCloudflare・Entra・NetBird、restic → R2のバックアップと建て直しの手順も |
| [**mado**](https://github.com/danything/mado) | OIDCでログインして、ブラウザからRDPする小さなゲートウェイ。.NETのWindowsサービスとタスクトレイをMSIで入れ、署名を確かめて自分で更新する。クラスタが落ちたときの入口にも使っている |
| [**helm-mosp**](https://github.com/danything/helm-mosp) | 勤怠管理[MosP](https://github.com/es-mind/MosP)のDockerイメージとHelm chart。毎月、最新コミットを自動でビルドしてGHCRに置く |
| [**genkan**](https://github.com/danything/genkan) | compose.yml 1枚のリバースプロキシ。ローカルの`*.localhost`も本番のドメインも同じ設定で振り分ける |
| [**infisical-push-bridge**](https://github.com/danything/infisical-push-bridge) | セルフホストのInfisical（無料版）で、Webhookを受けて`InfisicalSecret`をその場で同期させる。Helm chartあり |
| [**wslc-compose**](https://github.com/danything/wslc-compose) | `compose.yaml`をWSLコンテナ（`wslc`）で動かす。docker composeのよく使う範囲を依存クレートなしのRustで。wingetで入る |

### アプリケーション

| Repository | 概要 |
| --- | --- |
| [**denpa**](https://github.com/danything/denpa) | チューナーを挿すだけで動くテレビ録画サーバ。設定ファイルは書かず、番組表から予約して、録画もライブも字幕・データ放送つきでブラウザで観る。CMは自動で飛ばす。Linux・Mac・Windows・Kubernetes |
| [**denpa-tv**](https://github.com/danything/denpa-tv) | denpaをAndroid TV / Google TVで観るアプリ。Jetpack Compose for TV |
| [**denpa-font**](https://github.com/danything/denpa-font) | 字幕・データ放送・番組表向けの等幅の丸ゴシック。BIZ UDゴシックの角を丸め、ARIBの記号を描き足したもの（OFL） |
| [**corp**](https://github.com/danything/corp) | [doany.io](https://doany.io)のソース。Astro + [Blades](https://blades.dev/)の静的なページを、お問い合わせを受ける小さなBunのサーバーが配信する |
| [**blog**](https://github.com/danything/blog) | [b.doany.io](https://b.doany.io)のソース。[Fuwari](https://github.com/saicaca/fuwari)ベースのAstro製ブログ。検索はPagefind、コメントはyosegaki |
| [**yosegaki**](https://github.com/danything/yosegaki) | SvelteKit + Bun + SQLiteのコメントサーバ。scriptタグ1つで埋め込めて、管理画面は無い。どのコメント欄からでもサイト全体の新着と自分宛ての返信が見える |
| [**ashi**](https://github.com/danything/ashi) | AIに、足を。話しかけられなくても自分で問いを選んで調べ、ノートと日記を残して休むAI。頭はClaude API、足（ループ・予算・ガードレール）はSvelteKit + Bun |
| [**aizuchi**](https://github.com/danything/aizuchi) | チャットで相槌を打つAIボット。コネクタ（Slack）・LLMプロバイダ（Claude）・道具（GitHub、OpenProjectなど）を差し替えられる.NET Native AOTの器で、Helm chart付き |
| [**xool**](https://github.com/danything/xool) | [x.doany.io](https://x.doany.io)。𝕏の前日のポストを集計して、通信簿として自動でポストする |
| [**lgtm**](https://github.com/danything/lgtm) | [l.doany.io](https://l.doany.io)。画像を放り込むとLGTMを敷き詰めたwebpにして、貼り付け用のMarkdownを返す |
| [**yuzuriha**](https://github.com/danything/yuzuriha) | [y.doany.io](https://y.doany.io)。0円物件を掲載サイトから集めて、衛星写真の地図に載せる |

## Tech Stack

<div align="center">

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Talos Linux](https://img.shields.io/badge/Talos%20Linux-FF7300?style=flat-square&logo=talos&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?style=flat-square&logo=argo&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=flat-square&logo=helm&logoColor=white)
![Cilium](https://img.shields.io/badge/Cilium-F8C517?style=flat-square&logo=cilium&logoColor=black)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Forgejo](https://img.shields.io/badge/Forgejo-FB923C?style=flat-square&logo=forgejo&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Renovate](https://img.shields.io/badge/Renovate-1A1F6C?style=flat-square&logo=renovate&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat-square&logo=cloudflare&logoColor=white)
![Pulumi](https://img.shields.io/badge/Pulumi-8A3391?style=flat-square&logo=pulumi&logoColor=white)

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Svelte](https://img.shields.io/badge/Svelte-FF3E00?style=flat-square&logo=svelte&logoColor=white)
![Astro](https://img.shields.io/badge/Astro-BC52EE?style=flat-square&logo=astro&logoColor=white)
![Bun](https://img.shields.io/badge/Bun-000000?style=flat-square&logo=bun&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white)
![Oxlint](https://img.shields.io/badge/Oxlint-32F3E9?style=flat-square&logo=oxc&logoColor=black)
![C#](https://img.shields.io/badge/C%23-512BD4?style=flat-square&logo=dotnet&logoColor=white)
![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=flat-square&logo=kotlin&logoColor=white)
![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-635BFF?style=flat-square&logo=stripe&logoColor=white)
![Caddy](https://img.shields.io/badge/Caddy-1F88C0?style=flat-square&logo=caddy&logoColor=white)
![Shell](https://img.shields.io/badge/Shell-4EAA25?style=flat-square&logo=gnubash&logoColor=white)

</div>

---

<div align="center">

**[doany.io](https://doany.io)**・[ブログ](https://b.doany.io)・[お問い合わせ](https://doany.io/contact/)

</div>
