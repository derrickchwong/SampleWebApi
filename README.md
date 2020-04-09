
# a sample ASP.NET Core webapi

## pre-requisite

1. ensure you have dotnet core installed
2. docker engine installed

The following was tested based on the following on MacOS Mojave 10.14.6 (18G103)

```
$ dotnet --version
3.0.100
```

```
$ docker -v
Docker version 19.03.4, build 9013bf5
```

## how to create this project

```
$ dotnet new webapp -o SampleWebApi --no-https
```

## build docker image using Tanzu Build Service

```
⇒  pb image apply -f image-config.yml -p ./SampleWebApi
```

## check the build status 

```
⇒  pb image builds harbor.derrickwong.hk/apps/dotnet-core-sample-web-api:0.0.1
Build    Status      Started Time           Finished Time          Reason    Digest
-----    ------      ------------           -------------          ------    ------
    1    SUCCESS     2020-04-09 00:46:41    2020-04-09 00:48:29    CONFIG    93f2fd43b6b3390e30c7c9e5ffdd0fd13d2911a7f7170eefd3e719378b4a1d75
    2    SUCCESS     2020-04-09 01:00:43    2020-04-09 01:01:49    COMMIT    ed1663c64d59c8a3802f8ec9c6f2743ff6e7b98316945cfb4e0b4f95e9a00018
    3    SUCCESS     2020-04-09 01:08:20    2020-04-09 01:10:28    CONFIG    476ea9f2afb18fe8b7e24847b744f41b9564be2f8632d5442ec8cee779655272
    4    SUCCESS     2020-04-09 01:10:28    2020-04-09 01:12:00    CONFIG    344e3768cac4080eca81b187fb66aadf6383c40707a1135ffc3a93c91472c0cf
    5    BUILDING    2020-04-09 09:04:38    --                     CONFIG    --
```

## check the build log

