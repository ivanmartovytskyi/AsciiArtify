# Tools for running Kubernetes cluster locally

## Minicube

[minikube](https://minikube.sigs.k8s.io/docs/start/) is local Kubernetes, focusing on making it easy to learn and develop for Kubernetes.
All you need is Docker (or similarly compatible) container or a Virtual Machine environment, and Kubernetes is a single command away: minikube start

## Kind

[kind](https://kind.sigs.k8s.io/docs/user/quick-start/) is a tool for running local Kubernetes clusters using Docker container “nodes”.
kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

## K3d

[k3d](https://k3d.io/v5.5.1/) is a lightweight wrapper to run k3s (Rancher Lab’s minimal Kubernetes distribution) in docker.
k3d makes it very easy to create single- and multi-node k3s clusters in docker, e.g. for local development on Kubernetes.
Note: k3d is a community-driven project but it’s not an official Rancher (SUSE) product.

## Features
| Tool      | Description                                                         | Podman Support | Advantages                                                                                                      | Disadvantages                                                                                                                      |
|-----------|---------------------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| minikube  | - Supported OS: Windows, macOS, Linux                               | No             | - Ease of use                                                                                                  | - Deployment speed may be slow for large projects                                                                                    |
|           | - Architectures: x86, x86-64, ARM                                   |                | - Wide community support                                                                                       | - Dependency on virtualization technologies like VirtualBox or Docker Desktop                                                       |
|           | - Automation: Yes                                                   |                | - Documentation                                                                                                |                                                                                                                                    |
|           | - Additional features: Monitoring (via addons), Kubernetes management (kubectl) |            |                                                                                                                |                                                                                                                                    |
| kind      | - Supported OS: Windows, macOS, Linux                               | Yes            | - Deployment speed                                                                                             | - May be more complex to configure and customize                                                                                     |
|           | - Architectures: x86, x86-64, ARM                                   |                | - Ease of use                                                                                                  | - Possible stability issues under heavy loads                                                                                       |
|           | - Automation: Yes                                                   |                | - Flexibility in managing Kubernetes clusters                                                                 |                                                                                                                                    |
|           | - Additional features: Monitoring (depends on the tool used), Kubernetes management (kubectl) | |                                                                       |                                                                                                                                    |
| k3d       | - Supported OS: Windows, macOS, Linux                               | Yes            | - Deployment speed                                                                                             | - Possible stability issues under heavy loads                                                                                       |
|           | - Architectures: x86, x86-64, ARM                                   |                | - Ease of use                                                                                                  |                                                                                                                                    |
|           | - Automation: Yes                                                   |                | - Flexibility in managing Kubernetes clusters                                                                 |                                                                                                                                    |
|           | - Additional features: Monitoring (depends on the tool used), Kubernetes management (kubectl) | |                                                                       |                                                                                                                                    |

## Conclusion

I recommend using minikube as the most mature tool for local testing with convenient monitoring tools, addons, and a strong community. But in case you still have problems with docker licensing, you can consider kind as a tool that fully supports work with podman.

## Demo

![minikube cluster](https://github.com/ivanmartovytskyi/AsciiArtify/blob/demo.gif)

## Instructions(Ubuntu 20.04 LTS)

### Install minikube
> curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

> sudo install minikube-linux-amd64 /usr/local/bin/minikube

### Create cluster
> minikube start --driver=docker

### Create deployment
> kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0

### Expose cluster port
> kubectl expose deployment hello-minikube --type=NodePort --port=8080

### Check deployemts
> kubectl get deployments

### Check services
> kubectl get services hello-minikube

### Port forward and get url
> minikube service hello-minikube

### Cleanup
> minikube delete
