# Install PSO 

Install PSO CSI driver inside k8's cluster

## Prerequistes

- helm client installed
- helm server installed
- tiller installed
- tiller account created
- git installed

### Install

You need to add the helm chart for Pure Storage

Add/update the helm repo for Pure
 
```
helm repo add pure https://purestorage.github.io/helm-charts
helm repo update
```


Create a values file to configure your PSO installation. 

You can download a sample by cloning the repo for [PSO](https://github.com/purestorage/helm-charts)

browse to the pure-csi directory and edit the values.yaml to add your arrays


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


##########################

worker node network config 

```
[root@knode04 ~]# ifconfig -s
Iface      MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
cali024e51bbd07  1480  4626365      0     60 0        366465      0      0      0 BMRU
cali0b1ba833b45  1480    52475      0     45 0            85      0      0      0 BMRU
cali29715c001b8  1480  4626365      0     60 0        366465      0      0      0 BMRU
cali36d72db93d8  1480  4626365      0     60 0        366465      0      0      0 BMRU
cali56cbf5b9371  1480  4626365      0     60 0        366465      0      0      0 BMRU
cali7987bda2083  1480    52475      0     45 0            85      0      0      0 BMRU
cali84b0ff3a62d  1480  4626365      0     60 0        366465      0      0      0 BMRU
cali9d8bde2b569  1480  4626365      0     60 0        366465      0      0      0 BMRU
calib5c9f472904  1480  4626365      0     60 0        366465      0      0      0 BMRU
calic0c0932cdcf  1480  9735981      0    355 0       7937587      0      0      0 BMRU
calic3a9fe3f3ca  1480    52475      0     45 0            85      0      0      0 BMRU
calic5079a5922d  1480    52475      0     45 0            85      0      0      0 BMRU
calic7dfa7b2543  1480  9735981      0    355 0       7937587      0      0      0 BMRU
calid8458403ced  1480        0      0      0 0             0      0      0      0 BMRU
calid8a8730495f  1480        0      0      0 0             0      0      0      0 BMRU
calif158eb81a71  1480  9735981      0    355 0       7937587      0      0      0 BMRU
ens192           1500  9735981      0    355 0       7937587      0      0      0 BMRU
ens224           1500  4626365      0     60 0        366465      0      0      0 BMRU
lo              65536   553112      0      0 0        553112      0      0      0 LRU
tunl0            1480  4535227      0      0 0       4390215      0      0      0 ORU

```
TYPE=Ethernet
BOOTPROTO=static
NAME=ens224
DEVICE=ens224
ONBOOT=yes
IPADDR=192.168.170.234
PREFIX=24
```



## Authors

* **Andy Parsons** - - [opslounge](https://github.com/opslounge)
