# skipper

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.18.39](https://img.shields.io/badge/AppVersion-0.18.39-informational?style=flat-square)

A Helm chart for deploying [skipper](https://github.com/zalando/skipper) as cluster internal service proxy

### Example Usage

1. Add the skipper as a [Helm Chart Dependency](https://helm.sh/docs/helm/helm_dependency/)
```yaml
- name: skipper
  alias: my-service-proxy
  version: "1.0.0" # or put the latest version number here
  repository: "oci://ghcr.io/magda-io/charts"
```

> Please note: `alias` field is optional. Its purpose is to give the helm chart an alias name (rather than the default `skipper`) so it's possible to use `skipper` chart multiple times in your deployment.

2. Config the proxy via "values" file
```yaml
my-service-proxy:
  service:
    # set the service name. This DNS name would be avialble within cluster
    # by default, it would be release name + - + alias name
    name: service-access-name
  routes: |
    myRoutes:
      * -> setRequestHeader("my header", "xxxxxx")
        -> setPath("/v1${request.path}")
        -> preserveHost("false")
        -> "https://xxxxx.xxxx.com";
```

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://ghcr.io/magda-io/charts | magda-common | 2.3.1 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `3` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| config | object | `{"access-log":"/dev/stdout","address":":9090","application-log":"/dev/stdout"}` | skipper config file see https://opensource.zalando.com/skipper/tutorials/basics/#yaml-configuration |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/zalando/skipper"` |  |
| image.tag | string | `""` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | list | `[]` |  |
| livenessProbe.httpGet.path | string | `"/__status/live"` |  |
| livenessProbe.httpGet.port | int | `9090` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| probeRoutes | string | `"// routes used to setup k8s probes\nprobe_liveness_up: \n  Method(\"GET\") && Path(\"/__status/live\") -> inlineContent(\"OK\") -> <shunt>;\nprobe_liveness_down: \n  Method(\"GET\") && Path(\"/__status/live\") && Shutdown() -> status(503) -> inlineContent(\"shutdown\") -> <shunt>;\nprobe_readiness_up: \n  Method(\"GET\") && Path(\"/__status/ready\") -> inlineContent(\"OK\") -> <shunt>;\nprobe_readiness_down: \n  Method(\"GET\") && Path(\"/__status/ready\") && Shutdown() -> status(503) -> inlineContent(\"shutdown\") -> <shunt>;\n"` |  |
| readinessProbe.httpGet.path | string | `"/__status/ready"` |  |
| readinessProbe.httpGet.port | int | `9090` |  |
| replicaCount | int | `1` |  |
| resources.requests.cpu | string | `"150m"` |  |
| resources.requests.memory | string | `"150Mi"` |  |
| routes | string | `"// everything else 404\ndefaultRoute: * -> <shunt>;\n"` |  |
| securityContext.readOnlyRootFilesystem | bool | `true` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `1000` |  |
| service.name | string | `""` | default, the service name would be release name + '-' chart name (or chart alias name) this field allow you to override the default service name |
| service.ports[0].name | string | `"http"` |  |
| service.ports[0].port | int | `80` |  |
| service.ports[0].targetPort | int | `9090` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| tolerations | list | `[]` |  |