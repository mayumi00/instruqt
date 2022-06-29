---
slug: 06-deploying-using-the-command-line
id: kvp4frjsoqvh
type: challenge
title: Topic 6 - Deploying the application from the command line
difficulty: basic
timelimit: 900
---
このトピックでは、 `oc`コマンドを使用して、以前にWebコンソールを使用してデプロイしたアプリケーションを、再度デプロイします。

# コマンドラインツールを使用してのアプリケーションのデプロイ

`Step 1:` 次のコマンドを実行してアプリケーションをデプロイします。

```
oc new-app python:latest~https://github.com/openshift-instruqt/blog-django-py
```

次のような出力が表示されます。

```
--> Found image f813306 (5 months old) in image stream "openshift/python" under tag "latest" for "python:latest"

    Python 3.9
    ----------
    Python 3.9 available as container is a base platform for building and running various Python 3.9 applications and frameworks. Python is an easy to learn, powerful programming language. It has efficient high-level data structures and a simple but effective approach to object-oriented programming. Python's elegant syntax and dynamic typing, together with its interpreted nature, make it an ideal language for scripting and rapid application development in many areas on most platforms.

    Tags: builder, python, python39, python-39, rh-python39

    * A source build using source code from https://github.com/openshift-instruqt/blog-django-py will be created
      * The resulting image will be pushed to image stream tag "blog-django-py:latest"
      * Use 'oc start-build' to trigger a new build

--> Creating resources ...
    imagestream.image.openshift.io "blog-django-py" created
    buildconfig.build.openshift.io "blog-django-py" created
    deployment.apps "blog-django-py" created
    service "blog-django-py" created
--> Success
    Build scheduled, use 'oc logs -f buildconfig/blog-django-py' to track its progress.
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/blog-django-py'
    Run 'oc status' to view your app.
```

OpenShiftは、ソースコードをホストするGitリポジトリの名前に基づいてアプリケーションのデフォルト名を割り当てます。

Webアプリケーションを含むGitリポジトリのURLは次のとおりです。 `https://github.com/openshift-instruqt/blog-django-py`

この場合、アプリケーションの名前は`blog-django-py`です。名前を変更したい場合は、名前を引数とする``--name``オプションを使用して指定する事ができます。

# アプリケーションのモニタ

`Step 2:` 次のコマンドを実行すると、ビルドの実行中にビルドのログ出力をモニタすることができます。

```
oc logs bc/blog-django-py --follow
```

このコマンドは、ビルドが完了すると終了します。ターミナルウィンドウで `CTRL+C` と入力して、コマンドを中断することもできます。

----

`Step 3:` 次のコマンドを実行して、projectにデプロイされているアプリケーションのステータスを表示します。

```
oc status
```

アプリケーションのビルドとデプロイが完了すると、次のような出力が表示されます。

```
root@container:/# oc status
In project myproject on server https://api.crc.testing:6443

svc/blog-django-py - 10.217.5.34:8080
  deployment/blog-django-py deploys istag/blog-django-py:latest <-
    bc/blog-django-py source builds https://github.com/openshift-instruqt/blog-django-py on openshift/python:latest
    deployment #2 running for about a minute - 1 pod
    deployment #1 deployed 2 minutes ago


1 info identified, use 'oc status --suggest' to see details.
```
----

Webコンソールからアプリケーションをデプロイする場合とは異なり、アプリケーションはデフォルトではOpenShiftクラスタの外部に公開されません。

`Step 4:` 次のコマンドを実行して、OpenShiftクラスタの外部にアプリケーションを公開します。

```
oc expose service/blog-django-py
```

次のような出力が得られます。

```
route.route.openshift.io/blog-django-py exposed
```

----



URLにアクセスするためのアイコンは、ビジュアライゼーションに引き続き表示されます。または、コマンドラインから作成されたルートに割り当てられたホスト名を表示するには、次のコマンドを実行します。


`Step 5:` アプリケーションがデプロイされ、インターネット経由でアクセスできることを確認するには、左側のターミナルウィンドウの横にある **Web Console** タブを選択してWebコンソールに切り替えます。次に、Webコンソールの左上にある **Topology** タブをクリックします。

Pythonアプリケーションを表す円形のグラフィックが表示されます。

ただし、Topology viewの視覚化では、ビルドおよびソースコードリポジトリに対応するアイコンが表示されないことに注意してください。これは、Webコンソールからアプリケーションを作成するときに、デプロイメントに追加された特別なアノテーションとラベルに依存しているためです。これらの注アノテーションは、コマンドラインからアプリケーションを作成するときには自動的に追加されません。必要に応じて、後でアノテーションを追加できます。

URLにアクセスするためのアイコンは、視覚化したものに、引き続き表示されます。または、コマンドラインから作成されたrouteに割り当てられたホスト名を表示するには、次のコマンドを実行します。

```
oc get route/blog-django-py
```

次のような出力が得られます。

```
NAME             HOST/PORT                                                                  PATH   SERVICES         PORT       TERMINATION   WILDCARD
blog-django-py   blog-django-py-myproject.crc-gh9wd-master-0.crc.pfrbfxh9ypu7.instruqt.io          blog-django-py   8080-tcp                 None
```

# Congratulations!

`oc` コマンドを使用して、削除されたアプリケーションを再度デプロイしました。

----

**NEXT:** コマンドラインから新しいビルドをトリガーする。