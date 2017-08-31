# Harding Point : Graph Connect

This app allows you to quickly connect your Salesforce objects to Harding Point object graph.  For usage info see: http://www.HardingPoint.com/

Either use a shared instance of this app: https://graphconnect.herokuapp.com

Or deploy your own instance on Heroku:

You will need Salesforce credentials of [Create a Developer Edition](https://developer.salesforce.com/signup)

# Deployment
1. [Log into Salesforce](https://login.salesforce.com/) to Configure:

    1. [Click to Create a Connected App](https://login.salesforce.com/app/mgmt/forceconnectedapps/forceAppEdit.apexp)
        1. Check `Enable OAuth Settings`
        1. Set the `Callback URL` to `http://localhost:9000/_oauth_callback`
        1. In `Available OAuth Scopes` select `Full access (full)` and click `Add`
        1. Save the new Connected App and keep track of the Consumer Key & Consumer Secret for later use
    1. [Click to Create a Custom Setting](https://login.salesforce.com/setup/ui/listCustomSettings.apexp)
        1. Create Salesforce.com Custom Setting `HardingPoint as Hierarchy/Public`
        1. Create New Custom Field in HardingPoint Custom Setting `Name:graphdburl Field Type:URL Click Cave` (Leave page open we will change after install)

1. Deploy this app on Heroku: [![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

    1. Choose Heroku App Name
    1. Past Consumer Key & Consumer Secret into install boxes
    1. Go to Heroku Config Vars copy `GRAPHCONNECT_URL`  (Needed in Salesforce)
    
1. Update Salesforce Settings

    1. Update `graphdburl Custom Setting` with `GRAPHCONNECT_URL` from Heroku Config
    1. Edit the Connected App on Salesforce and update the `Callback URL` to be `https://YOUR_APP_NAME.herokuapp.com/_oauth_callback`

# Testing

1. Configure Graph Connect 

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
        
# Cleaning Graph

The graph will automatically repopulate with any data which is inserted and/or updated. The graph will not insert duplicates as it matches on the Id.
    
#### Delete All Data
    MATCH (n)
    DETACH DELETE n
    
    (Be Careful This Deletes Everything)
    
#### Delete one node and all relationships
    MATCH (n { name: 'Andres' })
    DETACH DELETE n
    
    (Use the Salesforce Id vs Name
    
    MATCH (n { Id: '00Q1I000001xNBdUAM' })
    DETACH DELETE n