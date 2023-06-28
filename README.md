


Getting started with Amazon ECS using AWS Copilot
=================================================

Get started with Amazon ECS using AWS Copilot by deploying an Amazon ECS application.

Prerequisites
-------------

Before you begin, make sure that you meet the following prerequisites:

*   Set up an AWS account. For more information see [Set up to use Amazon ECS](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/get-set-up-for-amazon-ecs.html).

*   Install the AWS Copilot CLI. Releases currently support Linux and macOS systems. For more information, see [Installing the AWS Copilot CLI](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Copilot.html#copilot-install).

*   Install and configure the AWS CLI. For more information, see [AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).

*   Run `aws configure` to set up a default profile that the AWS Copilot CLI will use to manage your application and services.

*   Install and run Docker. For more information, see [Get started with Docker](https://www.docker.com/get-started).


Deploy your application using one command
-----------------------------------------

Make sure that you have the AWS command line tool installed and have already run `aws configure` before you start.

Deploy the application using the following command.

```
git clone https://github.com/ryota-murakami/express-fargate-hello-world.git demo-app && \
cd demo-app &&                              \
copilot init --app demo                     \
--name api                                  \
--type 'Load Balanced Web Service'`         \
--dockerfile './Dockerfile'                   \
--port 80                                   \
--deploy
```

Deploy your application step by step
------------------------------------

### Step 1: Configure your credentials

Run `aws configure` to set up a default profile that the AWS Copilot CLI uses to manage your application and services.

`` `aws configure` ``

### Step 2: Clone the demo app

Clone a simple Flask application and Dockerfile.

`` `git clone https://github.com/aws-samples/amazon-ecs-cli-sample-app.git demo-app` ``

### Step 3: Set up your application

1.  From within the demo-app directory, run the `init` command.

    For Windows users, run the `init` command from the folder that contains the downloaded `copilot.exe` file.

    `` `copilot init` ``

    AWS Copilot walks you through the setup of your **first application and service** with a series of terminal prompts, starting with **next step**. If you have already used AWS Copilot to deploy applications, you're prompted to choose one from a list of application names.

2.  Name your application.

    `` `**What would you like to name your application? [? for help]**` ``

    **Enter** ``` `` `demo` `` ```.


### Step 4: Set up an ECS Service in your "demo" Application

1.  You're prompted to choose a service type. You're building a simple Flask application that serves a small API.

    `` `**Which service type best represents your service's architecture? [Use arrows to move, type to filter, ? for more help]    > **Load Balanced Web Service**      Backend Service      Scheduled Job**` ``

    **Choose** ``` `` `Load Balanced Web Service` `` ``` .

2.  Provide a name for your service.

    `` `**What do you want to name this Load Balanced Web Service? [? for help]**` ``

    **Enter** ``` `` `api` `` ``` for your service name.

3.  Select a Dockerfile.

    `` `**Which Dockerfile would you like to use for api? [Use arrows to move, type to filter, ? for more help]    > **./Dockerfile**      Use an existing image instead**` ``

    **Choose** ``` `` `Dockerfile` `` ```.

    For Windows users, enter the path to the Dockerfile in the `demo-app` folder `./Dockerfile`.

4.  Define port.

    `` `**Which port do you want customer traffic sent to? [? for help] (80)**` ``

    **Enter** ``` `` `80` `` ``` or accept default.

5.  You will see a log showing the application resources being created.

    `` `Creating the infrastructure to manage services under application demo.` ``

6.  After the application resources are created, deploy a test environment.

    `` `**Would you like to deploy a test environment? [? for help] (y/N)**` ``

    **Enter** ``` `` `y` `` ```.

    `` `Proposing infrastructure changes for the test environment.` ``

7.  You will see a log displaying the status of your application deployment.

8.
```
 Note: It's best to run this command in the root of your Git repository. Welcome to the Copilot CLI! We're going to walk you through some questions to help you get set up with an application on ECS. An application is a collection of containerized services that operate together.  Use existing application: `No` Application name: `demo` Workload type: `Load Balanced Web Service` Service name: `api` Dockerfile: `./Dockerfile` no EXPOSE statements in Dockerfile ./Dockerfile Port: `80` Ok great, we'll set up a `Load Balanced Web Service` named `api` in application `demo` listening on port `80`.  ✔ Created the infrastructure to manage services under application `demo`.  ✔ Wrote the manifest for service `api` at copilot/`api`/manifest.yml Your manifest contains configurations like your container size and port (:80).  ✔ Created ECR repositories for service `api`.  All right, you're all set for local development. Deploy: Yes  ✔ Created the infrastructure for the test environment. - Virtual private cloud on 2 availability zones to hold your services     [Complete] - Virtual private cloud on 2 availability zones to hold your services     [Complete]   - Internet gateway to connect the network to the internet               [Complete]   - Public subnets for internet facing services                           [Complete]   - Private subnets for services that can't be reached from the internet  [Complete]   - Routing tables for services to talk with each other                   [Complete] - ECS Cluster to hold your services                                       [Complete] ✔ Linked account `aws_account_id` and region `region` to application `demo`.  ✔ Created environment test in region `region` under application `demo`.                          Environment test is already on the latest version v1.0.0, skip upgrade. [+] Building 0.8s (7/7) FINISHED  => [internal] load .dockerignore                                                                                  0.1s  => => transferring context: 2B                                                                                    0.0s  => [internal] load build definition from Dockerfile                                                               0.0s  => => transferring dockerfile: 37B                                                                                0.0s  => [internal] load metadata for docker.io/library/nginx:latest                                                    0.7s  => [internal] load build context                                                                                  0.0s  => => transferring context: 32B                                                                                   0.0s  => [1/2] FROM docker.io/library/nginx@sha256:aeade65e99e5d5e7ce162833636f692354c227ff438556e5f3ed0335b7cc2f1b     0.0s  => CACHED [2/2] COPY index.html /usr/share/nginx/html                                                             0.0s  => exporting to image                                                                                             0.0s  => => exporting layers                                                                                            0.0s  => => writing image sha256:3ee02fd4c0f67d7bd808ed7fc73263880649834cbb05d5ca62380f539f4884c4                       0.0s  => => naming to `aws_account_id`.dkr.ecr.`region`.amazonaws.com/`demo`/`api`:cee7709                                      0.0s WARNING! Your password will be stored unencrypted in /home/user/.docker/config.json. Configure a credential helper to remove this warning. See https://docs.docker.com/engine/reference/commandline/login/#credentials-store  Login Succeeded The push refers to repository [`aws_account_id`.dkr.ecr.`region`.amazonaws.com/`demo`/`api`] 592a5c0c47f1: Pushed 6c7de695ede3: Pushed 2f4accd375d9: Pushed ffc9b21953f4: Pushed cee7709: digest: sha_digest  ✔ Deployed api, you can access it at http://demo-Publi-1OQ8VMS2VC2WG-561733989.`region`.elb.amazonaws.com.
```


### Step 5: Verify your application is running

View the status of your application by using the following commands.

List all of your AWS Copilot applications.

`` `copilot app ls` ``

Show information about the environments and services in your application.

`` `copilot app show` ``

Show information about your environments.

`` `copilot env ls` ``

Show information about the service, including endpoints, capacity and related resources.

`` `copilot svc show` ``

List of all the services in an application.

`` `copilot svc ls` ``

Show logs of a deployed service.

`` `copilot svc logs` ``

Show service status.

`` `copilot svc status` ``

List available commands and options.

`` `copilot --help` ``

`` `copilot init --help` ``

### Step 6. Learn to create a CI/CD Pipeline

Instructions can be found in the [ECS Workshop](https://ecsworkshop.com/microservices/frontend/#create-a-ci-cd-pipeline) detailing how to fully automate a CI/CD pipeline and git workflow using AWS Copilot.

### Step 7: Clean up

Run the following command to delete and clean up all resources.

`` `copilot app delete` ``