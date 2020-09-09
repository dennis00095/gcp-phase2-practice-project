# **Objectives**

This lab helps you learn the following:

  -  Define, deploy  and clean up a GKE job
  - Define, deploy and clean up a GKE Cronjob

## **_Activate Google Cloud Shell_**

 In GCP console, on the top right toolbar, click the Open Cloud Shell button and click **Continue** when prompted.

List active account name by the following command:

    gcloud auth list

List the project ID with this command:

    gcloud config list project

## _**Task 1. Define and deploy a Job manifest**_

- ### **Create a Google Kubernetes Engine cluster**

Step 1

In Cloud Shell, type the following command to set the environment variable for the zone and cluster name.

    export my_zone=us-central1-a
    export my_cluster=standard-cluster-1

Step 2

Configure kubectl tab completion in Cloud Shell.

    source <(kubectl completion bash)


Step 3

In Cloud Shell, type the following command to create a Kubernetes cluster.

    gcloud container clusters create $my_cluster --num-nodes 3  --enable-ip-alias --zone $my_zone

Step 4

In Cloud Shell, configure access to your cluster for the kubectl command-line tool, using the following command:

    gcloud container clusters get-credentials $my_cluster --zone $my_zone

Step 5

In Cloud Shell enter the following command to clone the repository to the lab Cloud Shell

    git clone https://github.com/GoogleCloudPlatformTraining/training-data-analyst

Step 6

Change to the directory that contains the sample files for this lab.

    cd ~/training-data-analyst/courses/ak8s/07_Jobs_CronJobs

- ### **Create and run a Job**

You will create a job using a sample deployment manifest called example-job.yaml that has been provided for you.

    apiVersion: batch/v1
    kind: Job
    metadata:
       # Unique key of the Job instance
       name: example-job
    spec:
        template:
            metadata:
                name: exaple-job
            spec:
                containers:
                - name: pi
                image: perl
                command: ["perl"]
                args: ["-Mbignum=bpi", "-wle", "print bpi(2000)"]
            # Do not restart containers after they exit
            restartPolicy: Never

Step 1

To create a Job from this file, execute the following command:

    kubectl apply -f example-job.yaml

Step 2

To check the status of this Job, execute the following command:

    kubectl describe job example-job

Step 3

To view all Pod resources in your cluster, including Pods created by the Job which have completed, execute the following command:

    kubectl get pods

- ### **Clean up and delete the Job**

Step 1

To get a list of the Jobs in the cluster, execute the following command:

    kubectl get jobs

Step 2

o retrieve the log file from the Pod that ran the Job execute the following command. You must replace [POD-NAME] with the node name you recorded in the last task

    kubectl logs [POD-NAME]

Step 3

To delete the Job, execute the following command:

    kubectl delete job example-job

## _**Task 2. Define and deploy a CronJob manifest**_

- ### **Create and run a CronJob**

The CronJob manifest file example-cronjob.yaml has been provided for you. This CronJob deploys a new container every minute that prints the time, date and "Hello, World!".

    apiVersion: batch/v1beta1
    kind: CronJob
    metadata:
        name: hello
    spec:
        schedule: "*/1 * * * *"
        jobTemplate:
            spec:
                template:
                    spec:
                        containers:
                        - name: hello
                            image: busybox
                            args:
                            - /bin/sh
                            - -c
                            - date; echo "Hello, World!"
                        restartPolicy: OnFailure

Step 1

To create a Job from this file, execute the following command:

    kubectl apply -f example-cronjob.yaml

Step 2

To get a list of the Jobs in the cluster, execute the following command:

    kubectl get jobs

Step 3

To check the status of this Job, execute the following command, where [job_name] is the name of your job:

    kubectl describe job [job_name]

Step 4

View the output of the Job by querying the logs for the Pod. Replace [POD-NAME] with the name of the Pod you recorded in the last step.

    kubectl logs [POD-NAME]

Step 5

To view all job resources in your cluster, including all of the Pods created by the CronJob which have completed, execute the following command:

    kubectl get jobs

- ### **Clean up and delete the Job**

In order to stop the CronJob and clean up the Jobs associated with it you must delete the CronJob.

Step 1

To delete all these jobs, execute the following command:

    kubectl delete cronjob hello

Step 2

To verify that the jobs were deleted, execute the following command:

    kubectl get jobs


# **End Your Lab**
