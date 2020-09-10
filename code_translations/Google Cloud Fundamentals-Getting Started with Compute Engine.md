# **Objectives**

In this lab, you will learn how to perform the following tasks:

- Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

- Create a Compute Engine virtual machine using the gcloud command-line interface.

- Connect between the two instances.

## _**Task 1: Sign in to the Google Cloud Platform (GCP) Console**_

Set lab environment and proceed to task 2

## _**Task 2: Create a virtual machine using the GCP Console**_

Step 1

Create a Virtual Machine called **my-vm-1** with the Google Cloud platform Console

    gcloud compute instances create "my-vm-1" \
    --machine-type "n1-standard-1" \
    --image-project "debian-cloud" \
    --image "debian-9-stretch-v20190213" \
    --subnet "default"

## _**Task 3: Create a virtual machine using the gcloud command line**_

Step 2

Compute a VM called **my-vm-2** using the gcloud CLI run the following command:

    gcloud compute instances create "my-vm-2" \
    --machine-type "n1-standard-1" \
    --image-project "debian-cloud" \
    --image "debian-9-stretch-v20190213" \
    --subnet "default"

## _**Task 4: Connect between VM instances**_

Step 3

Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network

    ping my-vm-1

Step 4

At the command prompt on my-vm-1, install the Nginx web server:

    sudo apt-get install nginx-light -y

Step 5

Use the nano text editor to add a custom message to the home page of the web server:

    sudo nano /var/www/html/index.nginx-debian.html

Step 6

Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:

    Hi from YOUR_NAME

Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.

Step 7

Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:

    curl http://localhost/

To exit the command prompt on my-vm-1, execute this command:

    exit

Step 8

To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:

    curl http://my-vm-1/


# **End lab**