# NKP-Katalog: Veeam Kasten for Kubernetes

Custom Catalog für NKP Kommander mit dem Kasten-Helm-Chart `k10`.

## Icon

Das Logo stammt aus dem SUSE Rancher Partner-Catalog (`rancher/partner-charts`,
`assets/icons/k10.png`) und ist bereits Base64-kodiert in
`services/kasten/metadata.yaml` eingetragen.

## Einbinden

1. Repo nach GitHub/GitLab pushen (muss vom Management-Cluster erreichbar sein).
2. Als Katalog im Workspace registrieren:

   ```bash
   nkp create catalog kasten-catalog \
     -w <workspace-name> \
     --branch main \
     --url https://github.com/<org>/<repo>
   ```

3. Prüfen:

   ```bash
   kubectl get gitrepository -n <workspace-namespace>
   kubectl get apps -n <workspace-namespace> | grep kasten
   ```

4. In der UI: Workspace > Applications > "Veeam Kasten for Kubernetes" > Enable.

## Neue Kasten-Version

Verzeichnis `services/kasten/9.0.11` kopieren, nach der neuen Chart-Version
benennen und `version:` in `kasten.yaml` anpassen. Verfügbare Versionen:

```bash
helm repo add kasten https://charts.kasten.io/
helm search repo kasten/k10 --versions | head
```
