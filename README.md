# Todo MVC example

The ubiquitous [TodoMVC][todomvc] client-side web application, written in Rust, with a [GraphQL][graphql] API over a PostgreSQL database, and authentication with Google OAuth2 implicit flow.

The following diagram shows the setup in Kubernetes, with Istio and Dapr sidecars in each pod. An Istio `VirtualService` routes `/api` requests to the `api` service via the Istio and Dapr sidecars.

![TodoMVC in Istio and Dapr](./docs/dapr-todomvc.svg)

[graphql]: https://github.com/graphql/graphql
[todomvc]: http://todomvc.com/

---

## To get started

- The Web UI [readme](./web/README.md)
- The API [readme](./api/README.md)
