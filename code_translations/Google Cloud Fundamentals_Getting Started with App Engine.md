# **Objectives**

In this, you learn how to perform the following tasks:

- Initialize App Engine.
- Preview an App Engine application running locally in Cloud Shell.
- Deploy an App Engine application, so that others can reach it.

- Disable an App Engine application, when you no longer want it to be visible.

After you set up your lab environment **_Activate Googgle Cloud Shell_**

In Cloud Shell, list the active account name with this command:

    gcloud auth list

List the project ID with this command:

    gcloud config list project

## _**Task 1: Initialize App Engine**_

Step 1

Initialize your App Engine app with your project and choose its region:

    gcloud app create --project=$DEVSHELL_PROJECT_ID

step 2

Clone the source code repository for a sample application in the hello_world directory:

    git clone https://github.com/GoogleCloudPlatform/python-docs-samples

Step 3

Navigate to the source directory:

    cd python-docs-samples/appengine/standard_python3/hello_world

## _**Task 2: Run Hello World application locally**_

In the Cloud Shell

Step 1

Execute the following command to download and update the packages list

    sudo apt-get update

Step 2

Set up a virtual environment in which you will run your application.

    sudo apt-get install virtualenv

If prompted [Y/n], press **_y_** and then hit _**Enter**_

    virtualenv -p python3 venv

Step 3

Activate the virtual environment.

    source venv/bin/activate

Step 4

Navigate to your project directory and install dependencies.

    pip install  -r requirements.txt

Step 5

Run the application:

    python main.py

Ignore any warning if any

Step 6

In **Cloud Shell**, click Web preview **(Web Preview)** > **Preview on port 8080** to preview the application.

To end the test, in the Cloud Shell press **_ctrl+C_** to abort the deployed services.


## **_Task 3: Deploy and run Hello World on App Engine_**

To deploy your application to the App Engine Standard environment:

Step 1

Navigate to the source directory:

    cd ~/python-docs-samples/appengine/standard_python3/hello_world

Step 2

Deploy your Hello World application.

    gcloud app deploy

If prompted "Do you want to continue (Y/n)?", press **_Y_** and then **_Enter_**.

Step 3

Launch your browser to view the app at http://YOUR_PROJECT_ID.appspot.com

    gcloud app browse

Copy and paste the URL into a new browser window.

## **_Task 4: Disable the application_**

Run the following command to disable the app

 gcloud app versions stop --service=servicename