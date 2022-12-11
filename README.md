# Kubernetes Engine Instruction

## **I. Cloud Shell commands**

### **_1. Enable and authenticate Container Registry to store Docker images_**

Open `Cloud Shell` (top-right corner), then type:

`gcloud services enable containerregistry.googleapis.com`

`gcloud auth configure-docker`

### **_2. Clone the source code and build a Docker image_**

`git clone https://github.com/quickhair/web-app-container.git`

`cd web-app-container`

`docker build -t gcr.io/minh-sandbox/web-app-container .`

Hit Authorize and login to your Google Cloud account if prompted. Explanation: `gcr.io` is one of the hostnames, `minh-sandbox` is the project ID, see https://cloud.google.com/container-registry/docs/overview for more details.

You can check and delete your Docker images with:

`docker images`

`docker rmi gcr.io/minh-sandbox/web-app-container`

### **_3. Push the Docker image to Container Registry_**

`docker push gcr.io/minh-sandbox/web-app-container`

You can search for `Container Registry` section in the console search bar and you'll see the 'web-app-container' repository you've just pushed. Go inside the repository, you'll see your Docker images; you can delete them here if you want to.

----------------------------------------------------------------------------------------------------

## **II. Google Cloud Console: Kubernetes Engine tutorial**

### **_1. Create a Kubernetes cluster_**

In the console left menu, go to `Compute Engine` and `Kubernetes Engine` sections and enable them if you haven't done so.

Next up, go to `Clusters` tab in the `Kubernetes Engine` section left menu -> hit `Create` -> `Configure (Standard)` -> name your Kubernetes cluster (e.g., production-cluster), choose a zone near you (optional: choose node locations if you want to), choose `Static` for `Control plane version` for now -> `Create`. Wait until the cluster is available.

By default, Kubernetes Engine will create a node pool of three VMs initially (you can create more node pool if needed). To view all the node pools and their corresponding nodes (VMs), in `Clusters` tab, click on the name of the cluster you want to view -> `Nodes` tab. You can also view these VMs in `Compute Engine` section.

### **_2. Deploy an app_**

To deploy a Docker image as an app container, hit `Workloads` tab in the left menu -> `Deploy`. Next up, choose `Existing container image` -> `Select` and then select one of the Docker images stored in the Container Registry -> `Continue`. Finally, name your app (e.g., demo-web-app), choose the cluster you want to deploy (e.g., production-cluster) -> `Deploy`.

Kubernetes Engine will deploy the app in all nodes in the node pool.

### **_3. Expose the app_**

Now, if you want to access this app from outside, you need to expose it to external traffic -> click `Expose` in the top-right corner. Next, you can change the external port if needed; otherwise, leave it 80 -> choose `Load balancer` for `Service type` and name your service -> `Expose`.

GCP will automatically assign an external IP to this app and you can use that IP address to access the app from outside (e.g., from a browser); the load balancer will distribute the load equally to all the VMs in the node pool. You can view all your app services in the `Services & Ingress` tab.

Now, you can click on the IP address at `External endpoints` line to redirect to your app in your browser.
