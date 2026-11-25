# outbound-smtp

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2.0.0](https://img.shields.io/badge/AppVersion-2.0.0-informational?style=flat-square)

Outbound-only SMTP relay with DKIM signing

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| vukomir | <vukomir@ianculov.ro> | <https://github.com/vukomir> |

## Source Code

* <https://github.com/DevHatRo/helm-charts>
* <https://github.com/DevHatRo/outbound-smtp>

## Requirements

Kubernetes: `>=1.25.0-0`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| acme.agreeTOS | bool | `false` | `ACME_AGREE_TOS`: must be true with ACME; you accept the CA's terms of service |
| acme.challenge | string | `"http"` | `ACME_CHALLENGE`: `http` (needs port 80 of every name to reach the pod) or `dns` |
| acme.directoryURL | string | `""` | `ACME_DIRECTORY_URL` (empty = Let's Encrypt production; use staging while testing) |
| acme.dnsProvider | string | `""` | `ACME_DNS_PROVIDER` for DNS-01: cloudflare, hetzner or cpanel |
| acme.domains | list | `[]` | `ACME_DOMAINS`: certificate names (defaults to `config.hostname`) |
| acme.email | string | `""` | `ACME_EMAIL`: optional contact address |
| acme.enabled | bool | `false` | Obtain the certificate from Let's Encrypt instead of `tls` (stored under /data/acme) |
| acme.existingSecret | string | `""` | Existing Secret with the DNS provider credentials as env vars (`CLOUDFLARE_DNS_API_TOKEN`, `HETZNER_API_TOKEN`, or `CPANEL_USERNAME`/`CPANEL_TOKEN`/`CPANEL_BASE_URL`) |
| acme.httpPort | int | `80` | Service port for the HTTP-01 challenge (container listens on 8080) |
| affinity | object | `{}` | Affinity |
| config.enablePort25 | bool | `false` | `SMTP_ENABLE_PORT25`: enable plain SMTP for trusted networks |
| config.hostname | string | `""` | Required. `SMTP_HOSTNAME`: name used in EHLO; must match the PTR record of the sending IP |
| config.logLevel | string | `"info"` | `LOG_LEVEL`: debug, info, warn or error |
| config.logRecipients | bool | `false` | `LOG_RECIPIENTS`: also log full recipient addresses (personal data) |
| config.maxMessageSize | string | `"25MB"` | `MAX_MESSAGE_SIZE`: largest accepted message |
| config.port25StartTLS | bool | `true` | `SMTP_PORT25_STARTTLS`: offer STARTTLS on port 25 |
| config.queueMaxAge | string | `"72h"` | `QUEUE_MAX_AGE`: queue lifetime before a message bounces |
| env | object | `{}` | Any other environment variable the relay reads, keyed by name (e.g. `DELIVERY_CONCURRENCY: "20"`, `OTEL_EXPORTER_OTLP_ENDPOINT`). Values are quoted. |
| envFrom | list | `[]` | Extra `envFrom` sources (ConfigMaps or Secrets) |
| extraVolumeMounts | list | `[]` | Extra volume mounts |
| extraVolumes | list | `[]` | Extra volumes |
| fullnameOverride | string | `""` | Override the full resource name |
| image.digest | string | `""` | Image digest (`sha256:...`); wins over `tag` when set |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"ghcr.io/devhatro/outbound-smtp"` | Image repository |
| image.tag | string | `""` | Image tag (defaults to the chart appVersion) |
| imagePullSecrets | list | `[]` | Image pull secrets |
| metrics.serviceMonitor.enabled | bool | `false` | Create a Prometheus Operator ServiceMonitor for the metrics Service (port 9090, never exposed publicly) |
| metrics.serviceMonitor.interval | string | `"30s"` | Scrape interval |
| metrics.serviceMonitor.labels | object | `{}` | Extra ServiceMonitor labels (e.g. for the Prometheus selector) |
| nameOverride | string | `""` | Override the chart name |
| nodeSelector | object | `{}` | Node selector |
| persistence.accessMode | string | `"ReadWriteOnce"` | Access mode |
| persistence.annotations | object | `{}` | PVC annotations |
| persistence.enabled | bool | `true` | Persist /data (SQLite queue, domains, DKIM keys, users). Without it everything is lost on pod restart. |
| persistence.size | string | `"1Gi"` | Volume size |
| persistence.storageClass | string | `""` | Storage class (empty = cluster default) |
| podAnnotations | object | `{}` | Pod annotations |
| podLabels | object | `{}` | Extra pod labels |
| podSecurityContext | object | `{"fsGroup":10001,"fsGroupChangePolicy":"OnRootMismatch","runAsGroup":10001,"runAsNonRoot":true,"runAsUser":10001,"seccompProfile":{"type":"RuntimeDefault"}}` | Pod security context. The image runs as uid/gid 10001; fsGroup makes the data volume writable. |
| probes | object | `{"liveness":{"failureThreshold":3,"httpGet":{"path":"/healthz","port":"metrics"},"periodSeconds":30,"timeoutSeconds":5},"readiness":{"failureThreshold":3,"httpGet":{"path":"/healthz","port":"metrics"},"periodSeconds":10,"timeoutSeconds":5},"startup":{"failureThreshold":60,"httpGet":{"path":"/healthz","port":"metrics"},"periodSeconds":5}}` | Startup, liveness and readiness probes. All use `/healthz` on the metrics port. The startup probe allows 5 minutes for a first ACME certificate to be issued. |
| resources | object | `{"limits":{"memory":"256Mi"},"requests":{"cpu":"50m","memory":"64Mi"}}` | Container resources |
| securityContext | object | `{"allowPrivilegeEscalation":false,"capabilities":{"drop":["ALL"]},"readOnlyRootFilesystem":true}` | Container security context |
| service.annotations | object | `{}` | Service annotations (e.g. load balancer settings) |
| service.externalTrafficPolicy | string | `""` | `Local` keeps the client source IP; required if you trust networks (`network add`) for clients outside the cluster, otherwise the relay sees node addresses. |
| service.smtpPort | int | `25` | Plain SMTP port for trusted networks, exposed only when `config.enablePort25` is true (container listens on 8025) |
| service.smtpsPort | int | `465` | Implicit TLS port (container listens on 8465) |
| service.submissionPort | int | `587` | STARTTLS submission port (container listens on 8587) |
| service.type | string | `"ClusterIP"` | Service type for the SMTP ports. Use LoadBalancer to accept mail from outside the cluster. |
| serviceAccount.annotations | object | `{}` | ServiceAccount annotations |
| serviceAccount.create | bool | `true` | Create a ServiceAccount |
| serviceAccount.name | string | `""` | ServiceAccount name (generated from fullname if empty) |
| smarthost.existingSecret | string | `""` | Existing Secret holding the smarthost password |
| smarthost.host | string | `""` | `SMARTHOST_HOST`: send everything through this host instead of MX lookup |
| smarthost.passwordKey | string | `"password"` | Key in `existingSecret` holding the password |
| smarthost.port | int | `587` | `SMARTHOST_PORT`: 465 uses implicit TLS, others STARTTLS |
| smarthost.username | string | `""` | `SMARTHOST_USERNAME` (requires `existingSecret`) |
| terminationGracePeriodSeconds | int | `40` | Seconds to wait on shutdown; the relay gives open sessions and deliveries 30s |
| tls.existingSecret | string | `""` | Existing `kubernetes.io/tls` Secret (keys `tls.crt`, `tls.key`) for SMTP_HOSTNAME, e.g. from cert-manager. Renewals are picked up without a restart. |
| tls.selfSigned | bool | `false` | Generate a self-signed certificate. For testing only: clients will not trust it. |
| tolerations | list | `[]` | Tolerations |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
