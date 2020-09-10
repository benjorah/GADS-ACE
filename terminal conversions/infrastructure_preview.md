# LAB:  Essential Google Cloud Infrastructure: Foundation -> infrastructure Overview

## Objectives:

In this lab, you will learn how to perform he following tasks:
 - Use Marketplace to build a Jenkins Continuous Integration environment.
 - Verify that you can manage the service from the Jenkins UI.
 - Administer the service from the Virtual Machine host through SSH.

## Steps
1. Use Marketplace to build a deployment
    ` JENKINS_IMAGE=$(gcloud compute images list --project=bitnami-launchpad | awk '$1~/jenkins/{print $1}' ) ZONE=us-west4-a   MACHINE_TYPE=g1-small`

    `gcloud compute instances create ${VM_NAME} --image-project bitnami-launchpad --image $JENKINS_IMAGE --zone $ZONE --machine-type $MACHINE_TYPE --metadata bitnami-base-password=JenkinsFoundersChair,bitnami-default-user=user,bitnami-key=jenkins,bitnami-name=Jenkins,bitnami-url=//bitnami.com/stack/jenkins,bitnami-description=Jenkins.,startup-script-url=https://dl.google.com/dl/jenkins/p2dsetup/setup-script.sh --tags https-server,bitnami-launchpad`

2.  Examine the deployment

    - Get the IP address of the machine running Jenkins
    `gcloud compute instances list --filter="zone:( us-west4-a )"`

    - Visit the site on http://[ip of the jenkins machine]
        - *Result*: The html source of the jenkins login page should be visible (might need to reload a couple of times) 
    
    - Login with the credentials used in the deployment
        - *Result*: The html source of the jenkins homepage would be visible

3. Administer the service

    - SSH into the jenkins machine
    `gcloud compute ssh [jenkins ip]`

    - Stop the jenkins service:
    `sudo /opt/bitnami/ctlscript.sh stop`

    - Navigate to the jenkins homepage
        - *Result*: The html source of the jenkins homepage would be unavailable

     - Restart the jenkins service:
    `sudo /opt/bitnami/ctlscript.sh restart`

    - Navigate to the jenkins homepage
        - *Result*: The html source of the jenkins homepage would be available again

