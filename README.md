# web-app-container
**_Cloud Shell_**

+++++++++++**_Enable and authenticate Contaner Registry to store Docker images_**+++++++++++

gcloud services enable containerregistry.googleapis.com

gcloud auth configure-docker

**_Clone and build Docker image_**

git clone https://github.com/quickhair/web-app-container.git

docker build -t gcr.io/minh-sandbox/web-app-container .

(gcr.io is one of the hostname (https://cloud.google.com/container-registry/docs/overview), 'minh-sandbox' is the project ID)

**_Push the DOcker image to Container Registry_**

docker push gcr.io/minh-sandbox/web-app-container
