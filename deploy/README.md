# Installing the Controller

You need a Kubernetes cluster with Internet connectivity.

## 1. Install [Metacontroller](https://metacontroller.github.io/metacontroller/guide/install.html):
  
  ```bash
  kubectl apply -k https://github.com/metacontroller/metacontroller/manifests/production
  ```

## 2. Install the Hyper Protect Virtual Servers Kubernetes Operator
The operator is can be installed via helm.

The static deployment manifests would be generated from the helm chart and bundled as part of a release on github.

### Generate my own Manifest files
You can generate your own static deployment manifests on your local workstation, using helm and make. 
Default deployment vlaues my be overwrtitten my customize the `helm-values.yaml` file.
    ```bash
    make manifests
    ``` 

## 3. Verify your installation by checking for the existence of the custom resources

```bash
kubectl get crds

NAME                                         CREATED AT
compositecontrollers.metacontroller.k8s.io   2023-03-15T21:32:11Z
controllerrevisions.metacontroller.k8s.io    2023-03-15T21:32:11Z
decoratorcontrollers.metacontroller.k8s.io   2023-03-15T21:32:11Z
onprem-hpcrs.hpse.ibm.com                    2023-03-17T12:44:30Z
vpc-hpcrs.hpse.ibm.com                       2023-03-17T12:44:30Z
```

```bash
kubectl get compositecontrollers

NAME                       AGE
k8s-operator-hpcr-onprem   5m37s
k8s-operator-hpcr-vpc      5m37s
```

```bash
kubectl get deployments

NAME                READY   UP-TO-DATE   AVAILABLE   AGE
k8s-operator-hpcr   1/1     1            1           6m35s
```

## Show Logs

```bash
kubectl logs -l app=k8s-operator-hpcr
```
