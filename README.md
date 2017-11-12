
This is a project from the Facebook Developer Circle Hackathon on the weekend of November 11-12 created by five people:
- Ian Duke (https://github.com/1andee),
- Harrison Kim (https://github.com/harrisonkimca),
- Rose Wan (https://github.com/rosexw/),
- Jacques Begin (https://github.com/HombreLoco), and
- Stephanie Zeng (https://github.com/stephanie56).

The objective of the hackathon is to produce a bot that responds to customers on Facebook Messenger when asked about different apparel. Smart AI can pick up the greeting, color, size, material, and return recommendations and details back to the customer.

# Instructions

DESCRIPTION

The purpose of the hackathon is to build an application which allows a consumer to get insightful information about a Toronto based company’s Shopify store using Facebook’s Messenger platform. The challenge will encourage participants to leverage the Shopify API to provide rich and meaningful responses to subjective questions, using 3rd party resources to perform natural language processing, machine learning, and sentiment analysis. The challenge will be open to any stack, but a seed project will be provided in Node JS. Participants should form teams of 3 to 5.

CHALLENGE

Candyboxx has a problem. They want their customers to be able to get information about their products easily. In the past, their customers have messaged Candyboxx with questions like:

How much will shipping be for a particular product?
I’m trying to buy clothing for my friend for her birthday, can you recommend something?
I’d like to buy a gift for my wife, what do you recommend?
I’m looking for an outfit in blue, do you have anything that matches?
Candybox is committed to providing their customers with expert recommendations, answers to questions about their products, and insight into fashion trends. Using Facebook’s messenger bot platform and Shopify’s API, the challenge is to create a messenger bot to interact with customers and the Candyboxx store. The bot is expected to let the consumer know what it can help with and should present the consumer with the information they request. You are free to use any additional third party services like wit.ai or api.ai to handle natural language processing or machine learning to make the experience even better.

RULES

To ensure a fun and fair competition, the following rules apply to all participants for the duration of the event:

Each team will consist of between 3 and 5 people. This includes any outside or remote people who will be contributing.
Team submissions consist of two parts.
The project must be committed to a public GitHub repository by 3PM on Sunday, November 12. Use this command to tag the commit that you want the judging panel to review:
git tag -a DevCTorontoHack2017-TEAM## -m "Hackathon submission by TEAM ##"
(Where ## is your team number)
Starting at 3PM, teams will present their project. Presentations will be limited to 5 minutes. If your project is incomplete or your demo is not working, you can present your findings and what your goals were. Don’t stress too much about not finishing; we’ll be judging on many factors, not just a working demo.
Failure to tag your team's final submission by the deadline will result in disqualification. Teams are free to continue working on the project after the deadline but only the commit that is tagged by 3PM on Sunday will be considered.
This is a competition but collaboration and problem solving with other teams is highly encouraged. The main goal is to learn and have fun.
You are not required to use the seed project we provide nor are you required to use the JavaScript stack.
The Developer Circles program and this event exist to foster a community around sharing and learning. Any behaviour that runs counter to that objective will not be tolerated and will result in team disqualification.


This is where the project started from:
# Facebook Developer Circle Toronto Hackathon Seed Project

Follow these steps to get your team's bot configured and off the ground.

> Each team member must create a personal Facebook account and a Facebook developer account [here] (https://developers.facebook.com/)

## Before you begin - team tasks

* Create a Facebook page [here] (https://www.facebook.com/pages/create)
    * Choose Cause or Community as the page type
    * Use this format for the page name: ```Developer Circles Toronto Hack 2017 Team ##```
    * Add a page username using the same format: ```@Developer Circles Toronto Hack 2017 Team ##```
    * Configure your page's button: Add Button > Get in Touch > Send Message
    * Bookmark your page and/or Pin to Favorites so you can find it later
    * Ensure all your team members are page admins
* Add a two-line comment on the [Hackathon Team Submissions thread] (https://www.facebook.com/groups/DevCToronto/search/?query=Hackathon%20Team%20Submissions) with your team's github repo url and page address

## Server Configuration - Part I
> these steps have no dependencies so complete them first
* Update config/default.json
    * "fb_validationToken": "make up a short phrase to use when you validate your webhook in a later step",
    * "sh_shopName": "select the value that was assigned to your team",
    * "sh_apiKey": "select the value that was assigned to your team",
    * "sh_apiPassword": "select the value that was assigned to your team",

## Configure your Facebook application - Part I
> The App Dashboard is the admin panel for all your Facebook Platform integrations. Every app you create contains some unique values which are used to secure the communication channels between your bot, the Messenger Platform and the people who message your page. You must copy these values into your bot's config file.
* Create a Facebook application in the [App Dashboard] (https://developers.facebook.com/apps)
    * Copy the App Secret value from the App Dashboard
* Update config/default.json
    * "fb_appSecret": "the auto generated value for your app in the App Dashboard"
* Add and configure the Messenger product
    * App Dashboard > {Your App} > Add Product > Messenger > Token Generation > Page > {select your team's page}
    * Copy the generated value
* Update config/default.json
    * "fb_pageAccessToken":  "the value generated in and copied from the App Dashboard"

## Start your server and ngrok tunnel
> You must run your server so that the Messenger Platform can verify that your webhook is available
* Run `npm install` from the project root folder to install all dependencies
* Run `npm start` to start the node server
* Run `ngrok http 5000` to get a public URL to your node server. DO NOT CLOSE THIS WINDOW!!!
* Update config/default.json
    * "host_url": "https://{your unique url}.ngrok.io"
    * If you close/restart the ngrok service, update this field with the new URL and restart the node server.
* Restart the node server to ensure that it reads and uses the new host_url config value

## Configure your Facebook application - Part II

* Configure the Webhooks product
    * App Dashboard > {Your App} > Messenger > Webhooks > Setup Webhooks
        * Callback URL:  https://{your unique url}.ngrok.io/webhook
            * If you close/restart the ngrok service, repeat this step with the new URL.
        * Verify token: use the value you defined for the fb_validationToken field in config/default.json
        * Subscription fields: select messages and messaging_postbacks as a minimum
    * App Dashboard > {Your App} > Messenger > Webhooks > Select a Page... > {select your team's page} > Subscribe

## Test your bot
* Open your Facebook page
* Click the Send Message button and tap the Get Started button
* Send a simple text message to your bot
> The message should be echoed back at you
* Send 'help' to your bot
> You should be presented with a message a button
* Tap the 'Get 3 products' button
> You should see a carousel with three cards, one for each product that was returned
