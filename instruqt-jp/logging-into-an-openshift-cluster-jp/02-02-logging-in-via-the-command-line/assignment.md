---
slug: 02-logging-in-via-the-command-line
id: wfcbavusacy3
type: challenge
title: Topic 2 - Logging in via the Command Line
tabs:
- title: Terminal 1
  type: terminal
  hostname: crc
- title: Web Console
  type: website
  hostname: crc
  url: https://console-openshift-console.crc-dzk9v-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: Visual Editor
  type: code
  hostname: crc
  path: /root
difficulty: basic
timelimit: 900
---
このトピックでは、`oc login`コマンドを利用して、ターミナルからOpenShiftクラスタにログインする方法を学習します。

# コマンドラインからのOpenShiftクラスタへのログイン

`Step 1:`  `-u` オプションでユーザ名を、  `-p` プションでユーザのパスワードを指定して、次のコマンドを実行してOpenShiftクラスタにログインします。

```
oc login -u developer -p developer
```

次のような出力が表示されます：

```
Login successful.

You don't have any projects. You can try to create a new project, by running

    oc new-project <projectname>
```

# プロジェクトでの作業

`Step 2:` 次のコマンドを実行してプロジェクトのnamespaceである`myproject`に移動します。前のトピックで、Webコンソールを利用してプロジェクト`myproject`を作成済みです：

```
oc project myproject
```

次のような出力が表示されます：

```
Already on project "myproject" on server "https://api.crc.testing:6443".
```

----

`Step 3:` 次のコマンドを実行して、現在アクセスできるプロジェクト一覧を表示します。:

```
oc get projects
```

次のような出力が表示されます：

```
NAME        DISPLAY NAME   STATUS
myproject   myproject      Active
```
----

`Step 4:` 次のコマンドを実行して、現在ログインしているユーザを確認します：

```
oc whoami
```

次の出力が表示されます。この場合、ユーザは `developer`です：

```
developer
```

----

`Step 5:` 次のコマンドを実行して、ログインしているサーバを確認します：

```
oc whoami --show-server
```
次の出力が表示されます。

```
https://api.crc.testing:6443
```

IDプロバイダーとして、外部認証サービスを利用している場合は、ログインの手順は少し異なります。（このトピックでは実施しません）

ユーザ名 (`-u`) とパスワード  (`-p`) オプションを指定せずに`oc login`でログインすると、次のようなエラーが発生し、認証サーバへ向けられます:

```
You must obtain an API token by visiting https://oauth-openshift.crc-dzk9v-master-0.crc.d9avlfzludvk.instruqt.io/oauth/token/request
```

API tokenを取得すると、認証サーバの認証プロセスに従ってユーザのログインクレデンシャルを受け取ります。認証サーバからログイン情報を取得したら、ターミナルに戻り、ログインクレデンシャルを使って`oc login`を実行します。

# Congratulations!

コマンドラインからOpenShiftクラスタにログインする方法を学習しました

----

**NEXT:** 他のユーザとの共同作業について学習します。
