# NKP-Katalog: Veeam Kasten for Kubernetes

Catalog-Collection für NKP 2.18+ (getestet gegen das Format von NKP 2.19)
mit dem Kasten-Helm-Chart `k10` 9.0.11. Kasten wird im Namespace
`kasten-io` installiert.

## Aufbau

```
applications/kasten/9.0.11/
├── metadata.yaml          # Kachel: Name, Beschreibung, Icon
├── kustomization.yaml
├── helmrelease.yaml       # Flux-Kustomization auf ./helmrelease
└── helmrelease/
    ├── kustomization.yaml
    ├── cm.yaml            # Default-Values
    └── kasten.yaml        # HelmRepository + HelmRelease
.release/release.yaml      # Release-Spec für Tag 2.19
```

## Veröffentlichen (macOS/Linux, nkp CLI 2.19)

```bash
nkp validate catalog-repository --repo-dir .
echo "$GHCR_TOKEN" | docker login ghcr.io -u ftrie-veeam --password-stdin
nkp experimental catalog release \
  --release-spec .release/release.yaml \
  --repo-dir . \
  --push-to-registry ghcr.io/ftrie-veeam
```

Danach die neuen Packages auf GitHub auf **Public** stellen
(Profil > Packages > Package settings > Change visibility).

## Einbinden

```bash
nkp create catalog-collection \
  --url oci://ghcr.io/ftrie-veeam/k10-for-nkp-catalog/collection \
  --tag 2.19 \
  --workspace dev-ws
```

## Neue Kasten-Version

`applications/kasten/9.0.11` kopieren, nach der neuen Version benennen,
`version:` in `helmrelease/kasten.yaml` anpassen und neu veröffentlichen.