```
⇒  pb image logs harbor.derrickwong.hk/apps/dotnet-core-sample-web-api:0.0.1 -b 5 -f
[setup-ca-certs] setup-ca-certs:main.go:15: create certificate...
[setup-ca-certs] setup-ca-certs:main.go:21: populate certificate...
[setup-ca-certs] setup-ca-certs:main.go:32: update CA certificates...
[setup-ca-certs] setup-ca-certs:main.go:39: copying CA certificates...
[setup-ca-certs] setup-ca-certs:main.go:45: finished setting up CA certificates
[setup-ca-certs]
[prepare] prepare:fetch.go:43: Successfully pulled harbor.derrickwong.hk/apps/dotnet-core-sample-web-api-source@sha256:f4043c9f864a87257e9ea76db4f192ed1e8f61477f43468884e7463132fe05e1 in path "/workspace"
[prepare]
[detect] 5 of 7 buildpacks participating
[detect] org.cloudfoundry.dotnet-core-runtime 0.0.127
[detect] org.cloudfoundry.dotnet-core-aspnet  0.0.118
[detect] org.cloudfoundry.dotnet-core-sdk     0.0.122
[detect] org.cloudfoundry.dotnet-core-build   0.0.68
[detect] org.cloudfoundry.dotnet-core-conf    0.0.115
[detect]
[analyze] Restoring metadata for "org.cloudfoundry.dotnet-core-runtime:aa9fc821099a28966d72d662c150c0caee729c4de99620e3f8aac10347d86c8e" from cache
[analyze] Restoring metadata for "org.cloudfoundry.dotnet-core-aspnet:5736292f80a9d921989072162b7ac6aca4f6381957c9e15c30e1b9fa073eb14e" from cache
[analyze] Restoring metadata for "org.cloudfoundry.dotnet-core-sdk:d70d8e29262b98bc24c6fd6b625bc6e7e9b06199631e469a5171347a9168c5e4" from cache
[analyze]
[restore] Restoring data for "org.cloudfoundry.dotnet-core-runtime:aa9fc821099a28966d72d662c150c0caee729c4de99620e3f8aac10347d86c8e" from cache
[restore] Restoring data for "org.cloudfoundry.dotnet-core-aspnet:5736292f80a9d921989072162b7ac6aca4f6381957c9e15c30e1b9fa073eb14e" from cache
[restore] Restoring data for "org.cloudfoundry.dotnet-core-sdk:d70d8e29262b98bc24c6fd6b625bc6e7e9b06199631e469a5171347a9168c5e4" from cache
[restore]
[build]
[build] .NETCore Runtime Buildpack 0.0.127
[build]    3.1.2: Contributing to layer
[build]     Reusing cached download from previous build
[build]     Expanding to /layers/org.cloudfoundry.dotnet-core-runtime/dotnet-runtime
[build]     Writing DOTNET_ROOT to shared
[build]     Writing RUNTIME_VERSION to build
[build]
[build] ASPNetCore Buildpack 0.0.118
[build]    3.1.2: Contributing to layer
[build]     Reusing cached download from previous build
[build]     Expanding to /layers/org.cloudfoundry.dotnet-core-aspnet/dotnet-aspnetcore
[build]   ASPNetCore Buildpack 0.0.118: Contributing to layer
[build]     Writing DOTNET_ROOT to shared
[build]
[build] .NET SDK Buildpack 0.0.122
[build]    3.1.102: Contributing to layer
[build]     Reusing cached download from previous build
[build]     Expanding to /layers/org.cloudfoundry.dotnet-core-sdk/dotnet-sdk
[build]     Writing SDK_LOCATION to build
[build]   .NET SDK Buildpack 0.0.122: Contributing to layer
[build]     Symlinking runtime libraries
[build]     Moving dotnet driver from /layers/org.cloudfoundry.dotnet-core-sdk/dotnet-sdk
[build]     Writing PATH to shared
[build]     Writing DOTNET_ROOT to shared
[build]
[build] .Net Build Buildpack 0.0.68
[build]   : Contributing to layer
[build]     Symlinking runtime libraries
[build]     Moving dotnet driver from /layers/org.cloudfoundry.dotnet-core-sdk/driver-symlinks
[build]     Symlinking the SDK from /layers/org.cloudfoundry.dotnet-core-sdk/dotnet-sdk
[build]   : Contributing to layer
[build]     Publishing source code
[build]
[build] Welcome to .NET Core 3.1!
[build] ---------------------
[build] SDK Version: 3.1.102
[build]
[build] Telemetry
[build] ---------
[build] The .NET Core tools collect usage data in order to help us improve your experience. The data is anonymous. It is collected by Microsoft and shared with the community. You can opt-out of telemetry by setting the DOTNET_CLI_TELEMETRY_OPTOUT environment variable to '1' or 'true' using your favorite shell.
[build]
[build] Read more about .NET Core CLI Tools telemetry: https://aka.ms/dotnet-cli-telemetry
[build]
[build] ----------------
[build] Explore documentation: https://aka.ms/dotnet-docs
[build] Report issues and find source on GitHub: https://github.com/dotnet/core
[build] Find out what's new: https://aka.ms/dotnet-whats-new
[build] Learn about the installed HTTPS developer cert: https://aka.ms/aspnet-core-https
[build] Use 'dotnet --help' to see available commands or visit: https://aka.ms/dotnet-cli-docs
[build] Write your first app: https://aka.ms/first-net-core-app
[build] --------------------------------------------------------------------------------------
[build] Microsoft (R) Build Engine version 16.4.0+e901037fe for .NET Core
[build] Copyright (C) Microsoft Corporation. All rights reserved.
[build]
[build]   Restore completed in 387.54 ms for /workspace/SampleWebApi.csproj.
[build]   SampleWebApi -> /workspace/bin/Release/netcoreapp3.1/ubuntu.18.04-x64/SampleWebApi.dll
[build]   SampleWebApi -> /workspace/bin/Release/netcoreapp3.1/ubuntu.18.04-x64/SampleWebApi.Views.dll
[build]   SampleWebApi -> /workspace/
[build]
[build] .NET Core Conf Buildpack 0.0.115
[build]   Process types:
[build]     web: cd /workspace && ./SampleWebApi --urls http://0.0.0.0:${PORT}
[build]
[export] Reusing layers from image 'harbor.derrickwong.hk/apps/dotnet-core-sample-web-api@sha256:344e3768cac4080eca81b187fb66aadf6383c40707a1135ffc3a93c91472c0cf'
[export] Reusing layer 'launcher'
[export] Reusing layer 'org.cloudfoundry.dotnet-core-runtime:dotnet-runtime'
[export] Reusing layer 'org.cloudfoundry.dotnet-core-aspnet:aspnet-symlinks'
[export] Reusing layer 'org.cloudfoundry.dotnet-core-aspnet:dotnet-aspnetcore'
[export] Reusing layer 'org.cloudfoundry.dotnet-core-sdk:driver-symlinks'
[export] Adding 1/1 app layer(s)
[export] Reusing layer 'config'
[export] *** Images (sha256:afd30e42250ca9f1f337b676337c4d8190933e74585032a111c6a5d774389411):
[export]       harbor.derrickwong.hk/apps/dotnet-core-sample-web-api:0.0.1
[export]       harbor.derrickwong.hk/apps/dotnet-core-sample-web-api:0.0.1-b5.20200409.010438
[export] Reusing cache layer 'org.cloudfoundry.dotnet-core-runtime:aa9fc821099a28966d72d662c150c0caee729c4de99620e3f8aac10347d86c8e'
[export] Reusing cache layer 'org.cloudfoundry.dotnet-core-aspnet:5736292f80a9d921989072162b7ac6aca4f6381957c9e15c30e1b9fa073eb14e'
[export] Reusing cache layer 'org.cloudfoundry.dotnet-core-sdk:d70d8e29262b98bc24c6fd6b625bc6e7e9b06199631e469a5171347a9168c5e4'
[export]
```

