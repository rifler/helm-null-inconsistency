# helm-null-inconsistency

Repository to demonstrate inconsistency in Helm template rendering (or maybe it is Go language flaw) when `null` is used.

## Problem

`null` value is rendered differently based on the context.

There are two charts:
- helm_render_null
- helm_render_void

### Case 1 - helm_render_null chart
Chart's `values.yaml` is empty.

User's values.yaml contains `resources.limits.cpu: null`.

When rendering the chart, the output contains `resources.limits.cpu: null`.

### Case 2 - helm_render_void chart
Chart's `values.yaml` has `resources.limits.cpu: 200m`.

User's values.yaml contains `resources.limits.cpu: null`.

When rendering the chart, the output does not contain `resources.limits.cpu` at all.

## How to reproduce

```bash
helm template ./helm_render_null/chart -f ./helm_render_null/values.yaml
# there is `resources.limits.cpu: null` in result output

helm template ./helm_render_void/chart -f ./helm_render_void/values.yaml
# no line `resources.limits.cpu` at all 
```

## Conclusion
Both chart's templates are the same.

Both user's values.yaml are the same.

The only difference is the initial value in chart's values.yaml.