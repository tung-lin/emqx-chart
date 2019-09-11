
# Introduction
This chart bootstraps an emqx deployment on a Kubernetes cluster using the Helm package manager. (fork from https://github.com/emqx/emqx-chart)

Add following configurations:
1. extraVolumes: Extra volumes to attach to the statefulset
2. extraVolumeMounts: Extra volume mounts to mount to the statefulset

# Prerequisites
+ Kubernetes 1.6+

# Installing the Chart
To install the chart with the release name `my-emqx`:

+   From github 
    ```
    $ git clone https://github.com/emqx/emqx-chart.git
    $ cd emqx-chart/charts/emqx
    $ helm install --name my-emqx .
    ```

+   From chart repos
    ```
    helm repo add emqx https://repos.emqx.io/charts
    helm install --name my-emqx emqx/emqx
    ```

# Uninstalling the Chart
To uninstall/delete the `my-emqx` deployment:
```
$ helm delete my-emqx
```

# Configuration
The following table lists the configurable parameters of the emqx chart and their default values.

| Parameter  | Description | Default Value |
| ---        |  ---        | ---           |
| `apiserver`  | Kubernates API server address |  https://kubernetes.default.svc:443    |
| `namespace`  | kubernetes namespace   |   default |
| `replicas` | It is recommended to have odd number of nodes in a cluster, otherwise the emqx cluster cannot be automatically healed in case of net-split. |3|
| `image` | EMQ X Image name |emqx/emqx:latest|
| `imagePullPolicy`  | Global Docker registry secret names as an array |IfNotPresent|
| `persistence.enabled` | Enable EMQX persistence using PVC |false|
| `persistence.storageClass` | Storage class of backing PVC |`nil` (uses alpha storage class annotation)|
| `persistence.existingClaim` | EMQ X data Persistent Volume existing claim name, evaluated as a template |""|
| `persistence.accessMode` | PVC Access Mode for EMQX volume |ReadWriteOnce|
| `persistence.size` | PVC Storage Request for EMQX volume |20Mi|
| `extraVolumes` | Extra volumes to attach to the statefulset | []
| `extraVolumeMounts` | Extra volume mounts to mount to the statefulset | []
| `resources` | CPU/Memory resource requests/limits |{}|
| `service.type`  | Emqx cluster service type. |ClusterIP|
| `service.mqttPort`  | Emqx cluster MQTT port. |1883|
| `service.mqttsslPort` | Emqx cluster MQTT(SSL) port.  |8883|
| `service.mgmtPort`  | Emqx cluster mgmt API.  |8080|
| `service.websocketPort`  | Emqx cluster WebSocket/http port. |8083|
| `service.wssPort`  | Emqx cluster WSS/HTTPS port.  |8084|
| `service.dashboardPort` | Emqx cluster dashboard port. |18083|
| `emqxAddressType` | The address type is used to extract host from k8s service. <br> Value: ip/dns/hostname  <br> Note: hostname is only supported after v3.2.1 | ip |
| `emqxConfig` | Emqx configuration item, see the [documentation](https://github.com/emqx/emqx-docker#emq-x-configuration) |{}|
| `emqxLicneseSecretName` | EMQX Enterprise Edition requires manual creation of a Secret containing the licensed content. Write the name of Secret to the value of "emqxLicneseSecretName" |""|
