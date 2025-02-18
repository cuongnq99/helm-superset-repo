<!--
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.
-->

<!--
NOTE: This file is generated by helm-docs: https://github.com/norwoodj/helm-docs#installation
-->

# superset

![Version: 0.14.0](https://img.shields.io/badge/Version-0.14.0-informational?style=flat-square)

Apache Superset is a modern, enterprise-ready business intelligence web application

**Homepage:** <https://superset.apache.org/>

## Source Code

* <https://github.com/apache/superset>

## TL;DR

```console
kubectl create namespace superset
helm repo add superset http://cuongnq99.github.io/helm-superset-repo
helm repo update
helm upgrade --install --values values.yaml superset superset/superset -n superset --timeout 15m --wait
```

Make sure you set your own `SECRET_KEY` to something unique and secret. This secret key is used by Flask for
securely signing the session cookie and will be used to encrypt sensitive data on Superset's metadata database.
It should be a long random bytes or str.

On helm this can be set on `extraSecretEnv.SUPERSET_SECRET_KEY` or `configOverrides.secrets`

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://registry-1.docker.io/bitnamicharts | postgresql | 12.1.6 |
| oci://registry-1.docker.io/bitnamicharts | redis | 17.9.4 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| bootstrapScript | string | see `values.yaml` | Install additional packages and do any other bootstrap configuration in this script For production clusters it's recommended to build own image with this step done in CI |
| configFromSecret | string | `"{{ template \"superset.fullname\" . }}-config"` | The name of the secret which we will use to generate a superset_config.py file Note: this secret must have the key superset_config.py in it and can include other files as well |
| configMountPath | string | `"/app/pythonpath"` |  |
| configOverrides | object | `{}` | A dictionary of overrides to append at the end of superset_config.py - the name does not matter WARNING: the order is not guaranteed Files can be passed as helm --set-file configOverrides.my-override=my-file.py |
| configOverridesFiles | object | `{}` | Same as above but the values are files |
| envFromSecret | string | `"{{ template \"superset.fullname\" . }}-env"` | The name of the secret which we will use to populate env vars in deployed pods This can be useful for secret keys, etc. |
| envFromSecrets | list | `[]` | This can be a list of templated strings |
| extraConfigMountPath | string | `"/app/configs"` |  |
| extraConfigs | object | `{}` | Extra files to be mounted as ConfigMap on the path specified in `extraConfigMountPath` |
| extraEnv | object | `{}` | Extra environment variables that will be passed into pods |
| extraEnvRaw | list | `[]` | Extra environment variables in RAW format that will be passed into pods |
| extraLabels | object | `{}` | Labels to be added to all resources |
| extraSecretEnv | object | `{}` | Extra environment variables to pass as secrets |
| extraSecrets | object | `{}` | Extra files to be mounted as Secrets on the path specified in `configMountPath` |
| extraVolumeMounts | list | `[]` |  |
| extraVolumes | list | `[]` |  |
| fullnameOverride | string | `nil` | Provide a name to override the full names of resources |
| hostAliases | list | `[]` | Custom hostAliases for all superset pods # https://kubernetes.io/docs/tasks/network/customize-hosts-file-for-pods/ |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"apachesuperset.docker.scarf.sh/apache/superset"` |  |
| image.tag | string | `nil` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.extraHostsRaw | list | `[]` |  |
| ingress.hosts[0] | string | `"chart-example.local"` |  |
| ingress.ingressClassName | string | `nil` |  |
| ingress.path | string | `"/"` |  |
| ingress.pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| init.adminUser.email | string | `"admin@superset.com"` |  |
| init.adminUser.firstname | string | `"Superset"` |  |
| init.adminUser.lastname | string | `"Admin"` |  |
| init.adminUser.password | string | `"admin"` |  |
| init.adminUser.username | string | `"admin"` |  |
| init.affinity | object | `{}` |  |
| init.command | list | a `superset_init.sh` command | Command |
| init.containerSecurityContext | object | `{}` |  |
| init.createAdmin | bool | `true` |  |
| init.enabled | bool | `true` |  |
| init.extraContainers | list | `[]` | Launch additional containers into init job pod |
| init.initContainers | list | a container waiting for postgres | List of initContainers |
| init.initscript | string | a script to create admin user and initialize roles | A Superset init script |
| init.jobAnnotations."helm.sh/hook" | string | `"post-install,post-upgrade"` |  |
| init.jobAnnotations."helm.sh/hook-delete-policy" | string | `"before-hook-creation"` |  |
| init.loadExamples | bool | `false` |  |
| init.podAnnotations | object | `{}` |  |
| init.podLabels | object | `{}` |  |
| init.podSecurityContext | object | `{}` |  |
| init.priorityClassName | string | `nil` | Set priorityClassName for init job pods |
| init.resources | object | `{}` |  |
| init.tolerations | list | `[]` |  |
| init.topologySpreadConstraints | list | `[]` | TopologySpreadConstrains to be added to init job |
| initImage.pullPolicy | string | `"IfNotPresent"` |  |
| initImage.repository | string | `"apache/superset"` |  |
| initImage.tag | string | `"dockerize"` |  |
| nameOverride | string | `nil` | Provide a name to override the name of the chart |
| nodeSelector | object | `{}` |  |
| postgresql | object | see `values.yaml` | Configuration values for the postgresql dependency. ref: https://github.com/bitnami/charts/tree/main/bitnami/postgresql |
| priorityClassName | string | `nil` | Set priorityClassName for superset pods |
| redis | object | see `values.yaml` | Configuration values for the Redis dependency. ref: https://github.com/bitnami/charts/blob/master/bitnami/redis More documentation can be found here: https://artifacthub.io/packages/helm/bitnami/redis |
| resources | object | `{}` |  |
| runAsUser | int | `0` | User ID directive. This user must have enough permissions to run the bootstrap script Running containers as root is not recommended in production. Change this to another UID - e.g. 1000 to be more secure |
| secretEnv | object | `{"create":true}` | Specify rather or not helm should create the secret described in `secret-env.yaml` template |
| secretEnv.create | bool | `true` | Change to false in order to support externally created secret (Binami "Sealed Secrets" for Kubernetes or External Secrets Operator) note: when externally creating the secret, the chart still expects to pull values from a secret with the name of the release defaults to `release-name-superset-env` - full logic located in _helpers.tpl file: `define "superset.fullname"` |
| service.annotations | object | `{}` |  |
| service.loadBalancerIP | string | `nil` |  |
| service.nodePort.http | int | `"nil"` |  |
| service.port | int | `8088` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` | Create custom service account for Superset. If create: true and serviceAccountName is not provided, `superset.fullname` will be used. |
| serviceAccountName | string | `nil` | Specify service account name to be used |
| supersetCeleryBeat.affinity | object | `{}` | Affinity to be added to supersetCeleryBeat deployment |
| supersetCeleryBeat.command | list | a `celery beat` command | Command |
| supersetCeleryBeat.containerSecurityContext | object | `{}` |  |
| supersetCeleryBeat.deploymentAnnotations | object | `{}` | Annotations to be added to supersetCeleryBeat deployment |
| supersetCeleryBeat.enabled | bool | `false` | This is only required if you intend to use alerts and reports |
| supersetCeleryBeat.extraContainers | list | `[]` | Launch additional containers into supersetCeleryBeat pods |
| supersetCeleryBeat.forceReload | bool | `false` | If true, forces deployment to reload on each upgrade |
| supersetCeleryBeat.initContainers | list | a container waiting for postgres | List of init containers |
| supersetCeleryBeat.podAnnotations | object | `{}` | Annotations to be added to supersetCeleryBeat pods |
| supersetCeleryBeat.podDisruptionBudget | object | `{"enabled":false,"maxUnavailable":1,"minAvailable":1}` | Sets the [pod disruption budget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) for supersetCeleryBeat pods |
| supersetCeleryBeat.podDisruptionBudget.enabled | bool | `false` | Whether the pod disruption budget should be created |
| supersetCeleryBeat.podDisruptionBudget.maxUnavailable | int | `1` | If set, minAvailable must not be set - see https://kubernetes.io/docs/tasks/run-application/configure-pdb/#specifying-a-poddisruptionbudget |
| supersetCeleryBeat.podDisruptionBudget.minAvailable | int | `1` | If set, maxUnavailable must not be set - see https://kubernetes.io/docs/tasks/run-application/configure-pdb/#specifying-a-poddisruptionbudget |
| supersetCeleryBeat.podLabels | object | `{}` | Labels to be added to supersetCeleryBeat pods |
| supersetCeleryBeat.podSecurityContext | object | `{}` |  |
| supersetCeleryBeat.priorityClassName | string | `nil` | Set priorityClassName for CeleryBeat pods |
| supersetCeleryBeat.resources | object | `{}` | Resource settings for the CeleryBeat pods - these settings overwrite might existing values from the global resources object defined above. |
| supersetCeleryBeat.topologySpreadConstraints | list | `[]` | TopologySpreadConstrains to be added to supersetCeleryBeat deployments |
| supersetCeleryFlower.affinity | object | `{}` | Affinity to be added to supersetCeleryFlower deployment |
| supersetCeleryFlower.command | list | a `celery flower` command | Command |
| supersetCeleryFlower.containerSecurityContext | object | `{}` |  |
| supersetCeleryFlower.deploymentAnnotations | object | `{}` | Annotations to be added to supersetCeleryFlower deployment |
| supersetCeleryFlower.enabled | bool | `false` | Enables a Celery flower deployment (management UI to monitor celery jobs) WARNING: on superset 1.x, this requires a Superset image that has `flower<1.0.0` installed (which is NOT the case of the default images) flower>=1.0.0 requires Celery 5+ which Superset 1.5 does not support |
| supersetCeleryFlower.extraContainers | list | `[]` | Launch additional containers into supersetCeleryFlower pods |
| supersetCeleryFlower.initContainers | list | a container waiting for postgres and redis | List of init containers |
| supersetCeleryFlower.livenessProbe.failureThreshold | int | `3` |  |
| supersetCeleryFlower.livenessProbe.httpGet.path | string | `"/api/workers"` |  |
| supersetCeleryFlower.livenessProbe.httpGet.port | string | `"flower"` |  |
| supersetCeleryFlower.livenessProbe.initialDelaySeconds | int | `5` |  |
| supersetCeleryFlower.livenessProbe.periodSeconds | int | `5` |  |
| supersetCeleryFlower.livenessProbe.successThreshold | int | `1` |  |
| supersetCeleryFlower.livenessProbe.timeoutSeconds | int | `1` |  |
| supersetCeleryFlower.podAnnotations | object | `{}` | Annotations to be added to supersetCeleryFlower pods |
| supersetCeleryFlower.podDisruptionBudget | object | `{"enabled":false,"maxUnavailable":1,"minAvailable":1}` | Sets the [pod disruption budget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) for supersetCeleryFlower pods |
| supersetCeleryFlower.podDisruptionBudget.enabled | bool | `false` | Whether the pod disruption budget should be created |
| supersetCeleryFlower.podDisruptionBudget.maxUnavailable | int | `1` | If set, minAvailable must not be set - see https://kubernetes.io/docs/tasks/run-application/configure-pdb/#specifying-a-poddisruptionbudget |
| supersetCeleryFlower.podDisruptionBudget.minAvailable | int | `1` | If set, maxUnavailable must not be set - see https://kubernetes.io/docs/tasks/run-application/configure-pdb/#specifying-a-poddisruptionbudget |
| supersetCeleryFlower.podLabels | object | `{}` | Labels to be added to supersetCeleryFlower pods |
| supersetCeleryFlower.podSecurityContext | object | `{}` |  |
| supersetCeleryFlower.priorityClassName | string | `nil` | Set priorityClassName for supersetCeleryFlower pods |
| supersetCeleryFlower.readinessProbe.failureThreshold | int | `3` |  |
| supersetCeleryFlower.readinessProbe.httpGet.path | string | `"/api/workers"` |  |
| supersetCeleryFlower.readinessProbe.httpGet.port | string | `"flower"` |  |
| supersetCeleryFlower.readinessProbe.initialDelaySeconds | int | `5` |  |
| supersetCeleryFlower.readinessProbe.periodSeconds | int | `5` |  |
| supersetCeleryFlower.readinessProbe.successThreshold | int | `1` |  |
| supersetCeleryFlower.readinessProbe.timeoutSeconds | int | `1` |  |
| supersetCeleryFlower.replicaCount | int | `1` |  |
| supersetCeleryFlower.resources | object | `{}` | Resource settings for the CeleryBeat pods - these settings overwrite might existing values from the global resources object defined above. |
| supersetCeleryFlower.service.annotations | object | `{}` |  |
| supersetCeleryFlower.service.loadBalancerIP | string | `nil` |  |
| supersetCeleryFlower.service.nodePort.http | int | `"nil"` |  |
| supersetCeleryFlower.service.port | int | `5555` |  |
| supersetCeleryFlower.service.type | string | `"ClusterIP"` |  |
| supersetCeleryFlower.startupProbe.failureThreshold | int | `60` |  |
| supersetCeleryFlower.startupProbe.httpGet.path | string | `"/api/workers"` |  |
| supersetCeleryFlower.startupProbe.httpGet.port | string | `"flower"` |  |
| supersetCeleryFlower.startupProbe.initialDelaySeconds | int | `5` |  |
| supersetCeleryFlower.startupProbe.periodSeconds | int | `5` |  |
| supersetCeleryFlower.startupProbe.successThreshold | int | `1` |  |
| supersetCeleryFlower.startupProbe.timeoutSeconds | int | `1` |  |
| supersetCeleryFlower.topologySpreadConstraints | list | `[]` | TopologySpreadConstrains to be added to supersetCeleryFlower deployments |
| supersetNode.affinity | object | `{}` | Affinity to be added to supersetNode deployment |
| supersetNode.autoscaling.enabled | bool | `false` |  |
| supersetNode.autoscaling.maxReplicas | int | `100` |  |
| supersetNode.autoscaling.minReplicas | int | `1` |  |
| supersetNode.autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| supersetNode.command | list | See `values.yaml` | Startup command |
| supersetNode.connections.db_host | string | `"{{ .Release.Name }}-postgresql"` |  |
| supersetNode.connections.db_name | string | `"superset"` |  |
| supersetNode.connections.db_pass | string | `"superset"` |  |
| supersetNode.connections.db_port | string | `"5432"` |  |
| supersetNode.connections.db_user | string | `"superset"` |  |
| supersetNode.connections.redis_cache_db | string | `"1"` |  |
| supersetNode.connections.redis_celery_db | string | `"0"` |  |
| supersetNode.connections.redis_host | string | `"{{ .Release.Name }}-redis-headless"` | Change in case of bringing your own redis and then also set redis.enabled:false |
| supersetNode.connections.redis_port | string | `"6379"` |  |
| supersetNode.connections.redis_ssl.enabled | bool | `false` |  |
| supersetNode.connections.redis_ssl.ssl_cert_reqs | string | `"CERT_NONE"` |  |
| supersetNode.connections.redis_user | string | `""` |  |
| supersetNode.containerSecurityContext | object | `{}` |  |
| supersetNode.deploymentAnnotations | object | `{}` | Annotations to be added to supersetNode deployment |
| supersetNode.deploymentLabels | object | `{}` | Labels to be added to supersetNode deployment |
| supersetNode.env | object | `{}` |  |
| supersetNode.extraContainers | list | `[]` | Launch additional containers into supersetNode pod |
| supersetNode.forceReload | bool | `false` | If true, forces deployment to reload on each upgrade |
| supersetNode.initContainers | list | a container waiting for postgres | Init containers |
| supersetNode.livenessProbe.failureThreshold | int | `3` |  |
| supersetNode.livenessProbe.httpGet.path | string | `"/health"` |  |
| supersetNode.livenessProbe.httpGet.port | string | `"http"` |  |
| supersetNode.livenessProbe.initialDelaySeconds | int | `15` |  |
| supersetNode.livenessProbe.periodSeconds | int | `15` |  |
| supersetNode.livenessProbe.successThreshold | int | `1` |  |
| supersetNode.livenessProbe.timeoutSeconds | int | `1` |  |
| supersetNode.podAnnotations | object | `{}` | Annotations to be added to supersetNode pods |
| supersetNode.podDisruptionBudget | object | `{"enabled":false,"maxUnavailable":1,"minAvailable":1}` | Sets the [pod disruption budget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) for supersetNode pods |
| supersetNode.podDisruptionBudget.enabled | bool | `false` | Whether the pod disruption budget should be created |
| supersetNode.podDisruptionBudget.maxUnavailable | int | `1` | If set, minAvailable must not be set - see https://kubernetes.io/docs/tasks/run-application/configure-pdb/#specifying-a-poddisruptionbudget |
| supersetNode.podDisruptionBudget.minAvailable | int | `1` | If set, maxUnavailable must not be set - see https://kubernetes.io/docs/tasks/run-application/configure-pdb/#specifying-a-poddisruptionbudget |
| supersetNode.podLabels | object | `{}` | Labels to be added to supersetNode pods |
| supersetNode.podSecurityContext | object | `{}` |  |
| supersetNode.readinessProbe.failureThreshold | int | `3` |  |
| supersetNode.readinessProbe.httpGet.path | string | `"/health"` |  |
| supersetNode.readinessProbe.httpGet.port | string | `"http"` |  |
| supersetNode.readinessProbe.initialDelaySeconds | int | `15` |  |
| supersetNode.readinessProbe.periodSeconds | int | `15` |  |
| supersetNode.readinessProbe.successThreshold | int | `1` |  |
| supersetNode.readinessProbe.timeoutSeconds | int | `1` |  |
| supersetNode.replicas.enabled | bool | `true` |  |
| supersetNode.replicas.replicaCount | int | `1` |  |
| supersetNode.resources | object | `{}` | Resource settings for the supersetNode pods - these settings overwrite might existing values from the global resources object defined above. |
| supersetNode.startupProbe.failureThreshold | int | `60` |  |
| supersetNode.startupProbe.httpGet.path | string | `"/health"` |  |
| supersetNode.startupProbe.httpGet.port | string | `"http"` |  |
| supersetNode.startupProbe.initialDelaySeconds | int | `15` |  |
| supersetNode.startupProbe.periodSeconds | int | `5` |  |
| supersetNode.startupProbe.successThreshold | int | `1` |  |
| supersetNode.startupProbe.timeoutSeconds | int | `1` |  |
| supersetNode.strategy | object | `{}` |  |
| supersetNode.topologySpreadConstraints | list | `[]` | TopologySpreadConstrains to be added to supersetNode deployments |
| supersetWebsockets.affinity | object | `{}` | Affinity to be added to supersetWebsockets deployment |
| supersetWebsockets.command | list | `[]` |  |
| supersetWebsockets.config | object | see `values.yaml` | The config.json to pass to the server, see https://github.com/apache/superset/tree/master/superset-websocket Note that the configuration can also read from environment variables (which will have priority), see https://github.com/apache/superset/blob/master/superset-websocket/src/config.ts for a list of supported variables |
| supersetWebsockets.containerSecurityContext | object | `{}` |  |
| supersetWebsockets.deploymentAnnotations | object | `{}` |  |
| supersetWebsockets.enabled | bool | `false` | This is only required if you intend to use `GLOBAL_ASYNC_QUERIES` in `ws` mode see https://github.com/apache/superset/blob/master/CONTRIBUTING.md#async-chart-queries |
| supersetWebsockets.extraContainers | list | `[]` | Launch additional containers into supersetWebsockets pods |
| supersetWebsockets.image.pullPolicy | string | `"IfNotPresent"` |  |
| supersetWebsockets.image.repository | string | `"oneacrefund/superset-websocket"` | There is no official image (yet), this one is community-supported |
| supersetWebsockets.image.tag | string | `"latest"` |  |
| supersetWebsockets.ingress.path | string | `"/ws"` |  |
| supersetWebsockets.ingress.pathType | string | `"Prefix"` |  |
| supersetWebsockets.livenessProbe.failureThreshold | int | `3` |  |
| supersetWebsockets.livenessProbe.httpGet.path | string | `"/health"` |  |
| supersetWebsockets.livenessProbe.httpGet.port | string | `"ws"` |  |
| supersetWebsockets.livenessProbe.initialDelaySeconds | int | `5` |  |
| supersetWebsockets.livenessProbe.periodSeconds | int | `5` |  |
| supersetWebsockets.livenessProbe.successThreshold | int | `1` |  |
| supersetWebsockets.livenessProbe.timeoutSeconds | int | `1` |  |
| supersetWebsockets.podAnnotations | object | `{}` |  |
| supersetWebsockets.podDisruptionBudget | object | `{"enabled":false,"maxUnavailable":1,"minAvailable":1}` | Sets the [pod disruption budget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) for supersetWebsockets pods |
| supersetWebsockets.podDisruptionBudget.enabled | bool | `false` | Whether the pod disruption budget should be created |
| supersetWebsockets.podDisruptionBudget.maxUnavailable | int | `1` | If set, minAvailable must not be set - see https://kubernetes.io/docs/tasks/run-application/configure-pdb/#specifying-a-poddisruptionbudget |
| supersetWebsockets.podDisruptionBudget.minAvailable | int | `1` | If set, maxUnavailable must not be set - see https://kubernetes.io/docs/tasks/run-application/configure-pdb/#specifying-a-poddisruptionbudget |
| supersetWebsockets.podLabels | object | `{}` |  |
| supersetWebsockets.podSecurityContext | object | `{}` |  |
| supersetWebsockets.priorityClassName | string | `nil` | Set priorityClassName for supersetWebsockets pods |
| supersetWebsockets.readinessProbe.failureThreshold | int | `3` |  |
| supersetWebsockets.readinessProbe.httpGet.path | string | `"/health"` |  |
| supersetWebsockets.readinessProbe.httpGet.port | string | `"ws"` |  |
| supersetWebsockets.readinessProbe.initialDelaySeconds | int | `5` |  |
| supersetWebsockets.readinessProbe.periodSeconds | int | `5` |  |
| supersetWebsockets.readinessProbe.successThreshold | int | `1` |  |
| supersetWebsockets.readinessProbe.timeoutSeconds | int | `1` |  |
| supersetWebsockets.replicaCount | int | `1` |  |
| supersetWebsockets.resources | object | `{}` |  |
| supersetWebsockets.service.annotations | object | `{}` |  |
| supersetWebsockets.service.loadBalancerIP | string | `nil` |  |
| supersetWebsockets.service.nodePort.http | int | `"nil"` |  |
| supersetWebsockets.service.port | int | `8080` |  |
| supersetWebsockets.service.type | string | `"ClusterIP"` |  |
| supersetWebsockets.startupProbe.failureThreshold | int | `60` |  |
| supersetWebsockets.startupProbe.httpGet.path | string | `"/health"` |  |
| supersetWebsockets.startupProbe.httpGet.port | string | `"ws"` |  |
| supersetWebsockets.startupProbe.initialDelaySeconds | int | `5` |  |
| supersetWebsockets.startupProbe.periodSeconds | int | `5` |  |
| supersetWebsockets.startupProbe.successThreshold | int | `1` |  |
| supersetWebsockets.startupProbe.timeoutSeconds | int | `1` |  |
| supersetWebsockets.strategy | object | `{}` |  |
| supersetWebsockets.topologySpreadConstraints | list | `[]` | TopologySpreadConstrains to be added to supersetWebsockets deployments |
| supersetWorker.affinity | object | `{}` | Affinity to be added to supersetWorker deployment |
| supersetWorker.autoscaling.enabled | bool | `false` |  |
| supersetWorker.autoscaling.maxReplicas | int | `100` |  |
| supersetWorker.autoscaling.minReplicas | int | `1` |  |
| supersetWorker.autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| supersetWorker.command | list | a `celery worker` command | Worker startup command |
| supersetWorker.containerSecurityContext | object | `{}` |  |
| supersetWorker.deploymentAnnotations | object | `{}` | Annotations to be added to supersetWorker deployment |
| supersetWorker.deploymentLabels | object | `{}` | Labels to be added to supersetWorker deployment |
| supersetWorker.extraContainers | list | `[]` | Launch additional containers into supersetWorker pod |
| supersetWorker.forceReload | bool | `false` | If true, forces deployment to reload on each upgrade |
| supersetWorker.initContainers | list | a container waiting for postgres and redis | Init container |
| supersetWorker.livenessProbe.exec.command | list | a `celery inspect ping` command | Liveness probe command |
| supersetWorker.livenessProbe.failureThreshold | int | `3` |  |
| supersetWorker.livenessProbe.initialDelaySeconds | int | `120` |  |
| supersetWorker.livenessProbe.periodSeconds | int | `60` |  |
| supersetWorker.livenessProbe.successThreshold | int | `1` |  |
| supersetWorker.livenessProbe.timeoutSeconds | int | `60` |  |
| supersetWorker.podAnnotations | object | `{}` | Annotations to be added to supersetWorker pods |
| supersetWorker.podDisruptionBudget | object | `{"enabled":false,"maxUnavailable":1,"minAvailable":1}` | Sets the [pod disruption budget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) for supersetWorker pods |
| supersetWorker.podDisruptionBudget.enabled | bool | `false` | Whether the pod disruption budget should be created |
| supersetWorker.podDisruptionBudget.maxUnavailable | int | `1` | If set, minAvailable must not be set - see https://kubernetes.io/docs/tasks/run-application/configure-pdb/#specifying-a-poddisruptionbudget |
| supersetWorker.podDisruptionBudget.minAvailable | int | `1` | If set, maxUnavailable must not be set - see https://kubernetes.io/docs/tasks/run-application/configure-pdb/#specifying-a-poddisruptionbudget |
| supersetWorker.podLabels | object | `{}` | Labels to be added to supersetWorker pods |
| supersetWorker.podSecurityContext | object | `{}` |  |
| supersetWorker.priorityClassName | string | `nil` | Set priorityClassName for supersetWorker pods |
| supersetWorker.readinessProbe | object | `{}` | No startup/readiness probes by default since we don't really care about its startup time (it doesn't serve traffic) |
| supersetWorker.replicas.enabled | bool | `true` |  |
| supersetWorker.replicas.replicaCount | int | `1` |  |
| supersetWorker.resources | object | `{}` | Resource settings for the supersetWorker pods - these settings overwrite might existing values from the global resources object defined above. |
| supersetWorker.startupProbe | object | `{}` | No startup/readiness probes by default since we don't really care about its startup time (it doesn't serve traffic) |
| supersetWorker.strategy | object | `{}` |  |
| supersetWorker.topologySpreadConstraints | list | `[]` | TopologySpreadConstrains to be added to supersetWorker deployments |
| tolerations | list | `[]` |  |
| topologySpreadConstraints | list | `[]` | TopologySpreadConstrains to be added to all deployments |
