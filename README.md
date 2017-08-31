# Harding Point : Engagement Graph : Connect
 

![Harding Point Engagement Graph](https://static.wixstatic.com/media/983560_7563ad3d347646e1a792e19a2c14e44c~mv2_d_2754_1836_s_2.png/v1/fill/w_1545,h_1030,al_c,usm_0.66_1.00_0.01/983560_7563ad3d347646e1a792e19a2c14e44c~mv2_d_2754_1836_s_2.png "Harding Point Graph Connect")


[Engagement Graph](http://www.HardingPoint.com) quickly builds and connects your Salesforce data with all your data 
islands.  The [Engagement Graph](http://www.HardingPoint.com) is used for deep analytics, artificial intelligence, 
reporting, and App Development. The more data and relationships you link with [Engagement Graph](http://www.HardingPoint.com) 
builds your living [Neural Network](http://www.HardingPoint.com).

* `Neural Network & AI` - Uses Additional Package on Top with your Engagement Graph
* `Engagement Orchestration & Flow` - Uses Additional Package with your Engagement Graph
* `Analytics & Reporting` - Uses Additional Package with your Engagement Graph

Use the shared instance of this app [https://graphconnect.herokuapp.com](https://graphconnect.herokuapp.com) or deploy 
your own instance on Heroku following instructions below. Recommend following instructions below unless you are 
linking multiple Salesforce instances to a single graph.

# Installation Instructions
1. [Login to Heroku](https://id.heroku.com/login) or [Create Heroku Credentials](https://signup.heroku.com)
1. [Login to Salesforce](https://login.salesforce.com) or [Create Salesforce Developer Edition](https://developer.salesforce.com/signup)

1. [Create a Salesforce Connected App](https://login.salesforce.com/app/mgmt/forceconnectedapps/forceAppEdit.apexp)
    1. Connected App Name `graphconnect`
    1. Contact Email `Support@HardingPoint.com`
    1. Check `Enable OAuth Settings`
    1. Set the `Callback URL` to `http://localhost:9000/_oauth_callback`
    1. In `Available OAuth Scopes` select `Full access (full)` and click `Add`
        1. Save the new Connected App and keep track of the Consumer Key & Consumer Secret for later use
1. [Create a Salesforce Custom Setting](https://login.salesforce.com/setup/ui/listCustomSettings.apexp)
    1. Create Salesforce.com Custom Setting `HardingPoint as Hierarchy/Public`
    1. Create New Custom Field in HardingPoint Custom Setting `Name:graphdburl Field Type:URL Click Save` (Leave 
        page open we will change after install)

1. [![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

    1. Choose Heroku App Name
    1. Past Consumer Key & Consumer Secret into install boxes
    1. Go to Heroku Config Vars copy `GRAPHCONNECT_URL`  (Needed in Salesforce)
    
1. [Switch to Salesforce Classic](https://login.salesforce.com/lightning/switcher?destination=classic)

1. [Update Custom Settings](https://login.salesforce.com/setup/ui/listCustomSettings.apexp) 
    1. Click on HardingPoint
    1. Click on Manage
    1. Click on New Default Organization Level Value
    1. Update `graphdburl` with `GRAPHCONNECT_URL` from Heroku Config
        
1. [Edit Connected App for Salesforce](https://login.salesforce.com/02u) 
    1. update the `Callback URL` to be `https://<YOUR_APP_NAME>.herokuapp.com/_oauth_callback`

# Deploying Graph Connect for Accounts

1. Login to https://<YOUR_APP_NAME>.herokuapp.com

1. Click [`Login via Salesforce - Normal Instance`]

    1. If you get a `Routing` error it is because Salesforce has not finished updating (wait 4 minutes)
    
1. Change Name to `Account` (It must be unique and has a limit)

1. Select SObject `Account` from SObject Dropdown

1. Select [`After Insert`] and [`After Update`]

1. Click [`Connect to Graph`]


# Testing Engagement Graph
    
1. [Update a Few Account Records](https://login.salesforce.com/001) - modify any data (Sends them to Graph)

1. Visit Graph
    
    1. Go back to your Heroku Dashboard and into <YOUR_APP_NAME>
    1. Click Resources
    1. Click GrapheneDB
        1. Scroll to bottom click `Launch` for Neo4j Browser
        1. Click Icon Top Left Corner
        1. You should see your object listed Click on it (ex Lead)
        
        
# Reproducing Engagement Graph From Above Image
    
1. Unlocking Hidden Connections

    1. [Deploy Graph Connect](http://www.HardingPoint.com) to User, Contact, Opportunity, Case
        1. Following "Deploying Engagement Graph" from Above for all objects listed above @ https://<YOUR_APP_NAME>.herokuapp.com
    1. Update your user or a user associated with the records (we used a demo account)
    1. Edit/Save your user [All Users](https://login.salesforce.com/005) - Change 1 piece of data
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
   

    
