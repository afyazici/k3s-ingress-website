# K3s Ingress WebSite

## Project Overview

This project involves deploying a Dockerized Nginx website using K3s, a lightweight Kubernetes distribution. The deployment will be managed via Kubernetes and will be accessible through a custom domain. The steps include setting up K3s, deploying the Nginx Ingress Controller, creating a Load Balancer, and finally deploying and exposing the Nginx website.
Prerequisites

* Domain name for accessing the website
* Basic knowledge of Kubernetes and Docker

## Setup Instructions

1. Install K3s

First, install K3s on your server. This lightweight Kubernetes distribution will serve as the foundation for your deployment.
By default, K3S cluster will use Traefik as “Ingress” and “Proxy”. If you want to install your K3S cluster without Traefik, you must pass a parameter before the cluster installation time.

```bash
export INSTALL_K3S_EXEC="server --no-deploy traefik"
curl -sfL https://get.k3s.io | sh -
sudo k3s kubectl get node
```

2. Deploy Nginx Ingress Controller

Next, deploy the Nginx Ingress Controller to handle incoming HTTP and HTTPS traffic.

```bash
sudo kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.7.1/deploy/static/provider/baremetal/deploy.yaml
```

3. Create a Load Balancer

Apply the Load Balancer configuration:

```bash
sudo kubectl apply -f loadbalancer.yaml
```

4. Deploy the Nginx Website

>[!NOTE]
>Replace DockerHub image and domain.com with your domain and image in `deployment.yaml`.

Apply the deployment configuration:

```bash
sudo kubectl apply -f deployment.yaml
```
## Accessing the Website

Once the deployment is complete, you should be able to access your Dockerized Nginx website through the domain name you specified.

## Troubleshooting

Ensure your domain name is correctly pointed to the K3s instance node.
Check the status of your Kubernetes resources using `kubectl get all -n ingress-nginx` and `kubectl get all`.
