# Twitter Sentiment Analysis with Logic Apps

In this lab we will create a logic app that triggers on finding feedback from twitter, analyze the tweets sentiments using Azure Cognetive Services and send the results to a slack channel.

## What will you need?
1. Active Azure account portal.azure.com
2. Active twitter account
3. Active slack channel

### Part 1
Create a Text Analytics API in the Azure portal
1. Follow the steps in this [walkthrough](https://docs.microsoft.com/en-us/azure/cognitive-services/cognitive-services-apis-create-account), make sure to select **Text Analytics API**
2. Wait a few minutes for the API keys to get ready. You should see the following message under *Quick Start* tab
![Alt text](./media/keyReady.jpg?raw=true)
3. Take a note of the Account Name, Key and Endpoint. We will use them later:

![Alt text](./media/cognitiveKey.jpg?raw=true)
![Alt text](./media/endpoint.jpg?raw=true)

### Part 2
Now we will create a Logic Apps that triggers on twitter feed, and posts them to a slack channel after a sentiment analysis on the content.

1. From the main Azure menu, choose **Create a resource > Enterprise Integration > Logic App**
![Alt text](./media/create-logic-app.jpg?raw=true)

2. Under Create logic app, provide details about your logic app and click **Create** once done.
![Alt text](./media/create-logic-app-settings.jpg?raw=true)

3. After Azure deploys your app, the Logic Apps Designer opens and shows a page with an introduction video and commonly used triggers. Under **Templates**, choose **When a new tweet is posted**.
![Alt text](./media/choose-logic-app-template.jpg?raw=true)

4. Allow the Logic App to read your twitter feed
[!Alt text](./media/twitter_signin.jpg?raw=true)

5. Set up the trigger to listen for tweets based on a keyword or hashtag. On polling-based triggers, such as the Twitter trigger, the recurrence property determines how often the logic app checks for new items.
![Alt text](./media/twitter.jpg?raw=true)

6. Now we will start analyzing the tweet text. In Logic App Designer, under the trigger, choose **New step**. Find the **Text Analytics** connector and select the **Detect Sentiment** action.
![Alt text](./media/create-text-sentiment-step.JPG?raw=true)

7. Enter the name, key and endpoint you noted in part 1
![Alt text](./media/cognitiveservice-key-setting.JPG?raw=true)

8. Under **Request Body**, select the **Tweet Text** field, which provides the tweet text as input for analysis.
![Alt text](./media/detect-sentiment.JPG?raw=true)

9. After you get the tweet data and insights about the tweet, we will post all into a slack channel. Click on **Next Step** and search for **Slack** and select **Post Messages**. 
You will need to signin to your slack account and allow the logic app to post in your behalf.
![Alt text](./media/slack-signin.JPG?raw=true)

10. Select the slack channel yo post to, and the message text. In this example we will post the tweet sentiment analysis score, the twitter handle and the tweet text.

![Alt text](./media/slack-step.JPG?raw=true)

11. Click on **Save** and **Run**. Tweet with the hashtag you set in step 5, you should see the sentiment score and text in your slack feed.