## to test run image


```
docker run --rm -it -p 8000:80 sample-webapi:0.1.0
```

test it with curl or browser
```
curl http://localhost:8000/weatherforecast
```

### with https, run the following command

if you created the app with https then you will need a certificate to run and test your application.


**Generate certificate and configure local machine**

This will generate a certificate and you need to specify a password for the certificate.

```
dotnet dev-certs https -ep ${HOME}/.aspnet/https/aspnetapp.pfx -p password
dotnet dev-certs https --trust
```

**run the container**

-v : mount the certificate in your local machine to the container
-p : forward a local machine port to container port e.g. forward local port 8000 (http) to container port 80
-e : environment variables for donet container to be overriden.

```
docker run --rm -it -p 8000:80 -p 8001:443 -e ASPNETCORE_URLS="https://+;http://+" -e ASPNETCORE_HTTPS_PORT=8001 -e ASPNETCORE_Kestrel__Certificates__Default__Password="password" -e ASPNETCORE_Kestrel__Certificates__Default__Path=/https/aspnetapp.pfx -v ${HOME}/.aspnet/https:/https/ sample-webapi:0.1.0
```

**test it**
```
curl https://localhost:8001/weatherforecast
```


## push to dockerhub

### tag it 

you will need to replace <dockerhub-user-id> with your dockerhub id, if you don't have one, sign up [here](https://hub.docker.com/signup).

```
docker tag sample-webapi:0.1.0 <dockerhub-user-id>/sample-webapi:0.1.0
```

### push to dockerhub


```
docker push <dockerhub-user-id>/sample-webapi:0.1.0
```

# Kubernetes deployment

if you have a kubernetes cluster you can test out the following.

for local testing you can used Docker Decktop Kubernetes, a single node local kubernetes cluster.

## testing the cluster

