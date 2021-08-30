## Deploying to Kubernetes as a Kontinue Workload

You need to have Kontinue and Cloud Native Runtimes installed on your cluster.

### Deploying to local cluster using Kubectl

To build and deploy the app run:

```
kubectl apply -f ./kubernetes/workload.yaml
```

To uninstall the app run:

```
kubectl delete -f ./kubernetes/workload.yaml
```


### Accessing the app deployed to local cluster

If you don't have `curl` installed it can be installed using downloads here: https://curl.se/download.html

You need to look up the Ingress endpoint for the Knative Serving install. See the [Install a networking layer](https://knative.dev/docs/install/install-serving-with-yaml/#install-a-networking-layer) and [Configure DNS](https://knative.dev/docs/install/install-serving-with-yaml/#configure-dns) sections for instructions for the different netwoking layers.

For _Kourier_ we can simply run the following port-forward command:

```
kubectl port-forward --namespace kourier-system service/kourier 8080:80
```

For _Contour_ we can simply run the following port-forward command:

```
kubectl port-forward --namespace contour-external service/envoy 8080:80
```

To invoke the deployed function run the following `curl` command in another terminal window:

```
curl localhost:8080 -w'\n' -H 'Content-Type: text/plain' -H 'Host: hello-fun.default.example.com' -d Fun
```
