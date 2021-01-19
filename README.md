# Todo MVC example

The ubiquitous [TodoMVC][todomvc] client-side web application, written in Rust, with a [GraphQL][graphql] API over a PostgreSQL database, and authentication with Google OAuth2 implicit flow.

The following diagram shows the setup in Kubernetes, with Istio and Dapr sidecars in each pod. An Istio `VirtualService` routes `/api` requests to the `api` service via the Istio and Dapr sidecars.

![TodoMVC in Istio and Dapr](./docs/dapr-todomvc.svg)

[graphql]: https://github.com/graphql/graphql
[todomvc]: http://todomvc.com/

---

## To get started

1. Install the `istioctl` cli, and the `dapr` cli, if you don't already have them.

   ```sh
   brew install istioctl
   brew install dapr-cli@1.0.0-rc.3
   ```

2. Install Istio and Dapr

   ```sh
   istioctl install
   dapr init --runtime-version 1.0.0-rc.2 --kubernetes
   ```

3. Install Zipkin into the cluster for tracing (will bring this into manifests later):

   ```sh
   kubectl create deployment zipkin -n default --image openzipkin/zipkin
   kubectl expose deployment zipkin -n default --type ClusterIP --port 9411
   ```

   To view the Zipkin dashboard:

   ```sh
   kubectl port-forward -n default svc/zipkin 9412:9411
   open http://localhost:9412
   ```

4. Apply system-wide manifests

   This will install a `gateway` resource in the `istio-system` namespace, to route HTTP traffic to our virtual services.

   ```sh
   (cd manifests && make)
   ```

5. Follow the Web UI [readme](./web/README.md)
6. Follow the API [readme](./api/README.md)
