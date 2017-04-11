# Resource Quota Demo Workflow

Kubernetes can restrict the amount of CPU and Memory for application pods. This is especially useful when Kubernetes cluster is not set to auto-scale and has contrained resources being shared by multiple teams. 

The revelvant Kubernetes documentation is found [here](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

These steps are to be executed from your local machine!

## 1. Navigate to the repository directory on your machine.  

```
$ cd /[LOCATION YOU CLONED THIS REPO]/GKE-hands-on-training
```

## 2. Execute the application service and deployment

```
$ kubectl apply -f examples/resource-quotas/service.yaml
$ kubectl apply -f examples/resource-quotas/deployment.yaml
```

## 3. Locate the pods

```
$ kubectl get pods -o wide
```

You should now see:

```
NAME                                   READY     STATUS    RESTARTS   AGE       IP               NODE
resource-quota-demo-4067652524-01jh5   1/1       Running   0          41s       172.16.235.216   worker1
resource-quota-demo-4067652524-72xxh   1/1       Running   0          41s       172.16.235.217   worker1
resource-quota-demo-4067652524-wnhgn   1/1       Running   0          41s       172.16.235.218   worker1
```

## 4. Obtain the name of the deployment

```
$ kubectl get deployments
```

```
NAME                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
resource-quota-demo   3         3         3            3           1m
```

## 5. Scale the deployment to something silly

Create 100 replicas of this crappy app!

```
$ kubectl scale deployment resource-quota-demo --replicas=100
```

## 6. Check the number of pods in the Kubernetes Dashboard

If you closed the Kuberentes Dashboard, follow the instructions to open Dashboard [here](https://github.com/chrisgaun/GKE-hands-on-training/blob/master/docs/3-build-cluster.md)

Now click on `pods` from the left hand navigation menu.

You should see healthy pods (with green ticks next to them)

However you should see many pods displaying the following:

```
pod (resource-quota-demo-4067652524-jxlrw) failed to fit in any node fit failure summary on nodes : Insufficient cpu (1), Insufficient memory (1)
```

## 7. Check the status of the deployment

We can also see the information by describing the deployment using:

```
$ kubectl describe deployment resource-quota-demo
```

You will see the section: 

```
Type         Status    Reason
Available    false     MinimumReplicasUnavailable 
```

## 8. Scale down the replica count

```
$ kubectl scale deployment resource-quota-demo --replicas=3
```

## 9. Delete the demo

Finally execute the following command to tidy away the demo:

```
$ kubectl delete -f examples/resource-quotas/service.yaml
$ kubectl delete -f examples/resource-quotas/deployment.yaml
```
