
## Prerequisites and Tools

Assumes kubectl is already installed on your workstation.

Lens is recommended for watching deployment, service and pod provisioning. https://k8slens.dev/

Review the knative install guide: https://knative.dev/docs/install/operator/knative-with-operators/#install-the-knative-operator

Requires `helm`.

YAML files referenced in this doc are under \src\knative-install-resources.

This doc is written against knative 1.3.1.

## Install Kubernetes Control Plane and Workers

Install a zone cluster (1 per billing account is free) for MVP.

This is currently installed as one large cluster, but instead install the cluster, create an autoscaling worker pool, then delete the default pool. 

TODO - refactor for the above and include reference to the terraform.

```
gcloud container --project "cuhealthai-foundations" clusters create "zonal-cluster-1" --zone "us-central1-c" --no-enable-basic-auth --cluster-version "1.21.6-gke.1500" --release-channel "regular" --machine-type "e2-medium" --image-type "COS_CONTAINERD" --disk-type "pd-standard" --disk-size "100" --metadata disable-legacy-endpoints=true --scopes "https://www.googleapis.com/auth/devstorage.read_only","https://www.googleapis.com/auth/logging.write","https://www.googleapis.com/auth/monitoring","https://www.googleapis.com/auth/servicecontrol","https://www.googleapis.com/auth/service.management.readonly","https://www.googleapis.com/auth/trace.append" --max-pods-per-node "110" --num-nodes "3" --logging=SYSTEM,WORKLOAD --monitoring=SYSTEM --enable-ip-alias --network "projects/cuhealthai-foundations/global/networks/default" --subnetwork "projects/cuhealthai-foundations/regions/us-central1/subnetworks/default" --no-enable-intra-node-visibility --default-max-pods-per-node "110" --no-enable-master-authorized-networks --addons HorizontalPodAutoscaling,HttpLoadBalancing,GcePersistentDiskCsiDriver --enable-autoupgrade --enable-autorepair --max-surge-upgrade 1 --max-unavailable-upgrade 0 --enable-shielded-nodes --node-locations "us-central1-c"
```

Configure .kube/config with credentials for the new cluster.

    gcloud container clusters get-credentials zonal-cluster-1 --zone us-central1-c --project cuhealthai-foundations

Copy the cluster config secret(s) to the password vault.

Once the cluster is up, fetching nodes should show something like this (example):

```
$>kubectl get nodes
NAME                                             STATUS   ROLES    AGE     VERSION
gke-zonal-cluster-1-default-pool-1915e7e8-2wz5   Ready    <none>   6m43s   v1.21.6-gke.1500
gke-zonal-cluster-1-default-pool-1915e7e8-dlht   Ready    <none>   6m43s   v1.21.6-gke.1500
gke-zonal-cluster-1-default-pool-1915e7e8-qcq1   Ready    <none>   6m43s   v1.21.6-gke.1500
```

## Install knative

Install the knative operator:

    kubectl apply -f https://github.com/knative/operator/releases/download/knative-v1.3.1/operator.yaml

Verify the installation; the deployment should be available (example):

```
$>kubectl get deployment knative-operator
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
knative-operator   1/1     1            1           69s
```

### knative-serving

Install the knative-serving file:

    kubectl apply -f knative-serving.yaml

Fetch the external IP address for DNS configuration:

    kubectl --namespace knative-serving get service kourier

It may take a minute, but eventually the EXTERNAL-IP address will be assigned (example shown).

```
NAME      TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)                      AGE
kourier   LoadBalancer   10.0.10.151   34.123.218.33   80:31370/TCP,443:31963/TCP   38s
```

Verify knative-serving is running:

    kubectl get KnativeServing knative-serving -n knative-serving

You should see READY = True.

```
NAME              VERSION   READY   REASON
knative-serving   1.3.0     True
```

Given the EXTERNAL-IP from a couple steps above, configure DNS `*.default` and `*.center` to a A records. `default` and `center` map here to k8s namespaces. For every new namespace used with knative, we need to add a separate wildcard A entry.

### knative-eventing

Install knative-eventing:

    kubectl apply -f knative-eventing.yaml

There are lots of eventing sources. TBD how we'll use these.

## Configure TLS

Following this guide, and assuming the use of the HTTP-01 challenge. https://knative.dev/docs/serving/using-auto-tls/#enabling-auto-tls

Add the cert-manager controller.

    kubectl apply --filename https://github.com/knative/net-certmanager/releases/download/knative-v1.3.0/release.yaml

Install cert-manager.

    helm repo add jetstack https://charts.jetstack.io
    helm repo update
    helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version v1.7.1 --set installCRDs=true

Install cluster issuer:

    kubectl apply -f letsencrypt-http01-issuer.yaml

Check to cluster issuer to see that READY = True:

    kubectl get clusterissuer letsencrypt-http01-issuer

Add a configmap for the certmananger:

    kubectl apply -f config-certmanager.yaml

Enable Auto-TLS. I'm patching below, but with Windows you may have to manually edit.

    kubectl patch configmap config-network --namespace knative-serving -p '{"data":{"auto-tls":"Enabled","autocreate-cluster-domain-claims":"true"}}'

Install a garbage collection policy

    kubectl apply -f gc.yaml
