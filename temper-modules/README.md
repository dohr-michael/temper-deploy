# Temper Modules

This directory is the GitOps source for the Temper Modules web application. An
ArgoCD Application points at this path on the environment branch; it is the
only component that applies these resources to the cluster.

Before its first sync, the destination namespace needs:

- `Secret/temper-modules-secrets`, with `MONGODB_URI` set to the connection URI
  for a dedicated `temper_modules` user and database on the shared MongoDB service;
- `Secret/ghcr-login-secret` if `ghcr.io/dohr-michael/temper-modules` is private.

The product pipeline commits an immutable image digest to the `dev` branch
after a green push to `main`.

The pod disables Kubernetes service-link environment variables. The generated
`TEMPER_MODULES_PORT` value for `Service/temper-modules` would otherwise replace
the image's numeric HTTP port with a TCP URL and prevent the API from starting.
