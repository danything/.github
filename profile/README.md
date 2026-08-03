<div align="center">

# Doa（ドゥエー）

**気ままな備忘録 — 自宅 k3s クラスタと、そこで動くものたち。**

[![Website](https://img.shields.io/badge/doany.io-000000?style=for-the-badge&logo=astro&logoColor=white)](https://doany.io)
[![Blog](https://img.shields.io/badge/Blog-FF5D01?style=for-the-badge&logo=rss&logoColor=white)](https://doany.io/archive/)
[![Contact](https://img.shields.io/badge/info@doany.io-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:info@doany.io)

📍 Japan

</div>

---

## About

個人で運用している自宅 Kubernetes（k3s）クラスタと、その上で動かしているアプリケーションを公開しています。

ホームラボの構成は **GitOps（ArgoCD）で全部リポジトリに寄せる**方針で、マニフェストを push すれば勝手に反映される状態を目指しています。日々の試行錯誤やハマりどころは [doany.io](https://doany.io) に記事として残しています。

- 🏗 **Infrastructure as Code** — k3s + ArgoCD + Traefik + Sealed Secrets
- 📦 **Containerize everything** — レガシーな業務システムも Docker / Helm chart 化
- 🤖 **Automate** — GitHub Actions で定期ビルド → GHCR へ push → ArgoCD がデプロイ
- ✍️ **Write it down** — Web・インフラ・決済まわり・車の話まで、備忘録として

## Products

### 📊 worklog — [w.doany.io](https://w.doany.io)

**インストール不要で、先月の稼働表を今から作れる。**

稼働表のために、毎日タイマーを押すのはもうやめませんか。
worklog は、普段使っている **Slack・GitHub・GitLab・Backlog・Jira・OpenProject・Redmine** の記録から、日別の稼働開始・終了・休憩・実働を自動で組み立てます。

- ⏱ **常駐ツールなし** — PC には何も入れません。入れ忘れも、押し忘れもありません
- ⏪ **過去にさかのぼれる** — 「先月分を今すぐ出したい」に、今日から間に合います
- 🔗 **つなぐだけ** — 使っているサービスを連携したら、あとは月を選ぶだけ
- 🔑 **GitHub アカウントでログイン** — 登録フォームはありません

> 🎁 **早期利用期間中につき、全機能を無料で開放しています。**（正式リリース後は月額 1,200円・税別）

[**▶ 今すぐ試す**](https://w.doany.io) ・ お問い合わせは [info@doany.io](mailto:info@doany.io)

### 🌱 新規サービス

**事業計画中。**

散らばっていて探しにくい情報を、探しやすい形に整えるサービスを構想しています。いまは調査と設計の段階です。

続報は [doany.io](https://doany.io) にて。

## Repositories

### インフラ / ホームラボ

| Repository | 概要 |
| --- | --- |
| [**k3s-gitops**](https://github.com/danything/k3s-gitops) | k3s クラスタ上のセルフホストアプリ群（AdGuard Home / ERPNext / Mattermost / Opengist / Portainer / VPN）を ArgoCD で管理 |
| [**helm-mosp**](https://github.com/danything/helm-mosp) | OSS 勤怠管理 [MosP](https://github.com/es-mind/MosP) の Docker イメージ化と Helm chart 配布。毎月最新コミットを自動ビルド |

> [!NOTE]
> クラスタ本体の初期構築（k3s のセットアップ、Traefik / ArgoCD / Sealed Secrets / 認証まわりのアドオン、StorageClass、バックアップ）は非公開のリポジトリで管理しています。上記の各リポジトリは、それが済んだクラスタに乗る**アプリ側のマニフェストのみ**を含みます。

### アプリケーション

| Repository | 概要 |
| --- | --- |
| [**denpa**](https://github.com/danything/denpa) | mirakc と 2 つだけで完結するテレビ録画アプリ。予約・録画・エンコード・配信を担い、メディアサーバは置かない。Docker / Kubernetes 用のイメージを GHCR で配布 |
| [**blog**](https://github.com/danything/blog) | [doany.io](https://doany.io) のソース。[Fuwari](https://github.com/saicaca/fuwari) ベースの Astro 製静的ブログ（Pagefind 検索 / remark42 コメント） |
| [**xool**](https://github.com/danything/xool) | [x.doany.io](https://x.doany.io) — Webhook から 𝕏 に投稿する API と、LGTM 画像の生成・ホスティング |

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
![Shell](https://img.shields.io/badge/Shell-4EAA25?style=flat-square&logo=gnubash&logoColor=white)

</div>

---

<div align="center">

**[doany.io](https://doany.io)** ・ [info@doany.io](mailto:info@doany.io)

</div>
