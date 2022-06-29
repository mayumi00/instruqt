---
slug: playground
id: z2ijai6l4ehp
type: challenge
title: OpenShift Playground (Japanese)
notes:
- type: text
  contents: |
    ## Goal

    Explore OpenShift version 4.9.

    ## Concepts

    ## Use case

    You control an OpenShift cluster for one hour. You can deploy your own container image, or set up a pipeline to build your application from source, then monitor it with Prometheus as it runs. Use an Operator to deploy and manage a database backend for your web app.

    This OpenShift cluster will self-destruct in one hour (60 min)
tabs:
- title: Terminal 1
  type: terminal
  hostname: crc
- title: Web Console
  type: website
  url: https://console-openshift-console.crc-dzk9v-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: Visual Editor
  type: code
  hostname: crc
  path: /root
difficulty: basic
timelimit: 3600
---
この演習では決まった演習項目はありません。自由に利用してください。

---

## Webコンソールを利用してのクラスタへのログイン

Webコンソールを利用してログインします。スクリーンの上部の *Web Console* タブをクリックすることで可能です。`admin` ユーザとしてログインする場合は次のユーザ名とパスワードを利用します。

* **Username:** `admin`
* **Password:** `admin`

![Web Console Login](https://raw.githubusercontent.com/openshift-instruqt/instruqt/master/assets/middleware/pipelines/web-console-login.png)


また `developer` ユーザとしてログインすることもできます。その場合は、次のユーザ名とパスワードを利用します。

* **Username:** `developer`
* **Password:** `developer`
---

## Command Line Interfaceでのクラスターへのログイン

この環境では、はじめからクラスター管理者(admin)としてログインしています。次のコマンドで現行セッションでの情報を表示することができます。

```
oc whoami
```

アプリケーションを作成する前に、個別のユーザでログインすることをお勧めします（Webコンソールを利用する場合も同様です）。この例ではユーザ`developer`のパスワード`developer`を指定して、ターミナルからOpenShiftクラスタにログインします。

```
oc login -u developer -p developer
```

---

## 新しいProjectの作成

``myproject`` という名前の新しいProjectを作成するためには、次のコマンドを実行します。

```
oc new-project myproject
```
同様のことをWebコンソールからも行えます。