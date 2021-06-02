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

## About the chart

The Spring pet clinic application is a well known example showing off the power of Spring. Over the years it's been refectored into microservices and then refactored for Kubernetes. That is what this chart deploys. To get deep with the application have a look at [our fork](https://github.com/platform9-community/spring-petclinc-cloud).

## Exposed services

To access any of the below services you'll either need to get the cluster's EXTERNAL-IP

```bash
kubectl get svc -n spring-petclinic api-gateway
```

Or if you using a cluser running on a local network, use a node's INTERNAL_IP

```bash
kubectl get node -o wide
```

### Pet clinic UI

The UI is served by the api gateway, which has a `NodePort` service attached. To access the application visit `http://<IP>:30808`.

[![Pet Clinic Home](<https://github.com/Platform9-Community/spring-petclinic-cloud/raw/master/docs/petclinic-home.png>]

### Management with spring admin

There is an instance of spring admin running where you can see each service's essentials and do things like turn logging levels up/down. Access admin server at `http://<IP>:30909`.

[![Pet Clinic Home](<https://github.com/Platform9-Community/spring-petclinic-cloud/raw/master/docs/spring-admin-wallboard.png>]

### Metrics with Grafana

The chart deploys Grafana with all it's default settings. It has an accompanying `NodePort` service, which can be accessed at `http://<IP>:30300`. Use the default creds of admin:admin. There is a single dashboard loaded that has Prometheus as a data source. Once logged in to Grafana go to `Dashboards > Manage > Spring Petclinic Metrics`.

[![Pet Clinic Home](<https://github.com/Platform9-Community/spring-petclinic-cloud/raw/master/docs/grafana-dash.png>]

### Logs with Kibana

All of the services are writing logs to stdout, which a FluentBit daemon is piping to Elasticstore. To query the logs visit the Kibana instance at `http://<IP>:30056`.

### Request tracing with Zipkin

All services are emitting reuqest traces to a Zipkin instance were you can visualize all the requests. This helm chart has no built in NodePort number. To access the collector UI get the auto-assigned forwarded port by running the below command.

```bash
kubectl -n spring-petclinic get svc zipkin-collector

#Output from the command
NAME               TYPE       CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
zipkin-collector   NodePort   10.X.X.X   <none>        9411:31928/TCP   165m
```

Then combine the cluster IP with the exposed port #. In the above case it would be `http://<IP>:31928`.
