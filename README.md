# Conference Oolong content (TEA 1.0.0)

Public demo catalog previously used with Oolong / TEA beta. The tree now
matches the TEA 1.0.0 layout that this Oolong branch serves.

Layout:

- `products/<name>/product.yaml` and `releases/<version>/release.yaml`
- `components/<name>/component.yaml` and matching releases
- `artifacts/<uuid>/v<n>.yaml` (no longer a single file per UUID)
- collection `artifacts` are `{ uuid, version }` objects
- collection dates use `createdDate`
- product and component releases name their parent UUID
- TEI values use `tei://host/type/value`
- artifact formats use `mediaType`
- component distributions use a UUID `distributionId`

Point an Oolong Git pod at this repository after the TEA 1.0.0 conversion is
pushed:

```bash
helm upgrade --install --create-namespace -n oolong oolong helm-chart/oolong \
  --set image=oolong-server:local \
  --set gitPod.enabled=true \
  --set gitPod.repoUrl='https://github.com/Reliza-Demos/conferences-oolong-content-2025-11.git' \
  --set gitPod.branch=main
```

A commit that changes a product name is published as a new revision. The server
polls `.oolong-current-revision` and serves the new snapshot after it validates.
