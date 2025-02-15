# Deploy Backend with Kubernetes

**Author:** Caelan Dever  
**Email:** caelanwd@gmail.com

---

## Deploy Backend with Kubernetes

<img width="595" alt="5i" src="https://github.com/user-attachments/assets/b88c77d9-9ce8-415d-9d89-a3de9d1d1983" />

---

## Introducing Today's Project!

In this project, I will set up manifest files and deploy that backend with Kubernetes!

### Tools and concepts

I used Kubernetes, ECR, kubectl, and EC2 to build and push a container image of the backend of an app. Key concepts include using manifests that tell Kubernetes how you'd like to deploy the backend.

### Project reflection

This project took me approximately 55 minutes. The most challenging part was applying the manifests with the right permissions. My favourite part was setting up the dockerfile. 

## What I'm deploying

To set up today's project, I launched a Kubernetes cluster. Steps I took to do this included installing eksctl, setting up IAM roles for the EC2 instance, and using the command eksctl to create a kubernetes cluster. 

### I'm deploying an app's backend

Next, I retrieved the backend that I plan to deploy. An app's backend means the "brain" of an application. It's where your app processes user requests and stores and retrieves data. I retrieved backend code by cloning the nextwork-flask-backend repo.

<img width="678" alt="3f" src="https://github.com/user-attachments/assets/2672d7b4-fa0d-45a3-961e-0d98cc9cd523" />


---

## Building a container image

Once I cloned the backend code, my next step is to build a container image of the backend. This is because when your team member prepared the app's backend, they wrote a file called a Dockerfile and stored it inside the GitHub repository.

When I tried to build a Docker image of the backend, I ran into a permissions error because c2-user, which is the user you've used to access this instance, doesn't have permission to run Docker commands. 

To solve the permissions error, I added ec2-user to the Docker group. The Docker group is a group in Linux systems that gives users the permission to run Docker commands. By default, only the root user can run Docker commands. 

<img width="945" alt="2d" src="https://github.com/user-attachments/assets/81bb32d3-41c4-48bc-8469-a53025021e4d" />

---

## Container Registry

I'm using Amazon ECR in this project to securely store, share, and deploy container images. ECR is a good choice for the job because t's an AWS service, which lets EKS deploy your container image with authentication setup.



Container registries like Amazon ECR are great for Kubernetes deployment because it is a great way to deploy containerized apps. Your cluster can pull whatever is the latest image in your repository on demand, which makes deployments stay consistent.


<img width="960" alt="4f" src="https://github.com/user-attachments/assets/0240b17f-10cd-4d91-8e7d-63ca0d1e591a" />


https://github.com/user-attachments/assets/c9380d6f-5772-4fc0-ad32-79deb3eb86ca


---

## EXTRA: Backend Explained

After reviewing the app's backend code, I've learnt that the app's backend fetches data based on a search topic you enter, The backend code uses Flask to connect with an external API, and process the data, the backend then sends the data back as JSON

### Unpacking three key backend files

The requirements.txt file lists the dependencies your app needs.

The Dockerfile gives Docker instructions on how a Docker image of the backend should be built. Key commands in this Dockerfile include RUN pip3 install -r requirements.txt installs the dependencies in requirements.txt.

The app.py file contains;  Setting up the app and routing: The code starts by importing the Flask framework and tools for creating an API, Fetching data, and Sending the response: The collected data is turned into a formatted JSON response.

## Manifest files

Kubernetes manifests are a set of instructions that tells Kubernetes how to run your app. Manifests are helpful because Kubernetes uses this information to know what your app needs, like which containers to run, how many copies to create.


A Deployment manifest manages details like the number of copies of your code that Kubernetes should run across your cluster, and which settings to apply. The container image URL in my Deployment manifest tells Kubernetes how to set up each container.

A Service resource exposes your application i.e. making it accessible to network traffic. My Service manifest sets up a service resource in Kubernetes to make nextwork-flask-backend accessible from outside the cluster.

<img width="895" alt="3c" src="https://github.com/user-attachments/assets/41978301-1ef3-41d1-a1ea-86ef3fa1782f" />

---

## Backend Deployment!

To deploy my backend application, I installed kubectl and applied the manifest files. 

### kubectl

kubectl is the command-line tool for interacting with Kubernetes resourcesI need this tool to apply our manifests and deploy our application. I can't use eksctl for the job because it is for setting up and deleting your EKS cluster and configuring it

<img width="595" alt="5i" src="https://github.com/user-attachments/assets/f80ddab3-f767-4fd9-9876-90a2374aa819" />


---

## Verifying Deployment

My extension for this project is to use the EKS console to view my EKS cluster in the console. I had to set up IAM access policies because AWS permissions alone don’t automatically carry over to Kubernetes I set up access by running an IAM command. 

Once I gained access into my cluster's nodes, I discovered pods running inside each node. Pods are Containers the smallest things you can deploy. Containers in a pod share the same network space & storage so they can communicate and share data better

The EKS console shows you the events for each pod, where I could see the steps that happened when Kubernetes was creating your pod. This validated that the backend is up and working and can be accessed within the cluster's network.

<img width="941" alt="3v" src="https://github.com/user-attachments/assets/d6ac5124-9719-4d0e-9ee6-d230e51f334f" />


https://github.com/user-attachments/assets/c93375db-b06f-4224-b145-03f1926caaeb




---

---

