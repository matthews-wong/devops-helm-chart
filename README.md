# static-site-chart

A tiny, dependency-free Helm chart for serving a static website from a
container and exposing it through a Kubernetes `Service` (and optionally an
`Ingress`).

It started as a way to stop hand-writing the same three manifests every time I
wanted to put a small site online. The chart is intentionally boring: one
`Deployment`, one `Service`, and an optional `Ingress`. No subcharts, no
CRDs, nothing to `helm dependency build`.

## What you get

- A `Deployment` running any image you point it at (defaults to `nginxdemos/hello`).
- A `ClusterIP` `Service` in front of it.
- An optional `Ingress` when you set `ingress.enabled: true`.
- A `PodDisruptionBudget` when you set a non-zero `minAvailable`.

## Install

```sh
helm install mysite ./static-site-chart \
  --set ingress.enabled=true \
  --set ingress.host=example.com
```

Or with a `values.yaml`:

```sh
helm install mysite ./static-site-chart -f my-values.yaml
```

## Upgrade / uninstall

```sh
helm upgrade mysite ./static-site-chart
helm uninstall mysite
```

## Values

See [`values.yaml`](./values.yaml) for every tunable knob and its default.
