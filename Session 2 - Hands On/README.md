## Continuous deployment to Azure with Visual Studio and Git with ASP.NET Core

1. [Prerequisites](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#prerequisites)
2. [Create an ASP.NET Core web app](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#create-an-aspnet-core-web-app)
3. [Create a web app in the Azure Portal](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#create-a-web-app-in-the-azure-portal)
4. [Enable Git publishing for the new web app](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#enable-git-publishing-for-the-new-web-app)
5. [Publish the web app to Azure App Service](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#publish-the-web-app-to-azure-app-service)
6. [Run the app in Azure](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#run-the-app-in-azure)
7. [Update the web app and republish](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#update-the-web-app-and-republish)
8. [View the updated web app in Azure](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#view-the-updated-web-app-in-azure)

This tutorial shows how to create an ASP.NET Core web app using Visual Studio and deploy it from Visual Studio to Azure App Service using continuous deployment.

See also [Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment](https://docs.microsoft.com/en-us/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic), which shows how to configure a continuous delivery (CD) workflow for [Azure App Service](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-overview) using Visual Studio Team Services. Azure Continuous Delivery in Team Services simplifies setting up a robust deployment pipeline to publish updates for apps hosted in Azure App Service. The pipeline can be configured from the Azure portal to build, run tests, deploy to a staging slot, and then deploy to production.

To complete this tutorial, a Microsoft Azure account is required. To obtain an account, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

### Prerequisites[](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#prerequisites)

This tutorial assumes the following software is installed:

- [Visual Studio](https://www.visualstudio.com/)
- [.NET Core SDK 2.0 or later](https://www.microsoft.com/net/download) 
- [Git](https://git-scm.com/downloads) for Windows

### Create an ASP.NET Core web app[](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#create-an-aspnet-core-web-app)

1. Start Visual Studio. 
2. From the **File** menu, select **New** &gt; **Project**. 
3. Select the **ASP.NET Core Web Application** project template. It appears under **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **.NET Core**. Name the project SampleWebAppDemo. Select the **Create new Git repository** option and click **OK**. 
![Image1](../images/01-new-project.png?raw=true)

4. In the **New ASP.NET Core Project** dialog, select the ASP.NET Core **Empty** template, then click **OK**. 
![Image2](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On/images/02-web-site-template.png?raw=true)

#### Running the web app locally[](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#running-the-web-app-locally)

1. Once Visual Studio finishes creating the app, run the app by selecting **Debug** &gt; **Start Debugging**. As an alternative, press **F5**. It may take time to initialize Visual Studio and the new app. Once it's complete, the browser shows the running app. 

![Image3](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On/images/04-browser-runapp.png?raw=true)


2. After reviewing the running Web app, close the browser and select the "Stop Debugging" icon in the toolbar of Visual Studio to stop the app. 

### Create a web app in the Azure Portal[](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#create-a-web-app-in-the-azure-portal)

The following steps create a web app in the Azure Portal:

1. Log in to the [Azure Portal](https://portal.azure.com/). 
2. Select **NEW** at the top left of the portal interface. 
3. Select **Web + Mobile** &gt; **Web App**. 

![Image4](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On/images/05-azure-newwebapp.png?raw=true)


4. In the **Web App** blade, enter a unique value for the **App Service Name**. 

![Image5](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On/images/06-azure-newappblade.png?raw=true)

5. Select **Create**. Azure will provision and start the web app. 

![Image6](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On/images/07-azure-webappblade.png?raw=true)

### Enable Git publishing for the new web app[](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#enable-git-publishing-for-the-new-web-app)

Git is a distributed version control system that can be used to deploy an Azure App Service web app. Web app code is stored in a local Git repository, and the code is deployed to Azure by pushing to a remote repository.

1. Log into the [Azure Portal](https://portal.azure.com/). 
2. Select **App Services** to view a list of the app services associated with the Azure subscription. 
3. Select the web app created in the previous section of this tutorial. 
4. In the **Deployment** blade, select **Deployment options** &gt; **Choose Source** &gt; **Local Git Repository**. 

![Image7](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On/images/deployment-options.png?raw=true)

5. Select **OK**. 
6. If deployment credentials for publishing a web app or other App Service app haven't previously been set up, set them up now: 
    - Select **Settings** &gt; **Deployment credentials**. The **Set deployment credentials** blade is displayed.
    - Create a user name and password. Save the password for later use when setting up Git.
    - Select **Save**.

7. In the **Web App** blade, select **Settings** &gt; **Properties**. The URL of the remote Git repository to deploy to is shown under **GIT URL**. 
8. Copy the **GIT URL** value for later use in the tutorial. 

![Image8](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On/images/09-azure-giturl.png?raw=true)

### Publish the web app to Azure App Service[](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#publish-the-web-app-to-azure-app-service)

In this section, create a local Git repository using Visual Studio and push from that repository to Azure to deploy the web app. The steps involved include the following:

- Add the remote repository setting using the GIT URL value, so the local repository can be deployed to Azure.
- Commit project changes.
- Push project changes from the local repository to the remote repository on Azure.

1. In **Solution Explorer** right-click **Solution 'SampleWebAppDemo'** and select **Commit**. The **Team Explorer** is displayed. 

![Image9](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On/images/10-team-explorer.png?raw=true)

2. In **Team Explorer**, select the **Home** (home icon) &gt; **Settings** &gt; **Repository Settings**. 
3. In the **Remotes** section of the **Repository Settings**, select **Add**. The **Add Remote**

dialog box is displayed. 
4. Set the **Name** of the remote to **Azure-SampleApp**. 
5. Set the value for **Fetch** to the **Git URL** that copied from Azure earlier in this tutorial. 

![Image10](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On/images/11-add-remote.png?raw=true)

6. Select the **Home** (home icon) &gt; **Settings** &gt; **Global Settings**. Confirm that the name and email address are set. Select **Update** if required. 
7. Select **Home** &gt; **Changes** to return to the **Changes** view. 
8. Enter a commit message, such as **Initial Push #1** and select **Commit**. This action creates a _commit_ locally. 

![Image11](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On/images/12-initial-commit.png?raw=true)

9. Select **Home** &gt; **Sync** &gt; **Actions** &gt; **Open Command Prompt**. The command prompt opens to the project directory. 
10. Enter the following command in the command window: 

git push -u Azure-SampleApp master 
11. Enter the Azure **deployment credentials** password created earlier in Azure. This command starts the process of pushing the local project files to Azure. The output from the above command ends with a message that the deployment was successful. Copy			  

remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://username@samplewebappdemo01.scm.azurewebsites.net:443/SampleWebAppDemo01.git
* [new branch]      master -&gt; master
Branch master set up to track remote branch master from Azure-SampleApp.
Note If collaboration on the project is required, consider pushing to [GitHub](https://github.com/) before pushing to Azure.  

#### Verify the Active Deployment[](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#verify-the-active-deployment)

Verify that the web app transfer from the local environment to Azure is successful.

In the [Azure Portal](https://portal.azure.com/), select the web app. Select **Deployment** &gt; **Deployment options**.

### Run the app in Azure[](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#run-the-app-in-azure)

Now that the web app is deployed to Azure, run the app.

This can be accomplished in two ways:

- In the Azure Portal, locate the web app blade for the web app. Select **Browse** to view the app in the default browser.
- Open a browser and enter the URL for the web app. Example: 

http://SampleWebAppDemo.azurewebsites.net

### Update the web app and republish[](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#update-the-web-app-and-republish)

After making changes to the local code, republish:

1. In **Solution Explorer** of Visual Studio, open the _Startup.cs_ file. 
2. In the Configure method, modify the Response.WriteAsync method so that it appears as follows: 		  

await context.Response.WriteAsync("Hello World! Deploy to Azure.");

3. Save the changes to _Startup.cs_. 
4. In **Solution Explorer**, right-click **Solution 'SampleWebAppDemo'** and select **Commit**. The **Team Explorer** is displayed. 
5. Enter a commit message, such as Update #2. 
6. Press the **Commit** button to commit the project changes. 
7. Select **Home** &gt; **Sync** &gt; **Actions** &gt; **Push**. 

### View the updated web app in Azure[](https://github.com/DevScope/HandsOn-ASP.NETCore/tree/master/Session%202%20-%20Hands%20On#view-the-updated-web-app-in-azure)

View the updated web app by selecting **Browse** from the web app blade in the Azure Portal or by opening a browser and entering the URL for the web app. Example: 

http://SampleWebAppDemo.azurewebsites.net