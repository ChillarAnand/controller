# Deis Workflow v2

[![Build Status](https://travis-ci.org/deis/workflow.svg?branch=master)](https://travis-ci.org/deis/workflow) [![codecov.io](https://codecov.io/github/deis/workflow/coverage.svg?branch=master)](https://codecov.io/github/deis/workflow?branch=master)

Deis (pronounced DAY-iss) is an open source PaaS that makes it easy to deploy and manage
applications on your own servers. Deis builds on [Kubernetes](http://kubernetes.io/) to provide
a lightweight, [Heroku-inspired](http://heroku.com) workflow.

## Work in Progress

![Deis Graphic](https://s3-us-west-2.amazonaws.com/get-deis/deis-graphic-small.png)

Deis Workflow v2 is currently in alpha. Your feedback and participation are more than welcome, but be
aware that this project is considered a work in progress.

The following features are not ready in Alpha1, but will be coming
soon.

- Complete SSL support
- Dockerfile builds
- Backup and restore features
- Persistent storage (though it can be manually configured)

## Hacking Workflow

First, [obtain a Kubernetes cluster][install-k8s]. Deis Workflow currently targets Kubernetes
v1.1 with the following requirements:

* Configure Docker's `insecure-registry` parameter to include the subnets used by your Kubernetes installation
* If you are testing the logger components, you must enable `DaemonSet` experimental APIs via `--runtime-config=extensions/v1beta1/daemonsets=true`

Next, install [helm](http://helm.sh). Next, add the deis repository to your chart list:

```console
$ helm repo add deis https://github.com/deis/charts
```

Then, install Deis!

To work off the latest stable

```console
$ helm install deis/deis
```

To work off the latest development version

```console
$ helm install deis/deis-dev
```

Complete instructions for installing and managing a Deis cluster are
available at https://github.com/deis/docs-v2

If you want to retrieve the latest client dev build for OS X or Linux, download the client:

```console
$ curl -sSL http://deis.io/deis-cli/install-v2-alpha.sh | bash
```

If you want to hack on a new feature, build the deis/workflow image and push it to a Docker
registry. The `$DEIS_REGISTRY` environment variable must point to a registry accessible to your
Kubernetes cluster. You may need to configure the Docker engines on your Kubernetes nodes to allow
`--insecure-registry 192.168.0.0/16` (or the appropriate address range).

When you want to test changes then commit the changes to your branch and run

```console
$ make deploy
```

This will build the required docker images and push them to the registry that was configured, then update and recreate the Replication Controller.
Give it a bit of time for the changes to go live.

## License

Copyright 2013, 2014, 2015, 2016 Engine Yard, Inc.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at <http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.


[install-k8s]: http://kubernetes.io/gettingstarted/
