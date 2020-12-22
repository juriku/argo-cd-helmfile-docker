# argo-cd-helmfile-docker
argo-cd image with helmfile and sops (helm secrets)

## image repository
https://hub.docker.com/repository/docker/juriku/argo-cd-helmfile


argo-cd helm chart ref: https://github.com/argoproj/argo-helm/tree/master/charts/argo-cd

## change image
```
global:
  image:
    repository: eu.gcr.io/yapily-staging/yapily-tools/argo-cd-helmfile
    tag: v1.8.1
```
## add plugin
```
server:
  config:
    configManagementPlugins: |
      - name: helmfile
        init:
          command: ["sh", "-c"]
          args: ["helmfile repos"]
        generate:
          command: ["/bin/sh", "-c"]
          args: ["helmfile template --skip-deps"]
```

## define plugin inside application
```
server:
  additionalApplications:
      source:
        plugin:
          name: helmfile
```