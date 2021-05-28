# Spring Pet Clinic for Kubernetes Helm Chart

* Installs the [Spring](https;//spring.io) pet clinic [demo app](https://github.com/spring-petclinic/spring-petclinic-cloud)

## Get Repo Info

```console
helm repo add Platform9-Community https://platform9-community.github.io/helm-charts
helm repo update
```

_See [helm repo](https://helm.sh/docs/helm/helm_repo/) for command documentation._

## Installing the Chart

To install the chart with the release name `spring-petclinic-cloud` to namespace `spring-petclinic`:

```console
helm install spring-petclinic-cloud Platform9-Community/spring-petclinic-cloud --namespace spring-petclinic --create-namespace
```

## Uninstalling the Chart

To uninstall/delete the `spring-petclinic-cloud` deployment from namespace `spring-petclinic`:

```console
helm uninstall spring-petclinic-cloud --namespace spring-petclinic
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

