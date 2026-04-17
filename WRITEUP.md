## Analyze, choose, and justify the appropriate resource option for deploying the app.

### Analysis of Deployment Solutions<br/>
**Virtual Machine (VM)**
* **Costs:** VMs are usually more expensive in the long run. Aside from the hourly rate for the compute, there’s a lot of "hidden" cost in the time spent managing the OS, security patches, and updates.
* **Scalability:** It's not very flexible. If the CMS gets a sudden traffic spike, I’d have to manually set up Scale Sets and Load Balancers, which is a lot of extra work to get right.
* **Availability:** To keep the site from going down, I'd have to manage my own Availability Sets. If the specific server hardware fails, the app goes down unless I’ve built a redundant setup myself.
* **Workflow:** The workflow is pretty slow. I have to RDP/SSH into the box, install the web server, and manually move code, which makes it harder to do quick updates.<br/>

**App Service**
* **Costs:** This is much better for the budget. I’m only paying for the App Service Plan, and since Azure handles the maintenance, I don't have to waste time (or money) on server admin tasks.
* **Scalability:** It’s almost effortless. I can just toggle on Autoscale, and the app will handle more users by adding more instances automatically based on CPU usage.
* **Availability:** High availability is essentially "baked in." Microsoft handles the patching and hardware health, so I don't have to worry about the site crashing because of a server-level failure.
* **Workflow:** This is the biggest win. I can link it directly to my GitHub repo so that every time I push code, the site updates automatically. Using deployment slots also means I can test things before they go live.<br/>

### Chosen Solution and Justification
I decided to go with **Azure App Service** for this deployment. For a CMS, it just makes more sense to use a managed service where I don't have to worry about the underlying infrastructure. It's faster to set up, easier to scale, and the built-in CI/CD support makes the whole development process a lot smoother than trying to manage a full Virtual Machine.<br/><br/>

## Assess app changes that would change your decision.<br/>
### How will the app change per your decision? <br/>
The biggest shift is that the app becomes more "cloud-native." I lose the ability to tweak deep OS settings, but I gain way more control over how the app is deployed and monitored. It also forces the app to be more reliable since it’s designed to run in a managed environment where instances might be swapped or restarted by Azure.<br/><br/>

### Other needs you must change to suit your application requirements:
* **Centralized Storage:** Since App Service storage isn't permanent for files, I'll need to use Azure Blob Storage for any images or documents uploaded to the CMS.
* **Database:** I'll connect the app to an Azure SQL instance instead of trying to run a database locally.
* **Config Settings:** I’ll move all the sensitive stuff, like API keys and connection strings, into the App Service "Environment Variables" so they aren't sitting in the code.
