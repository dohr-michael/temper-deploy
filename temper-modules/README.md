# Temper Modules

This directory is the GitOps source for the Temper Modules web application. An
ArgoCD Application points at this path on the environment branch; it is the
only component that applies these resources to the cluster.

Before its first sync, the destination namespace needs:

- `Secret/temper-modules-secrets`, with `MONGODB_URI` set to the connection URI
  of the MongoDB database dedicated to Temper Modules;
- `Secret/ghcr-login-secret` if `ghcr.io/dohr-michael/temper-modules` is private.

The product pipeline replaces `REPLACED_BY_CI` with an immutable image digest on
the `dev` branch after a green push to `main`.
