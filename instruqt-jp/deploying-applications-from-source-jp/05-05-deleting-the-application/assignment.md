---
slug: 05-deleting-the-application
id: ljlq5eps3zsy
type: challenge
title: Topic 5 - Deleting the application from the command line
difficulty: basic
timelimit: 900
---
このトピックでは、OpenShift `oc` コマンドラインを使用して、前のトピックでWebコンソールを使用して作成したアプリケーションを削除します。その後に、、`oc` を使用してコマンドラインからアプリケーションを再作成します。

# アプリケーションの削除

まず、OpenShiftクラスタで実行されているすべての基になるKubernetesリソースのリストを取得します。 OpenShiftは、Kubernetesクラスタ上で実行されるアーキテクチャーレイヤーと考えることができます。deployment、route、service accountなどのOpenShiftコンポーネントは、Kubernetesのリソースオブジェクトに対応します。

`Step 1:` 次のコマンドを実行して、OpenShiftクラスタで実行されている基になるKubernetesリソースの一覧を表示します。

```
oc get all -o name
```

これにより、次のような出力が表示されます。

```
pod/blog-django-py-1-build
pod/blog-django-py-64fb76b5c9-6hzhn
service/blog-django-py
deployment.apps/blog-django-py
replicaset.apps/blog-django-py-64fb76b5c9
replicaset.apps/blog-django-py-6c7f488b57
buildconfig.build.openshift.io/blog-django-py
build.build.openshift.io/blog-django-py-1
imagestream.image.openshift.io/blog-django-py
route.route.openshift.io/blog-django-py
```

作成したアプリケーションは1つだけなので、上記のリソースはすべてそのアプリケーションに関連しています。複数のアプリケーションをデプロイしている場合は、特定のアプリケーションに応じてリソースを識別し、特定のアプリケーションに対応するコンポーネントのみを削除する方法が必要です。

OpenShiftでリソースを特定のアプリケーションに関連付ける方法は、ラベルを使用することです。**label selector** を使用して、ラベルに従ってコンポーネントを取得します。

リソースには、ラベルなし、1つ、または複数のラベルを付けることができます。

You use the `oc describe` コマンドを使用して、ラベルを表示してリソースを精査します。
----

`Step 2:` 次のコマンドを実行して、`blog-django-py` という名前の `route` リソースの詳細を表示します。

```
oc describe route/blog-django-py
```

次のような出力が表示されます。

```
Name:                   blog-django-py
Namespace:              myproject
Created:                19 minutes ago
Labels:                 app=blog-django-py
                        app.kubernetes.io/component=blog-django-py
                        app.kubernetes.io/instance=blog-django-py
                        app.kubernetes.io/name=python
                        app.kubernetes.io/part-of=blog-django-py-app
                        app.openshift.io/runtime=python
                        app.openshift.io/runtime-version=3.6
Annotations:            openshift.io/host.generated=true
Requested Host:         blog-django-py-myproject.2886795320-80-simba02.environments.katacoda.com
                          exposed on router default (host apps-crc.testing) 19 minutes ago
Path:                   <none>
TLS Termination:        <none>
Insecure Policy:        <none>
Endpoint Port:          8080-tcp

Service:        blog-django-py
Weight:         100 (100%)
Endpoints:      10.128.0.65:8080
```
上記に表示された出力の４行目の `Labels:` 属性に注意してください。 `key-value` のペアとして記述された７つのラベルが表示されます。

```
app=blog-django-py
app.kubernetes.io/component=blog-django-py
app.kubernetes.io/instance=blog-django-py
app.kubernetes.io/name=python
app.kubernetes.io/part-of=blog-django-py-app
app.openshift.io/runtime=python
app.openshift.io/runtime-version=3.6
```

上記の出力の各行は、ラベルを説明しています。構造は`labelName=labelValue`です。従って、key-valueペアは次のようになります。。

```
app=blog-django-py
```

ラベルの名前は`app` で、値は `app=blog-django-py` です。

`oc` コマンドを使用して、ラベルに従ってリソースを取得できます。

----

`Step 3:` 以下のコマンドを実行して、key-valueペア　`app=blog-django-py` を持つすべてのリソースを取得します。

```
oc get all --selector app=blog-django-py -o name
```

次のような出力が表示されます。

```
pod/blog-django-py-7b98fb698b-vf6mb
service/blog-django-py
deployment.apps/blog-django-py
replicaset.apps/blog-django-py-7b98fb698b
replicaset.apps/blog-django-py-7fc8bdfb
buildconfig.build.openshift.io/blog-django-py
build.build.openshift.io/blog-django-py-1
imagestream.image.openshift.io/blog-django-py
route.route.openshift.io/blog-django-py
```

----

手順4：次のコマンドを実行して、ラベルペアapp=blogを持つリソースを取得します。

`Step 4:` 次のコマンドを実行してラベルペア `app=blog` を持つリソースを取得します。

```
oc get all --selector app=blog -o name
```

この場合、 `app=blog`　というラベルの付いたリソースが無いため、結果は空になります。

以前に、Webコンソールを使用してアプリケーションを作成した場合、ラベル `app=blog-django-py` をアプリケーションのすべてのリソースに自動的に適用しました。

ステップ5：次のコマンドを実行して、OpenShiftが自動的に適用したラベルを確認します。

----

`Step 5:` 次のコマンドを実行して、OpenShiftが自動的に適用したラベルを確認します。

```
oc get all --selector app=blog-django-py -o name
```

次のような出力が表示されます。

```
pod/blog-django-py-7b98fb698b-vf6mb
service/blog-django-py
deployment.apps/blog-django-py
replicaset.apps/blog-django-py-7b98fb698b
replicaset.apps/blog-django-py-7fc8bdfb
buildconfig.build.openshift.io/blog-django-py
build.build.openshift.io/blog-django-py-1
imagestream.image.openshift.io/blog-django-py
route.route.openshift.io/blog-django-py
```
----

ラベルを使用してリソースを選択すると、特定のアプリケーションに関連付けられているリソースを簡単に削除できます。

`Step 6:` 次のコマンドを実行して、以前にインストールしたPythonアプリケーションに関連付けられているすべてのリソースを削除します。

```
oc delete all --selector app=blog-django-py
```

次のような出力が表示されます。

```
pod "blog-django-py-7b98fb698b-vf6mb" deleted
service "blog-django-py" deleted
deployment.apps "blog-django-py" deleted
buildconfig.build.openshift.io "blog-django-py" deleted
build.build.openshift.io "blog-django-py-1" deleted
imagestream.image.openshift.io "blog-django-py" deleted
route.route.openshift.io "blog-django-py" deleted
```
----

`Step 7:` 次のコマンドを実行し、リソースが削除されたことを確認します。

```
oc get all --selector app=blog-django-py -o name
```

レスポンスは空です。

# Congratulations!

`oc` コマンドを利用して、アプリケーションを正常に削除しました。

----

**NEXT:** `oc` コマンドを使用して、アプリケーションをデプロイます。