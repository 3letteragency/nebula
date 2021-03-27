# nebula

<span style="display:block;text-align:center">[![GitHub](https://img.shields.io/static/v1.svg?color=db422a&logoColor=2a6bdb&style=for-the-badge&label=buildsociety&message=GitHub&logo=github)](https://github.com/3letteragency "view the source for all of our repositories.")</span>

![GitHub Workflow Status](https://img.shields.io/github/workflow/status/3letteragency/nebula/build?color=db422a&logoColor=FFFFFF&style=for-the-badge)
![Docker Pulls](https://img.shields.io/docker/pulls/3letteragency2/nebula?color=db422a&logoColor=2a6bdb&style=for-the-badge)
![Docker Image Size (latest by date)](https://img.shields.io/docker/image-size/3letteragency2/nebula?color=db422a&logoColor=2a6bdb&style=for-the-badge)
![Docker Stars](https://img.shields.io/docker/stars/3letteragency2/nebula?color=db422a&logoColor=2a6bdb&style=for-the-badge)

## Supported Architectures
Our images support multiple architectures such as x86-64, arm64 and armhf. We utilise the docker manifest for multi-platform awareness. More information is available from docker [here](https://github.com/docker/distribution/blob/master/docs/spec/manifest-v2-2.md#manifest-list).

Simply pulling [3letteragency/nebula](https://github.com//nebula) should retrieve the correct image for your arch.

## Version Tags

This image provides various versions that are available via tags. `latest` tag usually provides the latest stable version. Others are considered under development and caution must be exercised when using them.

| Tag | Description |
| :----: | --- |
| latest | Stable Nebula Releases |
| edge | Latest Nebula Releases |
| v1.3.0 | Nebula 1.3.0 Release |


## Usage

Here are some example snippets to help you get started creating a container.

### docker

```bash
    docker pull 3letteragency2/nebula:latest
    docker run -td --cap-add NET_ADMIN -v /path/to/config:/config --name nebula 3letteragency2/nebula:latest
```

User documentation for Nebula can be found at https://github.com/slackhq/nebula#readme

### Kubernetes Sidecar

```yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ...
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ...
  template:
    metadata:
      labels:
        app: ...
    spec:
      containers:
      - name: ...
      - name: nebula
        image: 3letteragency2/nebula:v1.2.0
        securityContext:
          capabilities:
            add:
              - NET_ADMIN
        volumeMounts:
        - mountPath: /config/config.yaml
          readOnly: true
          name: nebula-conf
        args: ["-config", "/config/config.yaml" ] 
      volumes:
      - name: nebula-conf
        configMap:
          name: nebula-conf
          items:
            - key: nebula.conf
              path: nebula.conf
```

## Parameters

Container images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| :----: | --- |
| `-v /config` | Nebula configuration directory. |

## Support Info

* Shell access whilst the container is running: `docker exec -it nebula /bin/sh`
* To monitor the logs of the container in realtime: `docker logs -f nebula`
* container version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' nebula`
* image version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' buildsociety/nebula`

## Updating Info

Most of our images are static, versioned, and require an image update and container recreation to update the app inside. We do not recommend or support updating apps inside the container.

An automated process for upgrading your container is available via [containrrr/watchtower](https://github.com/containrrr/watchtower).


## Licence

By using this image, you agree to the Nebula [licence](https://github.com/slackhq/nebula/blob/master/LICENSE)