```
kubectl cluster-info
Kubernetes master is running at https://kubernetes.docker.internal:6443
KubeDNS is running at https://kubernetes.docker.internal:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

## check current kube context

```
kubectl config get-context
```

## set kube context

If you have docker kubernetes running, set to docker-desktop context with the following command

```
kubectl config use-context docker-desktop
Switched to context "docker-desktop".
```

## to deploy 

change folder to ./SampleWebApi and run the following commands, it will deploy the application to docker-desktop kubernetes.

ensure the image used in the deployment is the tag you create with docker build and tag.

```
kubectl apply -f k8s/sample-webapi.yaml
kubectl get deployment
kubectl get pods
kubectl get services
```

## check deployment

the deployment will deploy 2 replica

```
kubectl get pods
NAME                                    READY   STATUS    RESTARTS   AGE
js-webapi-deployment-54df447bd8-rn7xh   1/1     Running   0          2m54s
js-webapi-deployment-54df447bd8-vbnzs   1/1     Running   0          2m54s
```

to access the application in browser, you need to get the NodePort of the service.

```
kubectl get services
NAME                TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
js-webapi-service   NodePort    10.101.26.17   <none>        8080:31740/TCP   8m15s
kubernetes          ClusterIP   10.96.0.1      <none>        443/TCP          10m
```

access the app: http://localhost:31740/weatherforecast

## scale the deployment

to scale from 2 to 3 replica, run the following command

```
kubectl scale --replicas=3 deployment js-webapi-deployment
deployment.extensions/js-webapi-deployment scaled

kubectl get pods
NAME                                    READY   STATUS    RESTARTS   AGE
js-webapi-deployment-54df447bd8-gscck   1/1     Running   0          14s
js-webapi-deployment-54df447bd8-rn7xh   1/1     Running   0          6m47s
js-webapi-deployment-54df447bd8-vbnzs   1/1     Running   0          6m47s
```

# service with LoadBalancer

edit the file k8s/sample-webapi.yaml

change service ```type: NodePort``` to ```type: LoadBalancer``` and run the following command 

```
kubectl apply -f k8s/sample-webapi.yaml
service/js-webapi-service configured
deployment.apps/js-webapi-deployment unchanged
```

you can access the application at : http://localhost:8080/weatherforecast

## to remove deployment

```
kubectl delete -f k8s/sample-webapi.yaml
service "js-webapi-service" deleted
deployment.apps "js-webapi-deployment" deleted
```

## deploy Kubernetes Dashboard

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml
```

To access Dashboard from your local workstation you must create a secure channel to your Kubernetes cluster. Run the following command:

```
kubectl proxy
```

Now access Dashboard at:

http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/

you get token to login, copy the token and provide it for login with TOKEN.

```
kubectl -n kube-system describe secret default
```

or 

```
TOKEN=`kubectl -n kube-system describe secret default | grep 'token:' | awk '{print $2}'`
kubectl config set-credentials docker-desktop --token="${TOKEN}"
```

# Using Helm

to setup helm with docker-decktop kubenetes

## Requirement
- download helm 


## install tiller 

ensure you are using docker-desktop kubernetes

```
kubectl config current-context
docker-desktop
```

then install tiller 

```
helm init
```

check tiller is up and running

```
kubectl get pods -n kube-system
NAME                                     READY   STATUS    RESTARTS   AGE
coredns-6dcc67dcbc-2sj96                 1/1     Running   0          162m
coredns-6dcc67dcbc-rts84                 1/1     Running   0          162m
etcd-docker-desktop                      1/1     Running   0          161m
kube-apiserver-docker-desktop            1/1     Running   0          161m
kube-controller-manager-docker-desktop   1/1     Running   0          161m
kube-proxy-n268j                         1/1     Running   0          162m
kube-scheduler-docker-desktop            1/1     Running   0          161m
kubernetes-dashboard-5f7b999d65-k4jbs    1/1     Running   0          104m
tiller-deploy-fc56b78dd-cdhn9            1/1     Running   0          4m32s
```

