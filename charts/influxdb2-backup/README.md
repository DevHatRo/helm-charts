# influxdb2-backup

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2.7.4](https://img.shields.io/badge/AppVersion-2.7.4-informational?style=flat-square)

A Helm chart for InfluxDB v2 Backup

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| vukomir | <vukomir@ianculov.ro> |  |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| backup.annotations | object | `{}` |  |
| backup.enabled | bool | `false` |  |
| backup.nodeSelector | object | `{}` |  |
| backup.persistence.accessMode | string | `"ReadWriteOnce"` |  |
| backup.persistence.annotations | string | `nil` |  |
| backup.persistence.enabled | bool | `false` |  |
| backup.persistence.size | string | `"8Gi"` |  |
| backup.podAnnotations | object | `{}` |  |
| backup.resources.requests.ephemeral-storage | string | `"8Gi"` |  |
| backup.schedule | string | `"0 0 * * *"` |  |
| backup.startingDeadlineSeconds | string | `""` |  |
| config.bucket | string | `"telegraf"` |  |
| config.host | string | `"http://localhost:8086"` |  |
| config.org | string | `"main"` |  |
| config.token | string | `nil` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"influxdb"` |  |
| image.tag | string | `"2.7.4-alpine"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `nil` |  |

