# Build the Kubernetes cluster

## 1. Sign into Google Cloud

Navigate to the Google Cloud portal: https://console.cloud.google.com/ 

For this workshop we will use the web-based command line, Google Cloud Shell, to eliminate differences in laptop images. 

Open the Google Cloud Shell

![Cloud Shell](https://image.ibb.co/ccoxLF/cloudshell.png)

List all the projects on Google Cloud to make sure everything is working and you're in the right place. 
```
$ gcloud projects list
```
If you used Google Cloud before you may have more than one project. Make sure you change to the correct project:
```
$ gcloud config set project [PROJECT_ID]
```

## 2. Provision Cluster

Run the command to create a 3-node cluster on Google cloud.

```
$ gcloud container clusters create "k8sintelgoogle" \
  --zone "us-east1-c" \
  --machine-type "n1-standard-1" \
  --image-type "GCI" --disk-size "100" \
  --scopes cloud-platform \
  --num-nodes "3"
``` 

## 3. Connect with Cluster

Install kubectl

```
$ gcloud components install kubectl
```

Get credentials

```
$ gcloud auth application-default login
```

Configure kubectl with the training cluster context.

```
$ gcloud container clusters get-credentials k8sintelgoogle
```

Verify kubectl can connect to the cluster

```
$ kubectl cluster-info
```

Since we are using the public cloud command line (essentially a VM in Google Cloud) we need to modify the Kubernetes Dashboard UI service and expose it to the internet

```
$ kubectl get svc kubernetes-dashboard -n kube-system -o yaml | \
sed "s/ClusterIP/LoadBalancer/" | \
kubectl apply -f - -n kube-system
```
Get the IP of the Dashboard

```
$ kubectl get svc kubernetes-dashboard -n kube-system -w
```
Grab the IP adress from the highlighted below and paste it into your prefered browser

![IP Address](http://i.imgur.com/i1hlPV2.png)

## 4. Run "Hello World"

Deploy "hello world" application to get something up and running on your new cluster

```
kubectl run hello-world --replicas=5 --labels="run=load-balancer-example" --image=gcr.io/google-samples/node-hello:1.0  --port=8080
```


## 5. Tour of Dashboard (the official UI of Kubernetes)

Instructor will give a tour of the Kubernetes Dashboard

## 6. Open New Command Line

To continue to use the CLI, open a new command prompt with the proxy running in the other one. 
