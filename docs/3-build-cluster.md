# Build the Kubernetes cluster

## 1. Sign into Google Cloud

Open a command shell. 

Sign into your Google Cloud account (need Google SDK [here](https://cloud.google.com/sdk/))

The following command will open up a browser window to authenticate using your Gsuite account associated with the Google Cloud.

```
$ gcloud auth login
```

## 2. Provision Cluster

Find the project ID

![Image of Google Cloud Dashboard](http://i.imgur.com/WRXSKt4.png)

Copy the following command and replace [PROJECT ID] with your specific project ID. 

```
$ gcloud container --project [PROJECT ID] clusters create "k8strainingcluster" --zone "us-west1-a" --machine-type "n1-standard-1" --image-type "GCI" --disk-size "100" --scopes "https://www.googleapis.com/auth/compute","https://www.googleapis.com/auth/devstorage.read_only","https://www.googleapis.com/auth/logging.write","https://www.googleapis.com/auth/servicecontrol","https://www.googleapis.com/auth/service.management.readonly","https://www.googleapis.com/auth/trace.append" --num-nodes "3" --network "default" --enable-cloud-logging --enable-cloud-monitoring --enable-autoupgrade
```
Run the command to create a 3-node cluster on Google cloud. 

## 3. Connect with Cluster

Install kubectl

```
gcloud components install kubectl
```

Get credentials

```
gcloud auth application-default login
```

Configure kubectl with the training cluster context. Copy the command line AND REPLACE PROJECT ID with your project ID. 

```
gcloud container clusters get-credentials k8strainingcluster --zone us-west1-a --project [PROJECT ID]
```

Verify kubectl can connect to the cluster

```
kubectl cluster-info
```

Start proxy to connect to the Kubernetes cluster. This command authenticates you with the Kubernetes API server. 

```
kubectl proxy
```
Note you can only run the Kubernetes Dashboard (official UI) on the machine in which you run this command. It won't work on remote machine.  

Open the Dashboard in browser with the following IP URL

```
127.0.0.1:8001/ui
```

Would accessing the Dashboard be the same on other instances of Kubernetes - e.g. not public cloud? Yes, but you can also access the Dashboard in other ways, including 

```
https://<IP of master node>/ui"
```

## 4. Run "Hello World"

Deploy "hello world" application to get something up and running on your new cluster

```
kubectl run hello-world --replicas=5 --labels="run=load-balancer-example" --image=gcr.io/google-samples/node-hello:1.0  --port=8080
```


## 5. Tour of Dashboard (the official UI of Kubernetes)

Instructor will give a tour of the Kubernetes Dashboard

## 6. Open New Command Line

To continue to use the CLI, open a new command prompt with the proxy running in the other one. 
