# openshift-apache-php

Template for running a apache php with phalcon framework on a container based on alpine linux/openshift/docker.

### Installation

You need oc (https://github.com/openshift/origin/releases) locally installed:

create a new project (change to your whishes) or add this to your existing project

```sh
oc new-project openshift-apache-php-phalcon \
    --description="WebServer - Apache PHP Phalcon" \
    --display-name="Apache PHP Phalcon"
```

Deploy (externally)

```sh
oc new-app https://github.com/weepee-org/openshift-apache-php-phalcon.git --name apache-php-phalcon
```

Deploy (weepee internally)
add to Your buildconfig
```yaml
spec:
  strategy:
    dockerStrategy:
      from:
        kind: ImageStreamTag
        name: php-phalcon-webserver:latest
        namespace: weepee-registry
    type: Docker
```
use in your Dockerfile
```sh
FROM weepee-registry/php-phalcon-webserver

# Your app
ADD app /app
```

#### Route.yml

Create route for development and testing

```sh
curl https://raw.githubusercontent.com/ure/openshift-apache-php-phalcon/master/Route.yaml | oc create -f -
```
