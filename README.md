# lab-env

Setting up with basic configurations in a Kubernetes-based lab environment on my Macbook M1(aarch64) with:
- Rancher Desktop or Colima
- kubectl
- kubectx
- Helm
- OpenTelemetry
- Vscode
- Docker & Docker Compose

## Free Services

- Observability
  - New Relic, https://newrelic.com/signup
- Computing / Storage / Database
  - Oracle Cloud (kr), https://www.oracle.com/kr/cloud/free/

## Local Dev. with Kubernetes

- Rancher Desktop
- Colima
- k3s
- Kind
- https://github.com/GoogleContainerTools/skaffold
- https://github.com/loft-sh/devspace

### Local development with Rancher Desktop

Prerequisites:
- Rancher Desktop (k3s)
- Docker Compose
- Quarkus Extentions
  - Jib
  - Kubernetes

A Quarkus example:
```
$ ./mvnw clean install -Dquarkus.container-image.build=true -Dquarkus.kubernetes.image-pull-policy=Never

(snip)
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Created container image 1110551/code-with-quarkus:1.0.0-SNAPSHOT (sha256:ec4d12f922615bdd21a424b5f59872465fc862b04ce47d3215f6dfd8b8e14e64)

# Kubernetes
$ kubectl apply -f target/kubernetes/kubernetes.yml 
$ kubectl get all -n default

# docker-compose
TBD

```

## Labs

### Multi-node Kubernetes cluster in local env with k3s & k3d

TBD

### Dapr

```
# https://docs.dapr.io/operations/hosting/self-hosted/self-hosted-overview/
# Apple M1 (aarch64)

$ arch -arm64 brew install dapr/tap/dapr-cli
$ dapr
.......

# self-hosted
$ dapr init

# Dapr app. (local)
$ dapr run --help
.....

$ dapr run --app-id demo --app-port 8080 --app-protocol http --dapr-http-port 3500 --dapr-grpc-port 50001 ./mvnw clean spring-boot:run
$ dapr run --app-id demo --app-port 8080 --app-protocol http --dapr-http-port 3500 --dapr-grpc-port 50001 ./mvnw compile quarkus:dev

# Test
# Invoking the service for the sidecar (http)
$ curl -X GET http://localhost:3500/v1.0/invoke/demo/method/world/100

----

# For Docker / Docker Compose
TBD

# For k8s
$ kubectx
rancher-desktop

$ dapr init -k -n dapr-system
$ kubectl get all -n dapr-system

```

## Refs.

- https://github.com/askblaker/k3s.rocks