# Build the Kubernetes Cluster
In the following section, there are commands highlighted in grey. You will copy and paste the commands into the Google CLoud Shell command prompt - $. The actual $ symbol is disregarded to make it easy to cut and paste. 
```
$
```
**Tips for those who have not used a command line in ages**

It may take few minutes for a command prompt to respond. However, if it ever gets stuck you can use "ctrl+c" to get back to the command line. 

You can use the up arrow to find previous entered commands. 

To copy from the command line, simply highlight (no ctrl+c !) 

## 1. Sign into Google Cloud

Navigate to the Google Cloud portal: https://console.cloud.google.com/ 

For this workshop we will use the web-based command line, Google Cloud Shell, to eliminate differences in laptop images. 

Open the Google Cloud Shell

![Cloud Shell](https://image.ibb.co/ccoxLF/cloudshell.png)

List all the projects on Google Cloud to make sure everything is working and you're in the right place. 
```
gcloud projects list
```
Set default zone in Google Cloud for the workshop
```
gcloud config set compute/zone us-east1-c
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

Run the command to create a 3-node cluster on Google cloud. This may take a minute to respond and will need to run for several minutes. It is a good time for a bathroom break.  

```
gcloud container clusters create "k8sintelgoogle" \
  --zone "us-east1-c" \
  --machine-type "n1-standard-1" \
  --image-type "GCI" --disk-size "100" \
  --scopes cloud-platform \
  --num-nodes "3"
``` 
When the command is finishing executing, you will see output like this
![Imgur](http://i.imgur.com/zAMyyez.png)

You should also navigate to the Google Container Engine section of the Google Cloud Portal https://console.cloud.google.com/kubernetes/list You should see the your newly created Kubernetes cluster.

Now navigate to the Google compute section and you will see the virtual machines that are hosting the Kubernetes fabric https://console.cloud.google.com/compute/instances  

## 4. Connect with Cluster

Make sure kubectl is up to date

```
gcloud components install kubectl
```

Configure kubectl with the training cluster context. 

```
gcloud container clusters get-credentials k8sintelgoogle \
--zone us-east1-c 
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
Grab the external IP address from the highlighted below and paste it into your prefered browser (your IP will be different from one below) 

![IP Address](http://i.imgur.com/i1hlPV2.png)

## 5. Run "Hello World"

In the command line, deploy "hello world" application to get something up and running on your new cluster

```
kubectl run hello-world \
--replicas=5 --labels="run=load-balancer-example" \
--image=gcr.io/google-samples/node-hello:1.0  \
--port=8080
```
Navigate to the "pods" section in the Kubernetes Dashboard you just opened up in the browser window. You should see "pods" being created. 

![Imgur](http://i.imgur.com/j8oVACv.png)

## 6. Tour of Dashboard (the official UI of Kubernetes)

Instructor will give a tour of the Kubernetes Dashboard and cover the constructs of Kubernetes. 
