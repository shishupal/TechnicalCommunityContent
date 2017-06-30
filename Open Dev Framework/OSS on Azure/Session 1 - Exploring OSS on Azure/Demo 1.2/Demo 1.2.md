# Demo 1.2: Tour of Open Source on Azure

This demo should take about 5 minutes.

## Objectives

The goal is to provide an overview of Open Source support on Azure.

## Requirements


Internet connection is required in order to access the Azure portal.

An active Azure subscription is required to host both the sample NodeJS app.

1.  Click on the Start free button.

    <img src="./media/image1.png" width="624" height="327" />

2.  Once registration is complete. You will need to log into the Azure portal to continue the demo setup process.

## Setup

Make sure to create your Azure account before the event.

Setting up the demo takes a few minutes so make sure to create it before the presentation. 


### Setup the App Service and Resource group

1.  Create an App Service that will automatically create a Resource Group to organize and manage all the Azure services that will be used by the demo.

> <img src="./media/image2.png" width="624" height="327" />

1. First, click the Add button (1). In the search box, enter the text "node"(2). Next, click on the Node JS Starter site (3). Then, click the Create button to complete the creating the resource group (4). Next, enter timesavednodejsdemo (or any other unique name) for the App name (5). Then, enter TimeSavedDemos for the Resource group (6). Finally, click on create (7). 

> <img src="./media/image3.png" width="624" height="327" />
> <img src="./media/image4.png" width="624" height="327" />

Now we will pin the Resource Group and App service activity to make our dashboard more interesting for the audience.

1. First, click on Resource Groups to open the Resource Group window (1). Next, enter the Resource Group name we created: TimeSavedDemos (2). Finally, right-click on TimeSavedDemos and select Pin to dashboard.

> <img src="./media/image5.png" width="624" height="327" />

This will place the resources listing for your TimeSavedDemos resource group on the dashboard.

1. For the app service activity, click on App Services from the menu (1). Next, search for your App Service by typing in timesavednodejsdemo (or the given name when you created the service) (2). Then, click on your app service (3). Finally click on the pins for the charts to add to your dashboard (4)

> <img src="./media/image6.png" width="624" height="327" />
> <img src="./media/image7.png" width="624" height="327" />



### Setup Deployment slots for the App Service
1.  Next we will add deployment slots for your Node JS starter app by clicking Deployment Slots (1). Next, click on Add Slot (2). Then, enter the name of the deployment slot. For this demo we will use "staging" (3). Finally, click OK (4).

> <img src="./media/image8.png" width="624" height="327" />
> <img src="./media/image9.png" width="624" height="327" />


### Demo Steps

### 

During the demo, the goal is to provide an overview of the breadth of support Azure offers for Open Source technology. The video provides a guideline of some of the items you may show and you are free to adjust the content accordingly.

You will start the demo with by accessing the Azure portal at https://portal.azure.com 

If you completed the setup steps before you started your demo, your dashboard should look like this:

> <img src="./media/image10.png" width="624" height="327" />

Highlight some of your favorite services from the left menu. If applicable, share a brief story about your experience with a particular service you used for Open Source.

Jump into the Resource group view and provide a brief explanation. A resource group is a logical grouping of Azure services. For example, in our setup, we have a TimeSavedDemos resource group that contains an App Service and a Web Service. You can add more to this resource group such as Linux virtual machines, NodeJS apps, and MongoDB. Click on the Resource Group you created in the setup steps and show the services you have deployed.

> <img src="./media/image11.png" width="624" height="327" />

Highlight the other Open Source services that are available by clicking on More Services in the left menu.

> <img src="./media/image12.png" width="624" height="327" />

On this screen highlight how many other services available such as virtual machines, Internet of things services, and data services.

Next, show the audience how to create a new service by clicking the New button.

> <img src="./media/image13.png" width="624" height="327" />

This will show a list of the available services and for this example, we will show them how to create a new Linux Virtual Machine. Click on Compute to see the list of virtual machines available.

> <img src="./media/image14.png" width="624" height="327" />

Go over how there are many different flavors of Linux VMs available such as Red Hat, Ubuntu, and SUSE. You can also find preconfigured Linux VMs that contain the Open Source software required to run LAMP, Wordpress, MEAN, and many more. For this demo we will show all the different preconfigured Linux VMs for MEAN. MEAN stands for MongoDB, ExpressJS, AngularJS, and NodeJS.

> <img src="./media/image15.png" width="624" height="327" />

Go back to the dashboard to talk about some of the items you have pinned. We can monitor our services with charts on traffic and errors in realtime. We can add shortcuts for quick access to our most critical applications. Click on one of the apps in your Resource group pinned on the dashboard.

> <img src="./media/image16.png" width="624" height="327" />

Show how you can have multiple deployment slots by clicking on deployment slot. (1) We have a production version with the app service and a web service for the staging environment. Next, click on the staging deployment slot (2)

> <img src="./media/image17.png" width="624" height="327" />

Next, click on the deployment options to show how Azure supports a variety of ways to deploy your application with the version control tools you are accustomed to such as GitHub, BitBucket, and VSTS.

> <img src="./media/image18.png" width="624" height="327" />
> <img src="./media/image19.png" width="624" height="327" />

Now go back to the dashboard and click on your timesavednodejsdemo app again.

> <img src="./media/image16.png" width="624" height="327" />

Click on Deployment options to access the Github commit log(1). Let the audience know that the deployment option for this app is via GitHub. Next, click on the GitHub commit (2). 

> <img src="./media/image20.png" width="624" height="327" />

You will now be able to view the log and see what node packages were installed for each commit.
> <img src="./media/image21.png" width="624" height="327" />

As you can see, Azure is truly technology agnostic and you can use all sorts of Open Source on the platform.


### 

### Teardown Steps

### 


1.  To delete the resource group from this demo, go into to the Resource group section within the Azure portal. Click on the ellipse (3 dots) button next to the resource group from this demo. Next, click on the delete action in the menu.

> <img src="./media/image22.png" width="624" height="327" />