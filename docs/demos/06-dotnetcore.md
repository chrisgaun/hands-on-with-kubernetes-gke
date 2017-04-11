# dotnetcore Workflow

These steps are executed from `kubectl` against your cluster

## 1. Navigate to your local repository directory

```
$ cd [pathtorepository]/GKE-hands-on-training
```

## 2. Execute the Kubernetes service and application deployment

```
$ kubectl apply -f examples/dotnetcore/service.yaml
$ kubectl apply -f examples/dotnetcore/deployment.yaml
```

## 3. Display the pods running which are serving our application

Execute the following command:

```
$ kubectl get pods -o wide
```

You should now see

```
NAME                           READY     STATUS    RESTARTS   AGE       IP               NODE
probes-demo-1216114202-fkbjn   0/1       Running   0          13s       172.16.235.211   worker1
probes-demo-1216114202-jl08v   0/1       Running   0          13s       172.16.235.212   worker1
probes-demo-1216114202-wv5jx   0/1       Running   0          13s       172.16.235.210   worker1
```

## 4. Browse to the Kubernetes Dashboard

Start a local proxy to your dashboard
```
kubectl proxy
```

Open the URL `http://localhost:8001/ui`


## 5. Obtain the public IP and port of the service

```
$ kubectl get services
```

You should now be seeing:

```
root@bootstrap-node:~/hands-on-with-kubernetes-workshop# kubectl get services
NAME          CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes    172.17.0.1      <none>        443/TCP        1h
dotnetcorek8s-v1   172.17.120.67   <nodes>       80:30226/TCP   1m
```

## 6. Browse to the website

*GET*

Now from your browser browse to `http://<public ip>/api/hello`

Your browser will display "Hello!"

*POST*

The dotnetcore api also allows POST requests to this endpoint with a parameter called `myname`.
Add `?myname=YOURNAME` to the URL above and your browser will display "Ahoy there, YOURNAME!"


## 11. Delete the demo

Finally execute the following command to tidy away the demo:

```
$ kubectl delete -f examples/dotnetcore/service.yaml
$ kubectl delete -f examples/dotnetcore/deployment.yaml
```
