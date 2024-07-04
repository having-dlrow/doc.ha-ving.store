# 💽 Storage

Microk8s

* 사용X 이미지 삭제

```
# 사용되지 않는 이미지 삭제
sudo microk8s.ctr images remove $(sudo microk8s.ctr images list -q)
```

* [https://kubernetes.io/docs/concepts/architecture/garbage-collection/](https://kubernetes.io/docs/concepts/architecture/garbage-collection/)
*

MicroK8s Storage

* [OpenEBS](https://openebs.io/) (openebs-hostpath)

```
sudo apt get update
sudo apt-get install open-iscsi
sudo systemctl enable iscsid
microk8s enable openebs
```

```
Infer repository community for addon openebs
Infer repository core for addon dns
Addon core/dns is already enabled
Infer repository core for addon helm3
Addon core/helm3 is already enabled
"openebs" has been added to your repositories
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "kubernetes-dashboard" chart repository
...Successfully got an update from the "openebs" chart repository
...Successfully got an update from the "harbor" chart repository
...Successfully got an update from the "jenkins" chart repository
...Successfully got an update from the "argo" chart repository
...Successfully got an update from the "prometheus-community" chart repository
...Successfully got an update from the "bitnami" chart repository
Update Complete. ⎈Happy Helming!⎈
NAME: openebs
LAST DEPLOYED: Fri Jun 21 16:26:02 2024
NAMESPACE: openebs
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Successfully installed OpenEBS.

Check the status by running: kubectl get pods -n openebs

The default values will install NDM and enable OpenEBS hostpath and device
storage engines along with their default StorageClasses. Use `kubectl get sc`
to see the list of installed OpenEBS StorageClasses.

**Note**: If you are upgrading from the older helm chart that was using cStor
and Jiva (non-csi) volumes, you will have to run the following command to include
the older provisioners:

helm upgrade openebs openebs/openebs \
        --namespace openebs \
        --set legacy.enabled=true \
        --reuse-values

For other engines, you will need to perform a few more additional steps to
enable the engine, configure the engines (e.g. creating pools) and create 
StorageClasses. 

For example, cStor can be enabled using commands like:

helm upgrade openebs openebs/openebs \
        --namespace openebs \
        --set cstor.enabled=true \
        --reuse-values

For more information, 
- view the online documentation at https://openebs.io/docs or
- connect with an active community on Kubernetes slack #openebs channel.
OpenEBS is installed


-----------------------

When using OpenEBS with a single node MicroK8s, it is recommended to use the openebs-hostpath StorageClass
An example of creating a PersistentVolumeClaim utilizing the openebs-hostpath StorageClass
```
