# my-app-gitops

GitOps manifests for the [bgd](https://github.com/carlos-salinas/bgd) demo app. OpenShift GitOps (Argo CD) syncs the **lab overlay**.

## Layout

```text
bgd/
  base/                 # Stable Deployment, Service, Route
  overlays/lab/         # What CI mutates + what Argo syncs
    kustomization.yaml  # images: (tag/digest)
    env-patch.yaml      # BG_COLOR, GIT_COMMIT
```

| Path | Purpose |
| ---- | ------- |
| `bgd/base/` | Immutable-ish defaults (image tag `1.0.0`, default env) |
| `bgd/overlays/lab/` | Lab overlay: image digest + env overrides |

Argo CD `Application` path: **`bgd/overlays/lab`**.

CI (`build-and-gitops` in osp-workbench) updates only the overlay (`images` + `env-patch.yaml`), then commits. Argo rebuilds with Kustomize and reconciles the cluster.
