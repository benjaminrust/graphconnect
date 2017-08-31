# Harding Point : Graph Connect
 

![Harding Point Graph Connect](https://static.wixstatic.com/media/983560_7563ad3d347646e1a792e19a2c14e44c~mv2_d_2754_1836_s_2.png/v1/fill/w_1545,h_1030,al_c,usm_0.66_1.00_0.01/983560_7563ad3d347646e1a792e19a2c14e44c~mv2_d_2754_1836_s_2.png "Harding Point Graph Connect")


[`Graph Connect`](http://www.HardingPoint.com) quickly builds and connects your Salesforce data with all your data 
islands.  The object graph is used for deep analytics, artificial intelligence, reporting, and App Development. The 
more data and relationships you link with [`Graph Connect`](http://www.HardingPoint.com) builds your living [`Neural 
Network`](http://www.HardingPoint.com).

Either use a shared instance of this app: https://graphconnect.herokuapp.com

Or deploy your own instance on Heroku:

You will need Salesforce credentials of [Create a Developer Edition](https://developer.salesforce.com/signup)

# Deployment
1. [Log into Salesforce](https://login.salesforce.com/) to Configure:

    1. [Click to Create a Connected App](https://login.salesforce.com/app/mgmt/forceconnectedapps/forceAppEdit.apexp)
        1. Connected App Name `graphconnect`
        1. Contact Email `Support@HardingPoint.com`
        1. Check `Enable OAuth Settings`
        1. Set the `Callback URL` to `http://localhost:9000/_oauth_callback`
        1. In `Available OAuth Scopes` select `Full access (full)` and click `Add`
        1. Save the new Connected App and keep track of the Consumer Key & Consumer Secret for later use
    1. [Click to Create a Custom Setting](https://login.salesforce.com/setup/ui/listCustomSettings.apexp)
        1. Create Salesforce.com Custom Setting `HardingPoint as Hierarchy/Public`
        1. Create New Custom Field in HardingPoint Custom Setting `Name:graphdburl Field Type:URL Click Save` (Leave 
        page open we will change after install)

1. Deploy this app on Heroku: [![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

    1. Choose Heroku App Name
    1. Past Consumer Key & Consumer Secret into install boxes
    1. Go to Heroku Config Vars copy `GRAPHCONNECT_URL`  (Needed in Salesforce)
    
1. Update Salesforce Settings

    1. Use Salesforce Classic to Edit Settings
    1. Update [Custom Settings](https://login.salesforce.com/setup/ui/listCustomSettings.apexp) 
        1. Click on HardingPoint
        1. Click on Manage
        1. Click on New Default Organization Level Value
        1. Update `graphdburl` with `GRAPHCONNECT_URL` from Heroku Config
        
    1. Edit the [Connected App](https://login.salesforce.com/02u) on Salesforce and update the `Callback URL` to be 
    `https://<YOUR_APP_NAME>.herokuapp.com/_oauth_callback`

# Testing

1. Configure [`Graph Connect`](http://www.HardingPoint.com)

    1. Visit https://<YOUR_APP_NAME>.herokuapp.com
    1. Login Via Salesforce
    1. Choose SObject you want to add to graph (Recommend Try Lead)
    1. Select after insert AND after update
    1. Change Name (has to be unique) - it will automatically add WebhookTrigger to end
        1. There is a limit to name length
    1. Connect to Graph
    1. Edit and Save Lead
    
1. Visit Graph
    
    1. Go back to your Heroku Dashboard and into <YOUR_APP_NAME>
    1. Click Resources
    1. Click GrapheneDB
        1. Scroll to bottom click `Launch` for Neo4j Browser
        1. Click Icon Top Left Corner
        1. You should see your object listed Click on it (ex Lead)
        
        
### Reproducing Graph At Top
    
1. Unlocking Hidden Connections

    1. Add [`Graph Connect`](http://www.HardingPoint.com) to User, Account, Contact, Opportunity, Case
        1. Following Step #1 under Testing Above for all objects listed above @ https://<YOUR_APP_NAME>.herokuapp.com
    1. Update your user or a user associated with the records (we used a demo account)
    1. Edit/Save your user [All Users](https://login.salesforce.com/005) - Change 1 piece of data
    1. Go run the [All Open Leads View](https://login.salesforce.com/00Q) - Mass update or update each record
    1. Go run the [All Accounts View](https://login.salesforce.com/001) - Mass update or update each record
    1. Go run the [All Contact View](https://login.salesforce.com/003) - Mass update or update each record
    1. Go run the [All Opportunities View](https://login.salesforce.com/006)- Mass update or update each record
    1. Go run the [All Closed Cased](https://login.salesforce.com/500)- Mass update or update each record
    1. Return to the Neo4j Browser 
        1. Directions from "Visit Graph" from above
        1. Click on "User"
        1. Double click on your User in the Graph to expand relationships
        
        
# Cleaning Graph

The graph will automatically repopulate with any data which is inserted and/or updated. The graph will not insert 
duplicates as it matches on the Id.

##### Delete All Data
    MATCH (n)
    DETACH DELETE n
    
    (Be Careful This Deletes Everything)
    
##### Delete One Node with Relationships
    MATCH (n { name: 'Andres' })
    DETACH DELETE n
    
##### Deleting Using the Salesforce Id
    
    MATCH (n { Id: '00Q1I000001xNBdUAM' })
    DETACH DELETE n
   

    
