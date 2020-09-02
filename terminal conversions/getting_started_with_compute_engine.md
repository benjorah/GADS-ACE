# LAB: Google Cloud Fundamentals: Getting Started with Compute Engine 

## Objectives:

In this lab, you will learn how to perform he following tasks:
 - Create a compute engine virtual machine using Google Colud Platform (GCP) console.
 - Create a compute engine virtual machine using the gcloud command-line interface.
 - Connect between the two instances

## Steps
1. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) console.

    ` gcloud compute instances create my-vm-1 -machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default" --tags http-access`

    ` gcloud compute firewall-rules create allow-http --action=ALLOW --destination=INGRESS --rules=http:80 --target-tags=http-access`

2.  Create a compute engine virtual machine using the gcloud command-line interface.

    ` gcloud compute set compute/zone us-central1-b`

    ` gcloud compute instances create my-vm-2 -machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"`

3. Connect between the two instances

    1. Use the ping command to confirm my-vm-2 can reach my-vm-1 over the network
        - Connect to my-vm-2:
        `gcloud compute ssh my-vm-2`

        - Ping my-vm-1 form my-vm-2:
        `ping -c 6 my-vm-1`

        - Use the ssh command to open command prompt on my-vm-1 from my-vm2:
        `ssh my-vm-1`

        - At the command prompt of my-vm-1, install the Nginx web server:
        `sudo apt-get install nginx-light -y`

        - Use the nano text editor to add a custom message to the home page of the web server: 
        `sudo nano /var/www/html/index.nginx-debian.html`

        - Use the arrow key to move the cursor to the line just below he h1 header. Add text like this nd replace YOUR_NAME with your name

        `Hi Okey`

        - Exit the text editor and confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
        `curl http://localhost/`
            - *Result*: The html source of the web server's homepage including custom message

        - To confirm that my-vm-2 can can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
        `curl http://my-vm-1/`
            - *Result*: The html source of the web server's homepage again including custom message

    2. Now get the external IP of myu-vm-1 instance with this command:

        `gcloud compute instances list --zone us-central1-a`
    
    3. Paste the copied IP address of my-vm-1 into a browser tab and hit enter

        - You will see your web server's homepage with your custom message
            - *Result*: The html source of the web server's homepage again including custom message