# my-app-gitops

GitOps manifests for the [bgd](https://github.com/carlos-salinas/bgd) demo app. OpenShift GitOps (Argo CD) syncs `bgd/base` into the cluster.

## Layout

| Path | Purpose |
| ---- | ------- |
| `bgd/base/` | Kustomize base: Deployment, Service, Route |

The Deployment uses `quay.io/csalinas/bgd` and env vars `BG_COLOR`, `MESSAGE`, `APP_VERSION`, and `GIT_COMMIT` (see the bgd image entrypoint). CI can rewrite the `image:` field (for example via the build-and-gitops pipeline in osp-workbench).
