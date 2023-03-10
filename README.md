# Apache Airflow in Kubernetes

All credit goes to Yuyu Lin https://sww.sas.com/people/?bool=and&keyword=yuyu+lin&search-type=name 

## Installation on execution on Windows (WSL) and Mac

### WSL

1. Install Docker Desktop https://rndconfluence.sas.com/confluence/display/SASSTUDIO/Setting+Up+a+Development+Environment
2. Install Ubuntu 22.04 https://learn.microsoft.com/en-us/windows/wsl/install
3. Install VSCode https://code.visualstudio.com/docs/remote/wsl
4. Install minikube 
```
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube
$ minikube start
```
5. Install helm
```
$ wget https://get.helm.sh/helm-v3.8.2-linux-amd64.tar.gz
$ tar xvf helm-*-linux-amd64.tar.gz
$ sudo mv linux-amd64/helm /usr/local/bin
```
5. Change the values.yaml to reflect your flow repository
```
$ cd helminstall
$ vi values.yaml # change to your git repo on the gitlab line or just let it use my public one
$ helm install airflow .
$ cd ..
$ kubectl get pods # takes about 5 minutes
NAME                                 READY   STATUS    RESTARTS   AGE
airflow-postgresql-0                 1/1     Running   0          32m
airflow-scheduler-79b98f946d-94kct   2/2     Running   0          32m
airflow-web-59767dfbf6-frlhr         2/2     Running   0          32m
```
6. Run VSCode
```
$ code .
```
7. Forward the port
```
$ kubectl port-forward --namespace default svc/airflow 8080:8080 &
```
8. Bring up Apache Airflow Kubernetes visualizations http://localhost:8080/home
```
username user
password test123
```

## What if somethign gets messed up

Remove airflow and everything out of the cluster start over
```
$ minikube delete
$ minikube start
```

