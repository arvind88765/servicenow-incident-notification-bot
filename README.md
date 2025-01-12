# ServiceNow Incident Notification Bot

This project involves creating a **Telegram bot** that sends notifications when incidents are created, updated, or when an SLA is about to breach. The notifications are sent via ServiceNow's **Business Rules** and **REST Messages**.

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Steps to Configure the Incident Notification Bot](#steps-to-configure-the-incident-notification-bot)
  - [1. Create a Business Rule in ServiceNow](#1-create-a-business-rule-in-servicenow)
  - [2. Create Your Telegram Bot](#2-create-your-telegram-bot)
  - [3. Set Up the REST Message for Telegram](#3-set-up-the-rest-message-for-telegram)
  - [4. Create a REST Message Step](#4-create-a-rest-message-step)
  - [5. Save the Business Rule and Test](#5-save-the-business-rule-and-test)
- [Conclusion](#conclusion)
- [Additional Notes](#additional-notes)

## Overview

This repository demonstrates how to send Telegram notifications using ServiceNow's **Business Rules** and **REST Message** capabilities. The notifications are sent based on incident creation, update events, and SLA breaches.

## Prerequisites

- **ServiceNow instance**: Ensure you have access to ServiceNow and have appropriate permissions to create Business Rules and REST Messages.
- **Telegram bot**: You need to create a Telegram bot and get your `chat_id` to send notifications.

## Steps to Configure the Incident Notification Bot

### 1. Create a Business Rule in ServiceNow

To send notifications to Telegram when an incident is created or updated, you need to set up a **Business Rule**.

- **Navigate to**: **System Definitions** > **Business Rules** > **New**.
- **Table Name**: Select **Incident** (or any other table depending on your project).
- **When**: Set it to **After Insert**.
- **Condition**: Add a condition to check for critical incidents (e.g., `priority = 1`).
  - Example: `priority=1^EQ`
- **Action**: Choose **Send a message to a Telegram bot when a critical incident is created**.

Alternatively, you can go to the **Advanced** tab and paste the script that sends the notification to Telegram.

> **Note**: We will not include the code here directly; it will be in a separate file that you can download.

### 2. Create Your Telegram Bot

To create a Telegram bot:

1. Go to **BotFather** in Telegram.
2. Use the command `/newbot` to create a new bot.
3. After creating the bot, you will receive a **Bot Token** that will be used in your ServiceNow script.
4. To get your **chat ID**, use **@WhatChatIDBot** in Telegram. Send any message, and use the `/getid` command to retrieve your chat ID.

### 3. Set Up the REST Message for Telegram

- **Navigate to**: **System Web Services** > **REST Message**.
- **Create a New REST Message** with the following details:
  - **Name**: Telegram Bot Message
  - **Namespace**: Leave it as default unless you're using custom namespaces.
  - **Endpoint**: `https://api.telegram.org/bot<Your-Bot-Token>/sendMessage`
    - Replace `<Your-Bot-Token>` with your actual bot token.
- Use this URL when configuring the REST Message or HTTP request to send messages to the Telegram bot.

### 4. Create a REST Message Step

1. Under the **REST Message Steps** section, click **New** to create a step.
2. Configure the step as follows:
  - **Step Name**: Send Message to Telegram
  - **HTTP Method**: **POST** (because you're sending data to Telegram).
  - **Request Body**: This is where you will send the JSON payload containing the message you want to send to Telegram.

    Example Request Body (JSON format):

    ```json
    {
      "chat_id": "<Your-Chat-ID>",
      "text": "New Critical Incident Created!\nIncident Number: INC0012345\nDescription: Server Down - Major Impact\nOpened at: 2025-01-12 10:00:00"
    }
    ```

    Explanation of fields:
    - `"chat_id"`: The unique identifier for your chat (e.g., `5486736990`).
    - `"text"`: The message text. You can include dynamic variables from the ServiceNow incident record (e.g., Incident Number, Short Description).

### 5. Save the Business Rule and Test

Once you've completed all the above steps:

- **Save the Business Rule** in ServiceNow.
- **Test** by creating or updating an incident to verify that notifications are successfully sent to your Telegram bot.

---

## Conclusion

By following these steps, you can successfully set up the **ServiceNow Incident Notification Bot** to send alerts to a Telegram bot whenever incidents are created, updated, or when SLA breaches are imminent.

---

## Additional Notes

- Replace all placeholders such as `<Your-Bot-Token>` and `<Your-Chat-ID>` with your actual values.
- You can customize the message format by including more details such as the incident's state, assignee, or impact.
- Make sure that your ServiceNow instance has the required permissions to execute REST messages.

---

### Code Files

- You can download the script file and REST message configurations from the **[GitHub Repository](#)** to integrate the solution in your ServiceNow instance.

---

Feel free to modify this README as needed, and add the download links for any files you wish to share.

