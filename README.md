# Hands on with Kubernetes Workshops

The following repository will create you a Kubernetes cluster using the following:

1. Sign up for a Google Cloud account:
    1. FREE TRIAL: $300 of Google Cloud for 12 months https://cloud.google.com/free/
    2. FREE KUBERNETES TIER: up to 5 nodes of Google Container Engine (GKE) are free. Note the underlining Google Compute Engine counts towards the $300 from the FREE TRIAL.    
2. Download Google SDK for Mac, Linux or Windows: https://cloud.google.com/sdk/downloads
3. Clone of this repo to upload applications.

## Course Documents

Join the course's Slack: [![Slackin](http://54.242.94.98/badge.svg)](http://54.242.94.98/)

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
