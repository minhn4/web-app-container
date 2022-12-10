# Kubernetes Engine Instruction

## **I. Cloud Shell commands for Docker images**

### **_1. Enable and authenticate Container Registry to store Docker images_**

Open `Cloud Shell` (top-right corner), then type:

`gcloud services enable containerregistry.googleapis.com`

`gcloud auth configure-docker`

++++++++++++++++++++**_2. Clone the source code and build a Docker image_**++++++++++++++++++

`git clone https://github.com/quickhair/web-app-container.git`

`docker build -t gcr.io/minh-sandbox/web-app-container .`

Hit Authorize and login to your Google Cloud account if prompted. Explanation: gcr.io is one of the hostnames, 'minh-sandbox' is the project ID, see https://cloud.google.com/container-registry/docs/overview for more details.

You can check and delete your Docker images with:

`docker images`

`docker rmi gcr.io/minh-sandbox/web-app-container`

+++++++++++++++++**_3. Push the Docker image to Container Registry_**+++++++++++++++++

`docker push gcr.io/minh-sandbox/web-app-container`

You can search for Container Registry in the Google Cloud console and you'll see the 'web-app-container' repository you've just pushed. Go inside the repository, you'll see your Docker image(s); you can delete them here if you want to.

----------------------------------------------------------------------------------------------------

## **_II. Google Cloud Console: Kubernetes Engine tutorial_**

+++++++++++++++++++++**_1. Create a Kubernetes cluster_**+++++++++++++++++++++++++++++++++

In GC console left menu, go to Kubernetes Engine tab -> Clusters and enable it if you haven't done that.

Next up, hit Create -> Configure (Standard) -> name your Kubernetes cluster (e.g., production-cluster), choose a zone near you (optional: choose node locations if you want to), choose Static for Control plane version for now -> Create. Wait until the cluster is available.

+++++++++++++++++**_2. Deploy a Docker image stored in Container Registry_**++++++++++++++++++

To deploy a Docker image as an app container, hit Workloads tab in the left menu -> Deploy. Next up, choose 'Existing container image' -> Select and then select one of the images stored in the Container Registry -> Continue. Finally, name your app (e.g., demo-web-app), choose the cluster you want to deploy -> Deploy.

+++++++++++++++++++++++**_3. Expose the app_**+++++++++++++++++++++++++++

Now, if you want to access this app from outside, you need to expose it to external traffic -> click Expose on the top-right corner. Next, you can change the external port if you want to, otherwise, leave it 80 -> choose Load balancer for Service type and name your service -> hit Expose. GCP will assign an external IP to this app and you can use that IP address to access the app (e.g., from a browser).
