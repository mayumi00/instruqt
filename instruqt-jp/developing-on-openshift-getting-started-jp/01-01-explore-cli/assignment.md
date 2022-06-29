---
slug: 01-explore-cli
id: pihsfi9zczhn
type: challenge
title: Topic 1 - Getting started with OpenShift
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
timelimit: 900
---
# コマンドラインインターフェース (CLI)を使用する

`oc`コマンドを使用してOpenShiftのコマンドラインインターフェースにアクセスします。`oc`コマンドを使用すると、OpenShiftクラスタ全体を操作して、新しいアプリケーションをデプロイすることができます。

Kubernetesに慣れているユーザーはOpenShiftにもすぐに適応できるようになります。`oc`はKubernetesの `kubectl` ツールのすべての機能を提供します。さらに、 `oc`を使用すると、OpenShiftの操作が簡単になります。 CLIは、次のような状況で理想的です。

* プロジェクトのソースコードを直接操作する
* OpenShift操作をスクリプトにする
* リソース帯域幅の制限により、Webコンソールの使用ができない場合

まず`oc`コマンドでログインすることから始めます。

# CLIを使用してログインする

`oc login`コマンドを使用してOpenShiftクラスタにログインします。
----

`Step 1:` 左側のターミナルウィンドウで次のコマンドを実行します。下のコマンドラインをクリックすると、クリップボードにコピーされます。コピーされた内容を、左側のターミナルにペーストしてください。

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

これはパスワードが`admin`である`admin`というユーザーで、OpenShiftクラスタのAPIサーバーにログインすることを意味しています。ログインに成功すると、次のような結果が表示されます。

```
Login successful.

You have access to 64 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "default".
```

Linuxの[`whoami`](https://en.wikipedia.org/wiki/Whoami)コマンドを実行すると、現在のユーザーとログインが成功したことがわかります。`oc`コマンドでも似たようなコマンドがあります。

----

`Step 2:` 次のコマンドを実行します。

```
oc whoami
```

次のような結果が表示され、現在`admin`ユーザーであることがわかります。

```
admin
```

# Congratulations!

`oc`コマンドラインツールを使用して、OpenShiftクラスタにログインすることができました。

----

**NEXT:** **Webコンソール** を使用して最初のプロジェクトを作成します。
