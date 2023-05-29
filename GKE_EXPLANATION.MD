# YOLO Application Deployment with K8s on GKE

This document explains the steps I followed to deploy the app in GKE.
Here's a [link](http://34.67.92.131:3000/) to the app.

## 1. Manifest folder

Created a folder for the manifest files (deployment, services and statefulsets files)
Here's a [link](/manifests/) to the manifests folder

### Deployment files

These folder contains manifest files for deploying client and backend services
Each of the services has one replica
Here's a [link](/manifests/deployments/) to the folder

### Service files

Created three load balancing service files for each service expose them to the internet
Here's a [link](/manifests/services/) to the folder.

### Statefulsets

Implemented stateful sets for the mongodb deployment to ensure persistence of data.
I first created a persistent volume claim file that would provision a volume for the stateful set when created.
Here's a [link](/manifests/statefulsets/) to the folder.

After creating the files in this folder, I used the cloud shell to provision a cluster and perform the deployent in the following steps:

1.  Create cluster:
    ```
    gcloud container clusters create-auto yolo-cluster --location=us-central1
    ```
2.  Clone my repository:
    I first linked my github repo to the GCP source repositories service.
    A replica of the repo named github_dedan-wamalwa_yolo was created in my source repositories service.
    Clone:

    ```
    gcloud source repos clone github_dedan-wamalwa_yolo
    ```

3.  Change and directory and apply the files:
    Change directory to the repository and apply the manifests files to deploy and create services
    Create deployments:

    ```
    kubectl apply -f file_name.yaml
    ```

    Get deployments:

    ```
    kubectl get deployments
    ```

    Create services:

    ```
    kubectl apply -f file_name.yaml
    ```

    Get services:

    ```
    kubectl get services
    ```

Then I got the IP from the External_IP column for the client service.