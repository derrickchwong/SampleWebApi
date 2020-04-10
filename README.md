
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

## update Harbor URL and Repo name

You need a Private Docker Registry and we recommend VMWare Harbor. Replace \<harbor-url\> and \<repo\> in image-config.yml and deploy.yml with your URL and repo name.

## build docker image using Tanzu Build Service

```
⇒  pb image apply -f image-config.yml -p .
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

if success, you can check your Harbor repo if the image is pushed.

## to test run image

```
docker run -e PORT=5000 -p 5000:5000 \<harbor-url\>/\<repo\>/dotnet-core-sample-web-api:0.0.1
```

test it with curl or browser
```
curl http://localhost:5000
```

# Kubernetes deployment

## to deploy

```
kubectl apply -f deploy.yml
```

A service and deployment will be created. Use below command to check the external IP

```
⇒  kubectl get svc dotnet-core-sample-web-api
NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)          AGE
dotnet-core-sample-web-api   LoadBalancer   10.100.200.129   34.69.62.134   5000:31602/TCP   52s
```

access the app: http://\<externam-ip\>:5000/

## to remove deployment

```
kubectl delete -f deploy.yaml
```
