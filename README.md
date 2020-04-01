# Jupyter-install

Install PSO CSI driver inside k8's cluster

## Prerequistes

- helm client installed
- helm server installed
- tiller installed
- tiller account created
- git installed

### Install

You need to clone the repo from Pure Storage

Add/update the helm repo for Pure
 
```
helm repo add pure https://purestorage.github.io/helm-charts
helm repo update
```

Clone the repo for PSO 

```
helm install --name pure-storage-driver pure/pure-csi --namespace pureflash -f path-to/values.yaml
```



browse to the pure-csi directory and edit the values.yaml to add your arrays

more on PSO install options can be found here [PSO](https://github.com/purestorage/helm-charts)

```
# provisioner. An example is shown below:
arrays:

  FlashArrays:
    - MgmtEndPoint: "10.226.224.110"
      APIToken: "your token here"
  FlashBlades:
    - MgmtEndPoint: "10.226.224.182"
      APIToken: "your token here"
      NfsEndPoint: "10.226.224.247"
```

You can install PSO using the command below

```
helm install --name pure-storage-driver pure/pure-csi --namespace pureflash -f path-to/values.yaml
```

```
aparsons@k8kube01:~/helm-charts/pure-csi$ helm install --name pure-storage-driver pure/pure-csi --namespace pureflash -f values.yaml
NAME:   pure-storage-driver
LAST DEPLOYED: Tue Mar 31 19:55:05 2020
NAMESPACE: pureflash
STATUS: DEPLOYED

RESOURCES:
==> v1/ClusterRole
NAME                         AGE
external-provisioner-runner  0s

==> v1/ClusterRoleBinding
NAME                  AGE
csi-provisioner-role  0s
csi-snapshotter-role  0s

==> v1/DaemonSet
NAME      DESIRED  CURRENT  READY  UP-TO-DATE  AVAILABLE  NODE SELECTOR  AGE
pure-csi  2        2        0      2           0          <none>         0s

==> v1/Pod(related)
NAME                READY  STATUS             RESTARTS  AGE
pure-csi-lgllv      0/3    ContainerCreating  0         0s
pure-csi-t5ml5      0/3    ContainerCreating  0         0s
pure-provisioner-0  0/3    ContainerCreating  0         0s

==> v1/Secret
NAME                     TYPE    DATA  AGE
pure-provisioner-secret  Opaque  1     0s

==> v1/Service
NAME                          TYPE       CLUSTER-IP      EXTERNAL-IP  PORT(S)    AGE
pure-provisioner              ClusterIP  10.111.206.102  <none>       12345/TCP  0s
pure-storage-driver-pure-csi  ClusterIP  10.98.130.30    <none>       12345/TCP  0s

==> v1/ServiceAccount
NAME  SECRETS  AGE
pure  1        0s

==> v1/StatefulSet
NAME              READY  AGE
pure-provisioner  0/1    0s

==> v1/StorageClass
NAME        PROVISIONER  AGE
pure        pure-csi     0s
pure-block  pure-csi     0s
pure-file   pure-csi     0s

==> v1beta1/CSIDriver
NAME      AGE
pure-csi  0s
```

Installed successfully



## Authors

* **Andy Parsons** - - [opslounge](https://github.com/opslounge)
