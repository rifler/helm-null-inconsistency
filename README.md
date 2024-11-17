# helm-null-inconsistency

```bash
helm template ./helm_render_null/chart -f ./helm_render_null/values.yaml
# there is `resources.limits.cpu: null` in result output

helm template ./helm_render_void/chart -f ./helm_render_void/values.yaml
# no line `resources.limits.cpu` at all 
```