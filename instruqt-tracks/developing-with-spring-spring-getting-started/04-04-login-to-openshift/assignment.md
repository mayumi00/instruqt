---
slug: 04-login-to-openshift
id: asy4fupx9uzi
type: challenge
title: Step 4
tabs:
- title: Terminal 1
  type: terminal
  hostname: crc
- title: Visual Editor
  type: code
  hostname: crc
  path: /root/projects/rhoar-getting-started/spring/spring-rhoar-intro
- title: OpenShift Web Console
  type: website
  url: https://console-openshift-console.crc-lgph7-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: basic
timelimit: 600
---
# Login to OpenShift Container Platform

**Red Hat OpenShift Container Platform** is the preferred runtime for the **Red Hat Runtimes** like **Spring Boot**, **Vert.x** etc. The OpenShift Container Platform is based on **Kubernetes** which is a Container Orchestrator that has grown in popularity and adoption over the last years. **OpenShift** is currently the only container platform based on Kubernetes that offers multitenancy. This means that developers can have their own personal, isolated projects to test and verify application before committing to a shared code repository.

OpenShift also ships with a feature rich web console as well as command line tools to provide users with a friendly interface to work with applications deployed to the platform.

**1. Open the OpenShift Web Console**

OpenShift ships with a web-based console that will allow users to perform various tasks via a browser.

Click on `OpenShift Web Console` tab then, login using the following credentials from the Web using.

*Note* that you might see *Your connection is not private* notification due to using an untrusted security certificate. Then, proceed to access the OpenShift web console via clicking *Advanced* option.

* Username:
```
developer
```

* Password:
```
developer
```

![Web Console Login](https://raw.githubusercontent.com/openshift-instruqt/instruqt/master/assets/middleware/quarkus/login.png)

Run **Skip Tour** to skip the new user introduction, you will be presented with a list of projects that your user has permission to view.

![Web Console Projects](https://raw.githubusercontent.com/openshift-instruqt/instruqt/master/assets/middleware/rhoar-getting-started-spring/projects.png)

Click on your new project name to be taken to the project overview page which will show you various options to add content to your project, create an application, component or service:

![Web Console Overview](https://raw.githubusercontent.com/openshift-instruqt/instruqt/master/assets/middleware/rhoar-getting-started-spring/overview-new.png)

There's nothing there now, but that's about to change.

**2. Login to OpenShift Container Platform**

Run the following command to login with the OpenShift CLI:

```
oc login -u developer -p developer
```

You should see:

```bash
Login successful.
You don't have any projects. You can try to create a new project, by running `oc new-project <projectname>`
```

**3. Create project**

[Projects](https://docs.openshift.com/container-platform/4.7/rest_api/project_apis/project-project-openshift-io-v1.html) are a top-level concept to help you organize your deployments. An OpenShift project allows a community of users (or a user) to organize and manage their content in isolation from other communities. Each project has its own resources, policies (who can or cannot perform actions), and constraints (quotas and limits on resources, etc.). Projects act as a wrapper around all the application services and endpoints you (or your teams) are using for your work.

For this scenario, let's create a project that you will use to house your applications.

```
oc new-project dev --display-name="Dev - Spring Boot App"
```

## Congratulations

You have now learned how to access your openshift environment.

In next step of this scenario, we will deploy our application to the OpenShift Container Platform.
