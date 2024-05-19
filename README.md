# Habit Tracker Application Deployment

This repository contains Kubernetes manifests for deploying a habit tracker application. The application consists of a client, server, and MongoDB database, and uses Ingress to route traffic.

## Overview

The habit tracker application is a web-based tool to help users keep track of their habits. It comprises three main components:

1. **Client**: The front-end of the application, built using a web framework.
2. **Server**: The back-end of the application, which handles business logic and interacts with the database.
3. **MongoDB**: The database used to store habit data.

## Project Structure

- **client-depl.yaml**: Deployment and Service configuration for the client application.
- **server-depl.yaml**: Deployment and Service configuration for the server application.
- **mongo-depl.yaml**: Deployment and Service configuration for the MongoDB database.
- **mongo-pvc.yaml**: PersistentVolumeClaim configuration for MongoDB storage.
- **mongo-secret.yaml**: Secret configuration for storing MongoDB connection URL.
- **ingress-srv.yaml**: Ingress configuration for routing external traffic to the client and server services.

## How It Works

1. **MongoDB Deployment**: The MongoDB database is deployed with a PersistentVolumeClaim to ensure data persistence.
2. **Server Deployment**: The server application is deployed and configured to use the MongoDB connection URL from a Kubernetes Secret.
3. **Client Deployment**: The client application is deployed to handle user interactions.
4. **Ingress Configuration**: An Ingress resource is set up to route traffic to the client and server applications based on the specified paths.

## Deployment Steps

1. **Deploy MongoDB**:

   ```sh
   kubectl apply -f mongo-pvc.yaml
   kubectl apply -f mongo-secret.yaml
   kubectl apply -f mongo-depl.yaml

2. **Deploy Server**:

   ```sh
   kubectl apply -f server-depl.yaml

3. **Deploy Client**:

   ```sh
   kubectl apply -f client-depl.yaml

4. **Deploy Ingress**:

   ```sh
   kubectl apply -f ingress-srv.yaml

## Simulating Real World Use Case

To simulate a real-world use case, you can set up your domain in the /etc/hosts file on your local machine. This allows you to access the application using a domain name as you would in a production environment.

1. **Get the Minikube IP address**:

   ```sh
   minikube ip

2. **Open the `/etc/hosts` file with vim:**:

   ```sh
   sudo vim /etc/hosts

3. **Add the following line to map the domain to your Minikube IP address (replace `MINIKUBE_IP` with the IP obtained from the previous step)::**:

   ```sh
   MINIKUBE_IP habittracker.com

4. **Save and close the file.**

Now, you can access the habit tracker application by navigating to `http://habittracker.com` in your web browser.

## Notes

- Ensure your Kubernetes cluster has an Ingress controller installed (e.g., NGINX Ingress Controller).
- Update the image versions and resource requests/limits as needed for your environment.
- The MongoDB connection URL in `mongo-secret.yaml` should match the service name and database name used in your application.

By following these steps, you can deploy the habit tracker application in a Kubernetes cluster and simulate a real-world environment using domain name mapping.