## package the app in helm


create the helm chart

```
helm create dotnet3-webapi-chart
```

install chart

```
helm install --name js-dotnet3-webapi dotnet3-webapi-chart
```

delete chart

```
helm delete js-dotnet3-webapi
```





# helm chart

the following commands required ```--tls``` with IBM Cloud Private 3.2.1 on Red Hat OKD 3.11 

## deploy dry-run

```
cloudctl login -a https://<Cluster Master Host>:<Cluster Master API Port> --skip-ssl-validation
```

with ICP 3.2.1 you should see the following when you run helm version command

```
helm version --tls
Client: &version.Version{SemVer:"v2.12.3", GitCommit:"eecf22f77df5f65c823aacd2dbd30ae6c65f186e", GitTreeState:"clean"}
Server: &version.Version{SemVer:"v2.12.3+icp", GitCommit:"", GitTreeState:""}
```

## create the chart

```
helm create dotnet3-webapi-chart
```

the above command will create a folder with the following structure

```
.
├── Chart.yaml
├── README.md
├── charts
├── templates
│   ├── NOTES.txt
│   ├── _helpers.tpl
│   ├── deployment.yaml
│   ├── ingress.yaml
│   ├── service.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml
```

where I have added README.md and modified values.yaml, deployment.yaml, service.yaml 

## test run your helm chart

you can test run your helm chart to check the output of the deployment as follows.

```
helm install --dry-run --debug ./dotnet3-webapi-chart --tls
```

## to deploy it

```
helm install --name js-dotnet3-webapi ./dotnet3-webapi-chart --tls
```

## listing of helm deployment

```
helm list

NAME                    REVISION        UPDATED                         STATUS          CHART                           APP VERSION     NAMESPACE
js-dotnet3-webapi       1               Wed Nov 27 20:48:21 2019        DEPLOYED        dotnet3-webapi-chart-0.1.0      1.0             default  

```

## to access the application

the application is deployed using NodePort to get the port value, run the following command

```
$ kubectl get services
NAME                                     TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
js-dotnet3-webapi-dotnet3-webapi-chart   NodePort    10.96.127.31   <none>        5000:31855/TCP   41s
kubernetes                               ClusterIP   10.96.0.1      <none>        443/TCP          5h32m
```

access the application API at http://localhost:31855/weatherforecast

## remove deployment

```
helm delete js-dotnet3-webapi --purge --tls
```

## ensure best practices in chart

```
helm lint ./dotnet3-webapi-chart
==> Linting ./dotnet3-webapi-chart
[INFO] Chart.yaml: icon is recommended

1 chart(s) linted, no failures
```

## to share it 

in order to share this chart, you need to package it as archive.

``` helm package ./dotnet3-webapi-chart ``` 

deploying with archive

``` helm install --name js-dotnet3-webapi dotnet3-webapi-chart-0.1.0.tgz --tls
```

# Using Operator Framework

## create a new operator from existing helm 

```
operator-sdk new dotnet3-webapi-operator --type=helm --helm-chart ./dotnet3-webapi-chart
```

change folder to ./dotnet3-webapi-operator and run the following command to build the image

## build it

```
operator-sdk build jaricsng/dotnet3-webapi-operator:0.1.0
```

push it to dockerhub

```
docker login
docker push jaricsng/dotnet3-webapi-operator:0.1.0
```

## deploy it

update the image name and tag in file ./dotnet3-webapi-operator/deploy/operator.yaml and then deploy it with the following commands

Before running the operator, the CRD must be registered with the Kubernetes apiserver

```
kubectl apply -f ./dotnet3-webapi-operator/deploy/crds/charts.helm.k8s.io_dotnet3webapicharts_crd.yaml

customresourcedefinition.apiextensions.k8s.io/dotnet3webapicharts.charts.helm.k8s.io created
```

