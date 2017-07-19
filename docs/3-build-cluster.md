# Build the Kubernetes Cluster
In the following section, there are commands highlighted in grey. You will copy and paste the commands into the Google CLoud Shell command prompt - $. The actual $ symbol is disregarded to make it easy to cut and paste. 
```
$
```
**Tips for those who have not used a command line in ages**

It may take some time for a command prompt to come up with a result. If it ever gets stuck you can use "ctrl+c" to get back to the command line. 

You can use the up arrow to find previous entered commands. 

## 1. Sign into Google Cloud

Navigate to the Google Cloud portal: https://console.cloud.google.com/ 

For this workshop we will use the web-based command line, Google Cloud Shell, to eliminate differences in laptop images. 

Open the Google Cloud Shell

![Cloud Shell](https://image.ibb.co/ccoxLF/cloudshell.png)

List all the projects on Google Cloud to make sure everything is working and you're in the right place. 
```
gcloud projects list
```
If you used Google Cloud before you may have more than one project. Make sure you change to your preferred project. If you never used Google Cloud before you can skip this command` line.
```
gcloud config set project [PROJECT_ID]
```
## 2. Clone Github

Clone this Github repo to the Cloud Shell so that you have all demo applications

```
git clone https://github.com/chrisgaun/hands-on-with-kubernetes-gke 
```

Now type "ls" into the command line. You should see the "hands-on-with-kubernetes-gke" repo. 

Change the directory to the cloned repo

```
cd hands-on-with-kubernetes-gke
```

## 3. Provision Cluster

Run the command to create a 3-node cluster on Google cloud. This may take a minute to respond and will need to run for several minutes. 

```
gcloud container clusters create "k8sintelgoogle" \
  --zone "us-east1-c" \
  --machine-type "n1-standard-1" \
  --image-type "GCI" --disk-size "100" \
  --scopes cloud-platform \
  --num-nodes "3"
``` 

## 4. Connect with Cluster

Install kubectl

```
gcloud components install kubectl
```

Get credentials

```
gcloud auth application-default login
```

Configure kubectl with the training cluster context. The 

```
gcloud container clusters get-credentials k8sintelgoogle
```

Verify kubectl can connect to the cluster

```
kubectl cluster-info
```

Since we are using the public cloud command line (essentially a VM in Google Cloud) we need to modify the Kubernetes Dashboard UI service and expose it to the internet

```
kubectl get svc kubernetes-dashboard -n kube-system -o yaml | \
sed "s/ClusterIP/LoadBalancer/" | \
kubectl apply -f - -n kube-system
```
Get the IP of the Dashboard

```
kubectl get svc kubernetes-dashboard -n kube-system -w
```
Grab the IP address from the highlighted below and paste it into your prefered browser

![IP Address](http://i.imgur.com/i1hlPV2.png)

## 5. Run "Hello World"

In the command line, deploy "hello world" application to get something up and running on your new cluster

```
kubectl run hello-world \
--replicas=5 --labels="run=load-balancer-example" \
--image=gcr.io/google-samples/node-hello:1.0  \
--port=8080
```

## 6. Tour of Dashboard (the official UI of Kubernetes)

Instructor will give a tour of the Kubernetes Dashboard
