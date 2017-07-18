# Hands on with Kubernetes Workshop Series - GKE

The following repository will help you create a Kubernetes cluster running on Google Container Engine:

1. Sign up for a Google Cloud account:
    1. FREE TRIAL: $300 of Google Cloud for 12 months https://cloud.google.com/free/
    2. FREE KUBERNETES TIER: up to 5 nodes of Google Container Engine (GKE) are free. Note the underlining Google Compute Engine counts towards the $300 from the FREE TRIAL. 
    3. Keep the Google Cloud console open once you signed up: https://console.cloud.google.com/ 
2. Click link to navigate in the Google Cloud Console to API Manager > Library https://console.cloud.google.com/apis/library. Enable the Compute Engine and Container Engine API: 
![Compute and Container Engine](http://i.imgur.com/obCh0lP.png)
![Enable APIs](http://i.imgur.com/BThkhfK.png)
3. Download Google SDK for Mac, Linux or Windows: https://cloud.google.com/sdk/. During this workshop we will use the Google Cloud shell but in everyday usage you would use the SDK to run commands in PowerShell (Windows) or the Mac OS X terminal. 
4. Clone of this repo to upload applications (upper right corner of this page)

![Clone Repo](http://i.imgur.com/2xplb5C.png)

## Course Documents

Join the course's Slack:

 [![Slackin](http://54.242.94.98/badge.svg)](http://54.242.94.98/)

You will find the presentation, links, commands and group questions pinned in the _#k8satgoogle_ channel

## Create Infrastructure & Provision Cluster

A list of steps to build and provision the Kubernetes cluster can be found [here](docs/3-build-cluster.md)

## Using Kubernetes

The presenter will go through a list of demos during the workshop.

Find the demos [here](docs/demos)

## Destroying Cluster After Training

Congrats on finishing the hands on introduction to Kubernetes!

To remove the Kubernetes cluster and underlying infrastructure execute the following from your local machine.

```
$ gcloud container clusters delete [NAME OF CLUSTER] --zone "[ZONE]"
```
If you used the standard command in this workshop to start the cluster than copy and paste the following:

```
$ gcloud container clusters delete k8strainingcluster --zone "us-west1-a"
```
You will still have roughly $300 in Google Cloud credits you can use to test out Kubernetes more.

## Reference

Kubernetes vs. Mesos Marathon vs. Docker Swarm vs. Cloud Foundry SWOT analysis found [here](https://apprenda.com/white-papers/container-orchestration-comparison-guide/)

Learn Why CTO's and Developers are Choosing Kubernetes [here](https://apprenda.com/why-kubernetes/)

Join the Kubernetes community [here](https://github.com/chrisgaun/GKE-hands-on-training/blob/master/community.md)

The Google SDK Container commands are found [here](https://cloud.google.com/sdk/gcloud/reference/container/)

***Kubernetes command line (Kubectl) cheat sheet*** [here](https://kubernetes.io/docs/user-guide/kubectl-cheatsheet/)


## Brought To You By

![Apprenda](https://upload.wikimedia.org/wikipedia/commons/c/cc/Apprenda_logo.png)

![Intel](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/Intel-logo.svg/320px-Intel-logo.svg.png)

![Google Cloud Platform](https://cloud.google.com/_static/1c93cfc82f/images/cloud/gcp-logo.svg)