Setup RBAC and deploy the webapi-operator
```
kubectl apply -f ./dotnet3-webapi-operator/deploy/service_account.yaml

serviceaccount/dotnet3-webapi-operator created
```

```
kubectl apply -f ./dotnet3-webapi-operator/deploy/role.yaml

role.rbac.authorization.k8s.io/dotnet3-webapi-operator created
```

```
kubectl apply -f ./dotnet3-webapi-operator/deploy/role_binding.yaml

rolebinding.rbac.authorization.k8s.io/dotnet3-webapi-operator created
```

finally, run the webapi-operator 
```
kubectl apply -f ./dotnet3-webapi-operator/deploy/operator.yaml

deployment.apps/dotnet3-webapi-operator created
```

### Verify that the Deployment is up and running

```
kubectl get deployment

NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
dotnet3-webapi-operator   1/1     1            1           9s
```

### Verify that the Pod is up and running

```
kubectl get pod

NAME                                       READY   STATUS    RESTARTS   AGE
dotnet3-webapi-operator-674666d495-c2zrl   1/1     Running   0          16s
```

## Create the example SampleWebApi with the Controller (CR)

to deploy a sample webapi using the controller (CR), run the command 

```
kubectl apply -f ./dotnet3-webapi-operator/deploy/crds/charts.helm.k8s.io_v1alpha1_dotnet3webapichart_cr.yaml

dotnet3webapichart.charts.helm.k8s.io/example-dotnet3webapichart created
```

Ensure that the webapi-operator creates the deployment for the CR

```
kubectl get deployment

NAME                                              READY   UP-TO-DATE   AVAILABLE   AGE
dotnet3-webapi-operator                           1/1     1            1           2m9s
example-dotnet3webapichart-dotnet3-webapi-chart   2/2     2            2           21s
```

Check the pods and CR status to confirm the status is updated with the webapi pod names

the controller will deploy 2 replica as defined in the deployment in helm chart.

```
kubectl get pods

NAME                                                              READY   STATUS    RESTARTS   AGE
dotnet3-webapi-operator-674666d495-ct2bf                          1/1     Running   0          2m28s
example-dotnet3webapichart-dotnet3-webapi-chart-5647495ff47vw78   1/1     Running   0          40s
example-dotnet3webapichart-dotnet3-webapi-chart-5647495ff4x4886   1/1     Running   0          40s
```

## clean up

```
kubectl delete -f ./dotnet3-webapi-operator/deploy/crds/charts.helm.k8s.io_v1alpha1_dotnet3webapichart_cr.yaml

dotnet3webapichart.charts.helm.k8s.io "example-dotnet3webapichart" deleted
```

```
kubectl delete -f ./dotnet3-webapi-operator/deploy/crds/charts.helm.k8s.io_dotnet3webapicharts_crd.yaml

customresourcedefinition.apiextensions.k8s.io "dotnet3webapicharts.charts.helm.k8s.io" deleted
```

```
kubectl delete -f ./dotnet3-webapi-operator/deploy/operator.yaml

deployment.apps "dotnet3-webapi-operator" deleted
```

```
kubectl delete -f ./dotnet3-webapi-operator/deploy/role_binding.yaml

rolebinding.rbac.authorization.k8s.io "dotnet3-webapi-operator" deleted
```

```
kubectl delete -f ./dotnet3-webapi-operator/deploy/role.yaml

role.rbac.authorization.k8s.io "dotnet3-webapi-operator" deleted
```

```
kubectl delete -f ./dotnet3-webapi-operator/deploy/service_account.yaml

serviceaccount "dotnet3-webapi-operator" deleted
```

# Appsody Stack

```
appsody stack create dotnet3-webapi-stack
```

the above command will create a structure as shown below

```
.
├── README.md
├── image
│   ├── Dockerfile-stack
│   ├── LICENSE
│   ├── config
│   │   └── app-deploy.yaml
│   └── project
│       └── Dockerfile
├── stack.yaml
└── templates
    └── hello
```
