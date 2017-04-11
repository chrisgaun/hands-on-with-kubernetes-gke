# Kdemo demo notes #

The main repo for kdemo is at [https://github.com/apprenda/kdemo](https://github.com/apprenda/kdemo)

You can clone it with:

```sh
git clone https://github.com/apprenda/kdemo.git
cd kdemo
```

Inside the kdemo project directory there's a `kubernetes/` folder with a few yaml files you can use to create the different resources for a demo.

## For a stadard (amd64) K8s cluster ##

```sh
kubectl create -f kubernetes/kdemo-dep.yaml
kubectl create -f kubernetes/kdemo-svc.yaml
```

This will create a **Deployment** with 2 replicas of the kdemo app and an associated **Service** that exposes it using a NodePort.

To scale the app to 8 replicas you can simply do:

```sh
kubectl scale deployment kdemo-dep --replicas=8
```

To scale it back in to a single replica do:

```sh
kubectl scale deployment kdemo-dep --replicas=1
```

Finally, to remove the resources completely run the following:

```sh
kubectl delete -f kubernetes/kdemo-dep.yaml
kubectl delete -f kubernetes/kdemo-svc.yaml
```

## For a Raspberry Pi (ARM) Mini Cluster ##

### Powering up the Mini Cluster ###

1. Plug in the first Raspberry Pi (the bottom one, without the Blinkt lights) to a mini-USB cable.
2. Wait approximately **2 minutes** for it to boot and for the K8s control plane components to come up.
3. Plug in the rest of the Raspberry Pi's one by one, starting with the second one (lowest) and moving upwards, waiting a few seconds between each one.
4. As the nodes come up the Blinkt should show a *startup* animation (green light expanding outwards).
5. After all four nodes show the animation the cluster should be ready.

### Connect to the Raspberry Pi Mini Cluster WiFi Access Point ###

From your computer, use your network settings interface to connect to the WiFi Access Point with an SSID of `K8sMiniCluster` and use the WAP2 password you received separately to authenticate. You should be connected to the cluster's master node in a few seconds. You can test basic connectivity by pinging it like this:

```sh
ping 192.168.2.10
```

### Configure `kubectl` to Connect to the Mini Cluter ###

To control the mini cluster your `kubectl` client must use the proper configuration file for authentication. Please make sure that you have the K8s `config` file you received separately in the proper location so that the `kubectl` command can use it.

### Clone the Blinkt Controller Repo ###

In addition to the previous repo, you should clone this one [https://github.com/apprenda/blinkt-k8s-controller](https://github.com/apprenda/blinkt-k8s-controller)

You can change back to the parent directory and clone it with:

```
cd ..
git clone https://github.com/apprenda/blinkt-k8s-controller.git
cd blinkt-k8s-controller
```

This repo contains the project for controlling the Blinkt LEDs in the Raspberry Pi mini cluster.

### Starting and Stopping the Blinkt DaemonSet Controller ###

The DaemonSet should already be running on the mini cluster, so it should't be necessary to start it manually. However, if you want to demo tearing it down and recreating it you can run the following commands (make sure you're inside the `blinkt-k8s-controller` project you just cloned):

To tear it down:

```
kubectl delete -f kubernetes/blinkt-k8s-controller-ds.yaml
```

You should see the *shutdown* animation (contracting red lights) on every node.

To bring it back up:

```
kubectl create -f kubernetes/blinkt-k8s-controller-ds.yaml
```

You should see the *startup* (green) animation again on all nodes.

### Deploying kdemo to the Raspberry Pi Mini Cluster ###

Switch back to the `kdemo` project directory.

If you cloned them both to the same parent directory you can do:

```sh
cd ../kdemo
```

Create a **Deployment** of kdemo with a single replica.

```sh
kubectl create -f kubernetes/kdemo-dep-arm.yaml
```

A blue light should light up in one of the Blinkts.

Just like before, to scale the app to 16 replicas you can simply do:

```
kubectl scale deployment kdemo-dep --replicas=16
```

Half of the lights should now be lit in blue.

To scale it back in to a single replica do:

```
kubectl scale deployment kdemo-dep --replicas=1
```

Finally, to remove the resources completely run the following:

```
kubectl delete -f kubernetes/kdemo-dep-arm.yaml
```
