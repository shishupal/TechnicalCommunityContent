# Demo 1.3: Running a MEAN app in a Docker and CosmosDB on Azure

This demo should take about 12 minutes.

## Objectives

The goal is to show how to run a MEAN app in docker container and extend the MongoDB to CosmoDB.

## Requirements


- Internet connection is required in order to access the Azure portal.

- An active Azure subscription (you can use the one created in previous Demo 1.2).

- Visual Studio Code. You can download from <https://code.visualstudio.com/>

- MongoDB. You can download from <https://www.mongodb.com/download-center#community>

- DockerHub account. Create one at <https://hub.docker.com/>
## Setup

Make sure to perform the following setup procedures before presenting the demo. The setup takes some time and you do not want to make the audience wait for the tasks to complete.


### Cloning the demo code from the github repository

1. Open Visual Studio code and click on Clone Git repository(1). For the demo we will be using the a Node To Do app built with MongoDB and AngularJS. The code can be cloned form GitHub from <https://github.com/scotch-io/node-todo.git> Paste this url into the Repository URL (2).

> <img src="./media/image1.png" width="624" height="327" />

We will now select the directory for us to store the code. In our demo we used C:\Users\hissi\meandemoapp(1).VS Code will ask whether you would like to Open the repository now. Go ahead and click Open Repository(2).
cli
> <img src="./media/image2.png" width="624" height="327" />
> <img src="./media/image3.png" width="624" height="327" />

Next, we want to make sure all we have our dependencies installed using NodeJS package manager npm. Enter CTRL+~ to open the PowerShell terminal. From here, type in the command "npm install" and wait for it to complete.

> <img src="./media/image4.png" width="624" height="327" />

### Installing Docker extension for Visual Studio Code

Click on the extensions icon from the left menu(1). Search for Docker and click install(2).

> <img src="./media/image12.png" width="624" height="327" />


### Running MongoDB locally

Run command prompt as administrator and type the following commands: 

cd C:\Program Files\MongoDB\Server\3.4\bin\
mongod.exe

> <img src="./media/image8.png" width="624" height="327" />

Minimize this window and keep it running for the demo.


### Demo Steps

### 

During the demo, the goal is to demonstrate how to deploy a local MEAN (MongoDB, ExpressJS, AngularJS, NodeJS) app onto Azure using Docker containers and extending the MongoDB to CosmosDB. The main reason to set it up like this is to ensure your app has the scaling capabilities to support super high traffic.

You will start the demo with Visual Studio Code with the git repository already cloned. Let the audience know that you cloned the repository and installed the dependencies with npm install before the presentation. Now open the server.js file(1). Next, highlight configuration for the MongoDB server(2). Note that it is currently configured for a local database.

> <img src="./media/image5.png" width="624" height="327" />

Since we want to deploy the MEAN app onto Azure, we need to configure the app to connect to a remote MongoDB instance. We are going to do this by setting up an environment variable for the remote database and fallback to the local database when the remote one is not available. You will change the highlighted line of code to:

mongoose.connect(process.env.myRemoteUrl || database.localUrl);

> <img src="./media/image6.png" width="624" height="327" />

Let's try running the app locally by selecting the debug icon from the left menu(1). Next, click on the gear icon to open the configuration and select the environment "Node.js"(2)

> <img src="./media/image7.png" width="624" height="327" />

Open your browser and goto: <http://localhost:8080/> to verify that the app is running.

> <img src="./media/image9.png" width="624" height="327" />

Let's deploy this app onto Azure by using Docker. If you haven't used Docker before, Microsoft makes it super easy by providing extensions for Visual Studio Code. First, click on the extensions icon in the left menu(1). Verify that the Docker extension exists(2).

> <img src="./media/image10.png" width="624" height="327" />

Open the prompt using the hotkey CTRL+SHIFT+P and type in Docker. Since we haven't configured the image for this app, choose add Docker files to workspace.

> <img src="./media/image11.png" width="624" height="327" />

Next, we choose Node.js for our application platform and set the port to 8080.

> <img src="./media/image13.png" width="624" height="327" />
> <img src="./media/image14.png" width="624" height="327" />

Now, let's take a look at the Docker file we created(1). Highlight how you can change the node image by changing (2). Confirm that the start command is using server.js(3).

