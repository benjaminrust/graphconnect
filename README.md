# Harding Point : Engagement Graph : Connect
 

![Harding Point Engagement Graph](https://static.wixstatic.com/media/983560_7563ad3d347646e1a792e19a2c14e44c~mv2_d_2754_1836_s_2.png/v1/fill/w_1545,h_1030,al_c,usm_0.66_1.00_0.01/983560_7563ad3d347646e1a792e19a2c14e44c~mv2_d_2754_1836_s_2.png "Harding Point Graph Connect")


[Engagement Graph](http://www.HardingPoint.com) quickly builds and connects your Salesforce data with all your data 
islands.  The [Engagement Graph](http://www.HardingPoint.com) is used for deep analytics, artificial intelligence, 
reporting, and App Development. The more data and relationships you link with your [Engagement Graph](http://www.HardingPoint.com) 
the quicker it builds, learns (via AI), and reacts (via Engagement Manager) from your [Neural Network](http://www.HardingPoint.com).

* [`Graph Connect Deploy`](https://graphconnect.herokuapp.com/) - Live Graph Connect  (Recommend following instructions below, if first time)
* [`Engagement Manager & Orchestration` - Login: readonly/readonly](http://engage.hardingpoint.com/) - Uses Additional Package with your Engagement Graph
* [`Engagement Browser` - Try Custom App Demo Now ](https://engagementbrowser.herokuapp.com/?neoid=0011I000003ExJzQAK) - Powered by Graph Connect - Synchronized from Salesforce
* `Neural Network & AI` - Uses Additional Package on Top with your Engagement Graph
* `Analytics & Reporting` - Uses Additional Package with your Engagement Graph

# Installation Instructions

1. ##### Request Alpha Access to [EngagementGraph AddOn](https://elements.heroku.com/addons/engagementgraph)
    1. Email EarlyAccess@HardingPoint.com your Heroku Username

1. <a href="https://id.heroku.com/login" target="_new">Login to Heroku</a> or <a href="https://signup.heroku.com" target="_new">Create Heroku Credentials</a>

1. <a href="https://login.salesforce.com" target="_new">Login to Salesforce</a> or <a href="https://developer.salesforce.com/signup" target="_new">Create Salesforce Developer Edition</a>

1. <a href="https://login.salesforce.com/lightning/switcher?destination=classic" target="_new">Switch to Salesforce Classic</a>

1. <a href="https://login.salesforce.com/app/mgmt/forceconnectedapps/forceAppEdit.apexp" target="_new">Create a Salesforce Connected App</a>
    1. Connected App Name `graphconnect`
    1. Contact Email `Support@HardingPoint.com`
    1. Check `Enable OAuth Settings`
    1. Set the `Callback URL` to `http://localhost:9000/_oauth_callback`
    1. In `Available OAuth Scopes` select `Full access (full)` and click `Add`
        1. Save the new Connected App and keep track of the Consumer Key & Consumer Secret for later use
        
1. <a href="https://login.salesforce.com/setup/ui/listCustomSettings.apexp" target="_new">Create a Salesforce Custom Setting</a>
    1. Create Salesforce.com Custom Setting `HardingPoint as Hierarchy/Public`
    1. Create New Custom Field in HardingPoint Custom Setting `Name:ApiToken Field Type: Text(255)`
    1. Create New Custom Field in HardingPoint Custom Setting `Name:GatewayToken Field Type: Text(255)`
    1. Create New Custom Field in HardingPoint Custom Setting `Name:graphdburl Field Type:URL Click Save`
    <!-- 1. Create New Custom Field in HardingPoint Custom Setting `Name:APIURL Field Type: URL` -->

1. [![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

    1. Choose Heroku App Name
    1. Past Consumer Key & Consumer Secret into install boxes
        1. Values from above when you created 'Connected App' in Salesforce.
    1. Go to Heroku Config Vars copy `GRAPHCONNECT_URL`  (Needed in Salesforce)

1. ##### Check email for Alpha Invite `Will Be Removed After Release`
    1. Install `engagementgraph` after receiving the Alpha invite from Heroku.  Command below.
        1. [Install Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)
        1. Running at Terminal or Command Prompt (After installing Heroku CLI)
            1. heroku login
            1. heroku addons:create engagementgraph:test --app YOUR_APP_NAME_HERE

1. <a href="https://login.salesforce.com/setup/ui/listCustomSettings.apexp" target="_new">Update Custom Settings</a>
    1. Click on HardingPoint
    1. Click on Manage
    1. Click on New Default Organization Level Value
    1. Update `GatewayToken` with `ENGAGEMENTGRAPH_GATEWAYTOKEN` from Heroku Config Variables
    1. Update `ApiToken` with `ENGAGEMENTGRAPH_APITOKEN` from Heroku Config Variables
        1. Request Early Access by emailing EarlyAccess@HardingPoint.com your Heroku Username 
        1. All Alpha testers will be given free access
    1. Update `graphdburl` with `GRAPHCONNECT_URL` from Heroku Config Variables (You can use any Neo4j URL)
    <!-- 1. Update `APIURL` with `ENGAGEMENTGRAPH_APIURL` from Heroku Config Variables -->
        
1. <a href="https://login.salesforce.com/02u" target="_new">Edit Connected App for Salesforce</a>
    1. update the `Callback URL` to be `https://<YOUR_APP_NAME>.herokuapp.com/_oauth_callback`

# Deploying Graph Connect for Accounts

1. Login to https://<YOUR_APP_NAME>.herokuapp.com

1. Click [`Login via Salesforce - Normal Instance`]

    1. If you get a `Routing` error it is because Salesforce has not finished updating (wait 4 minutes)

1. Select SObject `Account` from SObject Dropdown

1. Click [`Connect to Graph`]

(It will automatically process the history)

![Harding Point Connecth](https://static.wixstatic.com/media/983560_433e31decb984e7caba4de2bcc4e8a54~mv2_d_3076_1874_s_2.png/v1/fill/w_1897,h_1156,al_c,usm_0.66_1.00_0.01/983560_433e31decb984e7caba4de2bcc4e8a54~mv2_d_3076_1874_s_2.png)


# View Graph
    
    
    1. Go back to your Heroku Dashboard and into <YOUR_APP_NAME>
    1. Click Resources
    1. Click GrapheneDB
        1. Scroll to bottom click `Launch` for Neo4j Browser
        1. Click Icon Top Left Corner
        1. You should see your object listed Click on it (ex Account)
        
        
# Reproducing Engagement Graph From Above Image

    1. Deploy Graph Connect Account (Did above already)
    1. Deploy Graph Connect Contact
    1. Deploy Graph Connect Opportunity
    1. Deploy Graph Connect Case
    
        
# Cleaning Graph

When you deploy Graph Connect it automatically processes the history.

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
    
# Querying Data

##### Matching By Id

    MATCH (n{Id:'0010x000002IHpJAAW'}) return n;

##### Matching Node and Relationships

    MATCH (n{Id:'0010x000002IHpJAAW'})-[r]-(b) return b.name, labels(b);
    

##### Return Node and All Relationships

    MATCH (c:Account{sfdcid:"0013900001ZglUQAAZ"}) 
    WITH c
    OPTIONAL MATCH (c)-[r]-()
    RETURN c, r
   

    
