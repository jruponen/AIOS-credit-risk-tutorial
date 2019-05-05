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

Login to IBM Cloud at (https://cloud.ibm.com)

From the Dashboard, click Catalog, search for "object storage" and select "Object Storage"

Change service name to more descriptive, like:
Service name:	WS-ObjectStorage

Scroll down for "Pricing Plans"
Make sure "Lite" is selected for free testing

Press [Create]

In Cloud Object Storage service dashboard that opens, do nothing but instead
on the top menu, click Catalog again, select AI category and select "Machine Learning"

Change service name to more descriptive, like:
Service name:	Watson ML

Scroll down for "Pricing Plans"
Make sure "Lite" is selected for free testing

Press [Create]

In Watson Machine Learning service dashboard that opens, do nothing but instead
on the top menu, click Catalog again, select AI category "Watson Studio"

Change service name to more descriptive, like:
Service name:	Watson Studio

Scroll down for "Pricing Plans"
Make sure "Lite" is selected for free testing

Press [Create]

