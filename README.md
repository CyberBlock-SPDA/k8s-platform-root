# gitops-root

The production Flux Helm Controller is patched by
`clusters/prod-cluster/flux-system/kustomization.yaml` with
`--no-cross-namespace-refs=true`. Keep HelmRelease chart/source references in
the release namespace. This overlay patch is separate from the generated
`gotk-components.yaml` so it survives re-generation of Flux components.

The `backend-service` ServiceAccount and its namespaced
`gameserverallocations:create` Role are owned by the application Helm chart in
`k8s-apps-infrastructure`; do not recreate those objects from this repository.
The platform repo continues to own the tenant deployer and its platform
permissions, including namespace-scoped workload permissions and narrowly
scoped `bind`/`escalate` rights for the chart-managed backend and Alloy Roles.