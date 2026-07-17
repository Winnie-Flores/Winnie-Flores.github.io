---
title: ChatGPT 苹果充值与 Codex 登录（踩坑解疑）
date: 2026-07-18 01:10:00
updated: 2026-07-18 01:10:00
tags:
  - ChatGPT
  - Codex
  - Apple ID
categories:
  - 工具笔记
---

> 本文记录我在没有海外电话卡和海外银行卡的情况下，为 ChatGPT 订阅充值并登录 Codex 时遇到的问题。界面、价格、方案权益和地区政策都可能变化，请以 Apple 与 OpenAI 的最新官方说明为准。

## 1. 背景说明

开始探索 ChatGPT 时，我的 Apple ID、Google、ChatGPT 和 Codex 账号使用得比较混乱，导致充值、登录和使用过程中遇到了不少问题。这里整理一下亲自踩过的坑，以及最后可用的解决方案。

我的环境：

- 系统：macOS Sequoia 15.7.3
- 浏览器：Chrome
- 支付方式：支付宝购买 Apple 礼品卡
- ChatGPT：Chrome 网页端登录
- Codex：桌面应用与 CLI

## 2. 注册与账号统一

建议从一开始就确认以下账号之间的对应关系，并尽量保持统一：

1. 浏览器里正在使用的 ChatGPT 账号；
2. 手机 ChatGPT App 登录的账号；
3. Codex 登录时选择的 ChatGPT 账号；
4. 用于 App Store 付款的 Apple ID。

我最初使用 QQ 邮箱注册 Google，后来又换成 Gmail；ChatGPT 网页端则直接使用 Google 登录。账号过多会让后续排查订阅归属和登录状态变得很麻烦。

## 3. 通过 Apple 礼品卡订阅

以下是我的个人操作记录，不代表所有地区和时间都适用。

### 3.1 注册美区 Apple ID

我先在 iPhone 的“设置 → 通用 → 语言与地区”中将地区切换为美国，然后通过 Apple 官网注册美区 Apple ID。注册时地区需要保持一致，地址等信息应真实、合规并自行妥善保存。

以前将国区账号切换到美区后再切回，后来再次切换时无法跳过付款方式，所以我最终采用了单独注册美区账号的方式。不要频繁切换主账号地区，购买内容、订阅和可用 App 可能受到影响。

### 3.2 下载 ChatGPT App

在 App Store 中退出原账号，登录美区 Apple ID，下载官方 ChatGPT App。打开 App 后，需要登录与网页端相同的 ChatGPT 账号，避免订阅出现在另一个账号下。

### 3.3 购买并兑换 Apple 礼品卡

我的流程是：

1. 在支付宝中找到可用的境外 Apple 礼品卡服务；
2. 按准备订阅的金额购买礼品卡；
3. 在 App Store 右上角进入账号页面；
4. 选择“兑换充值卡或代码”，输入兑换码；
5. 回到 ChatGPT App，在订阅页面通过 Apple ID 余额付款。

礼品卡面额、税费、ChatGPT 价格和可购买地区都会变化，付款前务必核对币种、Apple ID 地区和实际扣款金额。不要在非可信页面提交兑换码。

## 4. Codex 安装与登录

Codex 的可用方案与使用额度会调整，不要再把“必须是 Plus 才能使用”当作固定规则。请查看 [OpenAI 关于使用 ChatGPT 方案访问 Codex 的说明](https://help.openai.com/en/articles/11369540-using-codex-with-your-chatgpt-plan)。

### 4.1 安装 Codex CLI

先检查 Node.js 与 npm：

```bash
node -v
npm -v
```

如果尚未安装 Node.js，可以通过 Homebrew 安装：

```bash
brew install node
```

安装或更新官方 Codex CLI：

```bash
npm install -g @openai/codex
```

验证安装：

```bash
which codex
codex --version
```

官方入门说明可参考：[OpenAI Codex CLI – Getting Started](https://help.openai.com/en/articles/11096431)。

### 4.2 出现 `command not found: codex`

先查看 npm 的全局安装目录：

```bash
npm prefix -g
```

如果其 `bin` 目录没有进入 PATH，可将下面一行加入 `~/.zshrc`：

```bash
export PATH="$(npm prefix -g)/bin:$PATH"
```

随后重新加载配置：

```bash
source ~/.zshrc
hash -r
```

### 4.3 使用官方登录流程

正常情况下直接运行：

```bash
codex
```

然后根据提示使用 ChatGPT 账号登录。如果以前使用过 API Key 或错误账号，可以先退出：

```bash
codex logout
```

浏览器登录不顺利时，当前 CLI 也提供设备码登录：

```bash
codex login --device-auth
```

终端会显示设备授权地址和一次性代码，按页面提示完成授权即可。

> 不建议安装来源不明的浏览器插件来提取 ChatGPT 登录信息，也不要复制、分享或手动导入他人生成的 `auth.json`。其中可能包含可用于访问账号的敏感凭证。

## 5. 常见问题

### 5.1 `Your access token could not be refreshed`

这通常表示本地凭证过期、登录账号不一致或授权流程没有完整结束。可以依次尝试：

```bash
codex logout
npm install -g @openai/codex
codex login --device-auth
```

登录时确认浏览器中选择的是正确的 ChatGPT 账号。仍然失败时，记录完整报错和 `codex --version`，再根据官方帮助排查。

### 5.2 对话频繁重新连接

我遇到过一次请求连续重连的问题，最终发现与本地网络代理配置有关。可以先检查代理软件是否正常、终端是否继承了错误的代理变量，以及代理端口是否与当前软件设置一致。

如果确实需要为终端配置代理，可以在当前终端临时设置；下面的端口仅为示例：

```bash
export HTTP_PROXY=http://127.0.0.1:7890
export HTTPS_PROXY=http://127.0.0.1:7890
export ALL_PROXY=socks5://127.0.0.1:7890
export NO_PROXY=localhost,127.0.0.1
```

不要盲目把代理配置永久写入系统文件。先确认临时配置有效，并确保遵守所在地区和网络服务的规则。

## 6. 最后总结

这次最大的经验不是某一条命令，而是：

1. 尽量统一 ChatGPT 网页端、App 和 Codex 使用的账号；
2. 付款前确认 Apple ID 地区、币种和订阅归属；
3. 优先使用 Codex 官方登录流程；
4. 不要通过第三方工具导出或传递登录凭证；
5. 遇到问题先记录版本、完整报错和当前网络环境，再逐项排查。

希望这份踩坑记录能帮你少绕一些弯路。
