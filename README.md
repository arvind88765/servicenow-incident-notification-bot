# 🚨 ServiceNow Incident Notification Bot 🚨

Hey there! 👋 Welcome to the **ServiceNow Incident Notification Bot** project. This is a cool little tool that sends instant Telegram notifications whenever something important happens with your ServiceNow incidents — whether it's a new incident, an update .


## 🧐 What's This About?

This is a simple way to keep track of critical incidents in ServiceNow and get notified instantly via **Telegram**. Imagine you're managing incidents, and you don't want to miss any important updates. Well, this bot will keep you updated right in your Telegram inbox. Whether it's the creation of a new incident, updates you'll get the message! 🚀

## 🔧 Prerequisites 

Before you dive into the setup, here’s what you’ll need:

1. **A ServiceNow account**: You need access to your ServiceNow instance.( am using PDI )
2. **Permissions**: Ensure you have the necessary permissions to create Business Rules and REST messages.
3. **Telegram Bot**: Create a Telegram bot for notifications (don’t worry, we’ll guide you through it 👇).
4. **Chat ID**: You'll need your **Telegram chat ID** to send the message to the correct chat (we’ll show you how to get it!).

## 🤖 How to Set Up the Bot?

Alright, let's get started! Here are the steps to make this bot work:

### 1. Create a Business Rule 🛠️

To trigger the notification when an incident is created or updated, we’ll use **Business Rules**.

- **Go to**: **System Definitions** > **Business Rules** > **New**.
- **Table Name**: Select **Incident** (this is for incident notifications; feel free to choose another table if you're working on something else).
- **When**: Set this to **After Insert** (so it triggers after an incident is created AND when incident is updated).
- **Condition**: Set to blank 
- **Action**: Choose **Send a message to a Telegram bot** when a critical incident is created.

You can also go to the **Advanced** tab and paste a script to handle sending messages to Telegram. Don’t worry, we’ll provide the script in the next steps.

> **Pro Tip**: This is where you set up the logic for your notifications. You can even get fancy and notify different chat IDs based on priority. 💬

### 2. Create Your Telegram Bot 🤖

Now for the fun part — creating your Telegram bot!

1. Open **Telegram** and find **@BotFather** (this is the official bot for creating other bots).
2. Type `/newbot` to create a new bot.
3. Follow the prompts. After you’re done, **BotFather** will give you a **Bot Token**.
4. To get your **chat ID**, use **@WhatChatIDBot**. Start a chat with it and type `/getid` to find your **chat ID** (this is where the bot will send messages).

### 3. Set Up REST Message for Telegram 📨

Now that we’ve got the bot and chat ID, we’ll set up a **REST Message** to send messages.

- **Go to**: **System Web Services** > **REST Message**.
- **Create a New REST Message** with the following details:
  - **Name**: `Telegram Bot Message`
  - **Namespace**: Leave as default.
  - **Endpoint**: `https://api.telegram.org/bot<Your-Bot-Token>/sendMessage`
    - Replace `<Your-Bot-Token>` with the actual bot token you got from **BotFather**.
     - Example : https://api.telegram.org/bot7g25847331:AAGR3LBP7PtCaomy7s30vCrTvGjpO8uhYTY/sendMessage

Now you’ve got the basic setup for the Telegram bot communication.

### 4. Create a REST Message Step 📝

Next, we need to set up a step for the **REST Message**. Here’s how:

1. Under **REST Message Steps**, click **New**.
2. Configure the step:
  - **Step Name**: `Send Message to Telegram`
  - **HTTP Method**: Select **POST** (since you’re sending data).
  - **End Point**: Example : https://api.telegram.org/bot7625797331:AAGR3LBP7PtCaomy7s39vCrTvGjjOYuhlTY/sendMessage
 

### 5. Save and Test 🎉

Once you've got everything set up, it's time to **Save** your business rule. 

Then, **test it**! Create or update an incident and check if the notification is sent to your Telegram bot.

---

## ✨ Conclusion

And that’s it! 🎉 You’ve now set up an awesome Telegram bot that will keep you updated on all the critical incidents in ServiceNow. Whether an incident is created, updated you’ll know immediately. 🕵️‍♂️

---

## 💡 Extra Tips

- If you want to send different messages for different types of incidents (e.g., critical vs. low priority), you can adjust the **Business Rule** condition.
- You can customize the message format — include the assignee, impact, or even a link to the incident.
- If you have a group chat, just use the **group chat ID** to send the notifications there.

---

### Code Files

- You can **download** the script files and REST message configuration from this repository. They’re ready for you to plug into your ServiceNow instance.

---

Enjoy! 🚀 Let me know if you need help with any part of the process. 😄



## ⚠️ IMPORTANT:
- Remember: The chat_id and bot token in the instructions above are just example values. You need to use your own chat ID and bot token to make this work.

