# skipper

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.18.39](https://img.shields.io/badge/AppVersion-0.18.39-informational?style=flat-square)

A Helm chart for deploying [skipper](https://github.com/zalando/skipper) as cluster internal service proxy

Requires MAGDA version v2.0.0 or above.

### How to Use

1. Add the skipper as a [Helm Chart Dependency](https://helm.sh/docs/helm/helm_dependency/)
```yaml
- name: magda-skipper
  alias: my-service-proxy
  version: "1.0.0" # or put the latest version number here
  repository: "oci://ghcr.io/magda-io/charts"
```

> Please note: `alias` field is optional. Its purpose is to give the helm chart an alias name (rather than the default `magda-skipper`) so it's possible to use `magda-skipper` plugins multiple times in your deployment.

2. Config the auth plugin with OIDC client Id & issuer
```yaml
my-service-proxy:
 
```

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://ghcr.io/magda-io/charts | magda-common | 2.3.1 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| additionalServices | list | `[]` |  |
| affinity | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `3` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| config | string | `"# skipper config file\naddress: \":9090\"\naccess-log: \"/dev/stdout\"\napplication-log: \"/dev/stdout\"\n"` |  |
| defaultService.name | string | `""` | default, the default service name would be release name + '-' chart name (or chart alias name) this field allow you to overide the default service name |
| defaultService.ports[0].name | string | `"http"` |  |
| defaultService.ports[0].port | int | `9090` |  |
| defaultService.ports[0].targetPort | int | `9090` |  |
| defaultService.type | string | `"ClusterIP"` |  |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/zalando/skipper"` |  |
| image.tag | string | `""` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | list | `[]` |  |
| livenessProbe | object | `{}` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| readinessProbe | object | `{}` |  |
| replicaCount | int | `1` |  |
| resources.requests.cpu | string | `"150m"` |  |
| resources.requests.memory | string | `"150Mi"` |  |
| routes | string | `"# setup \n* -> \"https://www.example.org\""` |  |
| securityContext.readOnlyRootFilesystem | bool | `true` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `1000` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| tolerations | list | `[]` |  |