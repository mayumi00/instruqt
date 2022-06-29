---
slug: 04-switching-between-accounts
id: i6fihe0qgoq4
type: challenge
title: Topic 4 - Switching Users Between Accounts
difficulty: basic
timelimit: 900
---
このトピックでは、 `oc login` コマンドを用いて、OpenShiftユーザーアカウント間を移動する方法を学習します。

`oc`コマンドラインツールを使用すると、一度に1つのOpenShiftクラスタとのみ対話できます。

したがって、1つのローカルユーザーとしてコンピューター上で別のシェルを開き、別のOpenShiftクラスタで作業することはできません。 これは、現在のログインセッションに関する状態が、`oc`コマンドを実行しているローカルユーザーのホームディレクトリに保存されているためです。

複数のOpenShiftクラスタに対して作業する必要がある場合、または同じOpenShiftクラスタ上の異なるユーザーとして作業する必要がある場合は、特定のユーザのログインコンテキストに切り替える必要があります。

このトラックでは、元々、`developer`ユーザーとして`oc login`を使用してコマンドラインからログインしました。 次のトピックでは、`user1`ユーザーとしてログインしました。

この時点では、まだログインしていて、両方のユーザーのアクティブなセッショントークンがありますが、現在は`user1`ユーザーとして操作しています。

----

`Step 1:` 次のコマンドをターミナルで実行して、`developer`ユーザに切り替えます：

```
oc login --username developer
```

次のような出力が表示されます:

```
Logged into "https://api.crc.testing:6443" as "developer" using existing credentials.

You have one project on this server: "myproject"

Using project "myproject".
```

前回のログイン時にパスワードを入力したため、`developer`のパスワードを入力する必要はありません。

OpenShift `oc` CLIツールは、ログイン情報をローカルマシンに保存します。 パスワードの入力または新しいセッショントークンの入力を求められるのは、アクティブなセッションの有効期限が切れたときだけです。

You don't need to provide a password for the user named `developer` because you provided the password during your previous login.

----

`Step 2:` 次のコマンドを実行して、`developer`であることを確認します：
```
oc whoami
```

次のような出力が表示されます:

```
developer
```

複数のOpenShiftクラスタに対して作業している場合は、`oc login`を使用してクラスタを切り替えます。 OpenShiftクラスタのURLを指定するだけで済みます。 たとえば、[Developer Sandbox for OpenShift][Developer Sandbox for OpenShift](https://developers.redhat.com/developer-sandbox)のアカウントを持っている場合は、次のように実行できます。

```
oc login --token=<token> --server=https://api.sandbox-m2.ll9k.p1.openshiftapps.com:6443
```

OpenShiftクラスタを切り替えるときに、使用するユーザを明示的に指定しない場合、OpenShiftはクラスタに最後にログインしたユーザを使用します。 必要に応じて、`--username`を指定できます。

各ユーザの詳細はコンテキストに個別に保存されるため、パスワードを入力したりトークンを登録したりせずにユーザを切り替えることができます。

次のコマンドを実行して、現在のコンテキストを表示します。：


```
oc whoami --show-context
```

次のような出力が表示されます:

```
myproject/api-crc-testing:6443/developer
```

----

`Step 3:` 次のコマンドを実行して、ログインしているOpenShiftクラスタの一覧を表示します：

```
oc config get-clusters
```

次のような出力が表示されます:

```
myproject/api-crc-testing:6443/developer
```

----

`Step 4:` 次のコマンドを実行して、これまでに作成されたすべてのコンテキストの一覧を取得します：

```
oc config get-contexts
```

次のような出力が表示されます:

```
[root@crc-dzk9v-master-0 /]# oc config get-contexts
CURRENT   NAME                                         CLUSTER                AUTHINFO                         NAMESPACE
          /api-crc-testing:6443/user1                  api-crc-testing:6443   user1/api-crc-testing:6443
          admin                                        crc                    admin
          myproject/api-crc-testing:6443/developer     api-crc-testing:6443   developer/api-crc-testing:6443   myproject
*         yourproject/api-crc-testing:6443/developer   api-crc-testing:6443   developer/api-crc-testing:6443   yourproject
          yourproject/api-crc-testing:6443/user1       api-crc-testing:6443   user1/api-crc-testing:6443       yourproject
```

多数のコンテキストが表示されます。

# Congratulations!

  `oc login` コマンドでOpenShiftクラスタでのユーザの切り替えを行い、コンテキスト情報を取得する方法を学習しました。

----

これでこのトラックの最後のトピックになります。