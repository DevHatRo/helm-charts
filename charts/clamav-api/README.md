# clamav-api

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.0.2](https://img.shields.io/badge/AppVersion-1.0.2-informational?style=flat-square)

A REST API for ClamAV antivirus scanning

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Vucomir Ianculov | <vucomir@ianculov.ro> |  |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Pod affinity settings |
| autoscaling.enabled | bool | `false` | Enable autoscaling |
| autoscaling.maxReplicas | int | `100` | Maximum number of replicas |
| autoscaling.minReplicas | int | `1` | Minimum number of replicas |
| autoscaling.targetCPUUtilizationPercentage | int | `80` | Target CPU utilization |
| autoscaling.targetMemoryUtilizationPercentage | int | `80` | Target memory utilization |
| config.debug | bool | `false` | Enable debug mode |
| config.ginMode | string | `"release"` | Gin framework mode |
| config.host | string | `"0.0.0.0"` | API host binding |
| config.maxSize | string | `"209715200"` | Maximum file size for scanning |
| config.port | string | `"6000"` | API port |
| config.socket | string | `"/var/run/clamav/clamd.ctl"` | ClamAV socket path |
| fullnameOverride | string | `""` | Override the full name |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"ghcr.io/devhatro/clamav-api"` | Image repository |
| image.tag | string | `""` | Image tag (defaults to Chart appVersion) |
| imagePullSecrets | list | `[]` | Image pull secrets |
| ingress.annotations | object | `{}` | Ingress annotations |
| ingress.className | string | `""` | Ingress class name |
| ingress.enabled | bool | `false` | Enable ingress |
| ingress.hosts | list | See values.yaml | Ingress hosts configuration |
| ingress.tls | list | `[]` | Ingress TLS configuration |
| nameOverride | string | `""` | Override the name |
| nodeSelector | object | `{}` | Node selector settings |
| persistence.accessMode | string | `"ReadWriteOnce"` | PVC access mode |
| persistence.annotations | object | `{}` | PVC annotations |
| persistence.enabled | bool | `false` | Enable persistence |
| persistence.size | string | `"1Gi"` | PVC size |
| persistence.storageClass | string | `""` | Storage class name |
| podAnnotations | object | `{}` | Pod annotations |
| podSecurityContext | object | See values.yaml | Pod security context |
| replicaCount | int | `1` | Number of replicas |
| resources | object | See values.yaml | Container resource requests and limits |
| securityContext | object | See values.yaml | Container security context |
| service.port | int | `6000` | Service port |
| service.type | string | `"ClusterIP"` | Service type |
| tolerations | list | `[]` | Pod tolerations | 
