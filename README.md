# AIOS-tutorial-credit-risk

Jukka Ruponen / IBM, 2019-05-04  

This is a sample tutorial to work with AI OpenScale (currently named as "Watson OpenScale").  

It is based on the Watson OpenScale tutorial [here](https://cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-obj), but is modified slightly for better suit to instructed tutorials in workshops.


### Pre-requisities

- You should have completed the AI OpenScale fast-start tutorial [here](https://cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start).

After completed the fast-start tutorial already (above), you should have:  
- IBM Cloud account (with an "IBM ID")
- Watson OpenScale service

To do this exercise, you are also going to need:  
- Watson Studio instance (will be created in this exercise)
- Watson Machine Learning instance (will be created in this exercise)
- Cloud Object Storage instance (will be created in this exercise)

All these can be created from IBM Cloud Catalog, under the AI category.  

If you do have some of these already, you can re-use them and do NOT need to recreate the services.  
(Just skip those steps below and follow instructions according to your environment/services).


### Short description of the tasks
1. Create the needed services
2. Create and configure a project in Watson Studio
3. Create and deploy "Credit Risk" model in WML (Watson Machine Learning service)
4. Setup Watson OpenScale to connect to your deployed model in WML
5. Configure OpenScale Monitors for "Credit Risk" model
6. Validate accuracy and fairness of the "Credit Risk" model in OpenScale
7. Make more scoring requests in WML to see how the monitored values change
8. Provide additional feedback data to assess accuracy


### Step 1 - Create the needed services

Login to IBM Cloud at https://cloud.ibm.com  

From the **IBM Cloud Dashboard**, click **Catalog**, search for text "**object storage**" and select "**Object Storage**"  

Change service name to more descriptive, like:  
Service name:	**WS-ObjectStorage**  

Scroll down for "**Pricing Plans**"  
Make sure "**Lite**" is selected for free testing  

Press **[Create]**  

In the Cloud Object Storage service details page that opens do nothing.   
Instead, click **Catalog** again on the top menu, select **AI** category and select "**Machine Learning**" service.  

Change service name to more descriptive, like:  
Service name:	**Watson ML**  

Scroll down for "**Pricing Plans**"  
Make sure "**Lite**" is selected for free testing  

Press **[Create]**  

In Watson Machine Learning service details page that opens do nothing.  
Instead, click **Catalog** again on the top menu, select **AI** category and select "**Watson Studio**" service.  

Change service name to more descriptive, like:  
Service name:	**Watson Studio**  

Scroll down for "**Pricing Plans**"  
Make sure "Lite" is selected for free testing  

Press **[Create]**  

You should be now at the Watson Studio service details page.  
Keep it open for the next step.  


### Step 2 - Create and configure a project in Watson Studio

On the Watson Studio service details page, press **[Get Started]**  

You should be now at the **Watson Studio welcome page**.  
Let's continue by creating our AI project, configure the project with Cloud Object Storage and Watson Machine Learning services (that you created above) and finally create our model and deploy to WML.  

Press **[Create a project]**  

Click **"Standard"** to create an empty project and set the follwing values:  

  Name: **AI model and validation project**  
  Description: **Credit Risk model for OpenScale monitoring and validation**  
  Define storage: Select your just created "**WS-ObjectStorage**"  

Press **[Create]**  

You are now in an empty project.  

Let's connect the **Watson Machine Learning service** to our project.  

On the top row, select "**Settings**" tab and scroll down to "**Associated services**"  
Next to "**Associated services**" section, press **[Add service]** drop down list on the right and select "**Watson**".  

Then press **[Add]** on the "**Machine Learning**" service area.  
On the "**Existing**" tab, select your existing Machine Learning service "**Watson ML**", that you just created earlier.  

Press **[Select]**


### Step 3 - Create and deploy "Credit Risk" model in WML (Watson Machine Learning service)

Let's create our Credit Risk model from sample.  

From the top actions, press **[+ Add to project]** and select "**Watson Machine Learning model**"  

On the right side section, select model type as "**From sample**"  
Select "**Credit Risk**" model (notice that when selected the name of model was also set to "**credit-risk**")  

Press **[Create]**  

Since your newly created model now opens in WML, we can also deploy it at once.  
Select "**Deployments tab**" and click **[Add deployment]**.  

Define the settings as:  
  Name: **credit-risk-deployment**  
  Deployment type: **Web service**  

Press **[Save]**  

You can now go back to your project page:  
On the top navigation path "My Projects / AI model and validation project", click on the project name "**AI model and validation project**".  

You should be now in the "**Assets**" view of the project and you should see your model under the "**Models**" section:

  *credit-risk, trained, mlib-2.3, spark-2.3 ...*


### Step 4 - Setup Watson OpenScale to connect to your deployed model in WML

Let's next configure OpenScale and connect to the model we just deployed.  

To access the OpenScale dashboard, go to https://aiopenscale.cloud.ibm.com  

Alternative way to go to your OpenScale dashboard:  
  Go to IBM Cloud at https://cloud.ibm.com  
  On the dashboard, the first "**Resource summary**" widget shows summary of your apps and services  
  Click "**Services**"  
  Scroll down until you see the "**Watson OpenScale**" service and click on its name  
  On the Watson OpenScale service details page, press **[Launch Application]**  


When in OpenScale dashboard, press the "**Configure**" icon on the left side options (it is the fourth from top).  

In the "**Configuration Summary**" page, press **[Edit]** (on the bottom of page)  

Select "**Watson Machine Learning**"  
(Notice, that OpenScale supports other scoring platforms as well)

Either keep the currently selected WML instance (recommended) or change it if needed.  
Remember, the "**Watson ML**" is the service we need to connect to because that is where we deployed our model.  

Press **[Next]**  

On the list of WML deployments, select the "**credit-risk-deployment**".  
**Note**: If there are other models selected already, you may want to keep them as well to retain their configuration in OpenScale).  

Press **[Next]**  

On the "**Select your database**" page, select the "**Use the free Lite plan database**"  
**Note**: Using the lite plan database is not GDPR compliant. Use it for testing only.  
For production use, setup a productional Db2 or PostgreSQL database instead.  

Press **[Next]**  

On the "**Summary**" page, press **[Save]** and then **[Yes]**  

Finally, when the configuration is saved, press **[Configure monitors]**  


