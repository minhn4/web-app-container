# Kubernetes Engine Instruction

**_I. Cloud Shell commands for Docker images_**

+++++++++++++**_1. Enable and authenticate Container Registry to store Docker images_**+++++++++++++

gcloud services enable containerregistry.googleapis.com

gcloud auth configure-docker

++++++++++++++++++++**_2. Clone and build the Docker image_**+++++++++++++++++++

git clone https://github.com/quickhair/web-app-container.git

docker build -t gcr.io/minh-sandbox/web-app-container .

(gcr.io is one of the hostnames, 'minh-sandbox' is the project ID, see https://cloud.google.com/container-registry/docs/overview for more details.)

+++++++++++++++++**_3. Push the Docker image to Container Registry_**+++++++++++++++++

docker push gcr.io/minh-sandbox/web-app-container

----------------------------------------------------------------------------------------------------

**_II. Console UI: Kubernetes Engine tutorial_**
