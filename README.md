# Salesforce Graph Connect

This app allows you to quickly connect your Salesforce objects to Harding Point object graph.  For usage info see: http://www.HardingPoint.com/

Either use a shared instance of this app: https://graphconnect.herokuapp.com

Or deploy your own instance on Heroku:

1. Create a new Connected App in Salesforce:

    1. [Create a Connected App](https://login.salesforce.com/app/mgmt/forceconnectedapps/forceAppEdit.apexp)
        1. Check `Enable OAuth Settings`
        1. Set the `Callback URL` to `http://localhost:9000/_oauth_callback`
        1. In `Available OAuth Scopes` select `Full access (full)` and click `Add`
        1. Save the new Connected App and keep track of the Consumer Key & Consumer Secret for later use
    1. [Create a Custom Setting](https://login.salesforce.com/setup/ui/listCustomSettings.apexp)
        1. Create Salesforce.com Custom Setting `HardingPoint as Hierarchy/Public`
        1. Create New Custom Field in HardingPoint Custom Setting `graphdburl type URL click save` (Leave page open we will change after install)

1. Deploy this app on Heroku: [![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

    1. Choose Heroku App Name
    1. Past Consumer Key & Consumer Secret into install boxes
    1. Go to Heroku Config Vars copy `GRAPHCONNECT_URL`  (Needed in Salesforce)
    
1. Update Salesforce Settings

    1. Update `graphdburl Custom Setting` with `GRAPHCONNECT_URL` from Heroku Config
    1. Edit the Connected App on Salesforce and update the `Callback URL` to be `https://YOUR_APP_NAME.herokuapp.com/_oauth_callback`