> <img src="./media/image15.png" width="624" height="327" />

The image is ready to be built! Bring up the prompt again with CTRL+SHIFT+P and search for Docker: Build Image.

> <img src="./media/image16.png" width="624" height="327" />

Next choose our Dockerfile we created earlier and prefix the image name with our DockerHub username: timesaved (use your own account). This will be used later when we push our image to DockerHub.
  
> <img src="./media/image17.png" width="624" height="327" />
> <img src="./media/image18.png" width="624" height="327" />

The Docker extension will issue the build command in the terminal. If you are familiar with the Docker commands, you could execute them directly from shell without the extension.

Next, we will push the image to the DockerHub to deploy it onto Azure. Let's use the extension again by opening the prompt with CTRL+SHIFT+P and search for Docker Push. Choose our image timesaved/node-todo:latest (your prefix may be different DockerHub account).

> <img src="./media/image19.png" width="624" height="327" />

The push commands executes and your Docker image is now on DockerHub.

Now we are ready to deploy our app onto Azure. We will be using the Azure CLI which is based on python that runs on any platform.

Our first step is to create a Resource group. Think of this as a logical grouping of Azure resources. We will run the following command:

`az group create -n meandemogroup -l westus`

Explain the parts of this command. The name of this Resource Group is meandemogroup and the location we chose was Western US data center.

> <img src="./media/image20.png" width="624" height="327" />

Let's use the configure command to set this Resource Group as our default so that we don't have to type it in subsequent commands.

`az configure -d group=meandemogroup`

Next, we will set up an App Service plan. This will define the infrastructure for the target deployment. The command is:

`az appservice plan create -n meandemoappserviceplan --is-linux`

We are including the Linux flag when creating the plan so that we get Linux virtual machines.

Note: This command may take a while to complete. You may want to perform these commands before the demo and breakdown each command to explain what each step does.

Now we can create an App Service Web App. We are going to create the Web App with the "i" option and provide the custom image we created (and pushed to DockerHub).

`az webapp create -n meandemoapp -p meandemoappserviceplan -i timesaved/node-todo`

Remember that the start command was defined as part of the Docker image. Therefore, running the Docker image will run the app.

Again, lets set the Web App as our default so that we do not have to keep typing it again in subsequent commands:

`az configure -d web=meandemoapp`

Next, let's browse the app to see if it works.

`az webapp browse`


Notice that the app does not load. This is because we no longer have access to our local MongoDB. We are going to provision a CosmosDB with a MongoDB adapter. This allows us to use CosmosDB as a drop in replacement for MongoDB.

To set this up, go back to your terminal in Visual Studio Code and run this command:

`az cosmosdb create -n meandemodb --kind MongoDB`

We now have a database and will have to configure our app to connect to it. To do this we will add an environment variable that contains the connection string to the database. Run the following command:

`$dbConnectionString=$(az cosmosdb list-connection-strings -n meandemodb -otsv --query "connectionStrings[0].connectionString")`

This command may look complicated, so let's break it down. We are using some PowerShell features to create a new variable that contains the result of the query for the list of CosmosDB connection string. What this does is queries CosmosDB for the connection strings, set the output to a tab delimited resultset, query the output for a specific connection string value that was returned.

Now that we have a connection string, let's add it to the environment variable for our app.

`az webapp config appsettings set --settings myRemoteUrl=$dbConnectionString`

Now go back to your browser to verify that your app is working now. The beauty of this setup is that we can now scale out our database with CosmosDB in line with our Web App residing in our scaleable App service plan.

> <img src="./media/image21.png" width="624" height="327" />

We can now go to the Azure portal to see the resources we created. First, click on the Resource Groups item on the left menu(1). Then, select our Resource Group for the demo: meandemogroup(2). Verify that all services we created for this demo: Web App, CosmosDB, and App Service Plan(3).


> <img src="./media/image22.png" width="624" height="327" />

### 

### Teardown Steps

### 

If you are not continuing to the next session demos you can delete the Azure resource group to remove all the services used in this demo.

1.  To delete the resource group from this demo, go into to the Resource group section within the Azure portal. Click on the ellipse (3 dots) button next to the resource group from this demo. Next, click on the delete action in the menu.

> <img src="./media/image22.png" width="624" height="327" />