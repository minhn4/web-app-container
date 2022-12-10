# Kubernetes Engine Instruction

**_I. Cloud Shell commands for Docker images_**

+++++++++++++**_1. Enable and authenticate Container Registry to store Docker images_**+++++++++++++

gcloud services enable containerregistry.googleapis.com

gcloud auth configure-docker

++++++++++++++++++++**_2. Clone the source code and build a Docker image_**++++++++++++++++++

git clone https://github.com/quickhair/web-app-container.git

docker build -t gcr.io/minh-sandbox/web-app-container .

(gcr.io is one of the hostnames, 'minh-sandbox' is the project ID, see https://cloud.google.com/container-registry/docs/overview for more details.)

+++++++++++++++++**_3. Push the Docker image to Container Registry_**+++++++++++++++++

docker push gcr.io/minh-sandbox/web-app-container

----------------------------------------------------------------------------------------------------

**_II. Google Cloud Console: Kubernetes Engine tutorial_**

++++++++++++++++++++++++**_1. Create a Kubernetes cluster_**++++++++++++++++++++++++++++++++++++++++

In GC console left menu, go to Kubernetes Engine tab -> Clusters and enable it if you haven't done that.

Next up, hit Create -> Configure (Standard) -> name your Kubernetes cluster (e.g., production-cluster), choose a zone near you (optional: choose node locations if you want to), choose Static for Control plane version for now -> Create. Wait until the cluster is available.

+++++++++++++++++++++**_2. Deploy a Docker image stored in Container Registry_**++++++++++++++++++++++++

To deploy a Docker image as an app container, hit Workloads tab in the left menu -> Deploy. Next up, choose 'Existing container image' -> Select and then select one of the images stored in the Container Registry -> Continue. Finally, name your app (e.g., demo-web-app), choose the cluster you want to deploy -> Deploy.

Now, if you want to access this app from outside, you need to expose it to external traffic. Click Expose on the top-right corner.
