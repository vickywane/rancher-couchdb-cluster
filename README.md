# rancher-couchdb-cluster
Repository containing the related files for my article published on Rancher on setting up a containerized distributed database cluster using Rancher.

## Creating a **Service Account** on the Google Cloud Platfrom.



## Creating a **Service Account Key** on the Google Cloud Platfrom.

To create a Service Account and launch the Cloud Shell, we would perform all needed operation using related commands from the Cloud Shell.

Run the following command from your local terminal if you have the gcloud SDK installed or use the Cloud Shell on the Google Cloud.


    gcloud iam service-accounts create couchdb-rancher --description="For CloudDB GKE deployment" --display-name="couchdb-rancher" 

Update the service account IAM roles using the command below replacing the `PROJECT_ID` placeholder with your `PROJECT_ID` ;


    gcloud projects add-iam-policy-binding PROJECT_ID --member="serviceAccount:couchdb-rancher@PROJECT_ID.iam.gserviceaccount.com" --role="roles/compute.viewer" --role="roles/viewer" --role="roles/container.admin" --role="roles/iam.serviceAccountUser" --condition=None

From the command above, we added the Service Account User, Kubernetes Engine Admin , Viewer and Compute Viewer roles to the created service account to grant Rancher access to those resources.

Last step is to download a service account key attached to the created service account. The command below creates the service account key and in JSON format.


    gcloud iam service-accounts keys create ~/key.json --iam-account couchdb-rancher@project-id.iam.gserviceaccount.com

Your service account key has been created. Type `cat key.json` to reveal and copy the contents to the Service Account input field in the Rancher cluster creation page. 
