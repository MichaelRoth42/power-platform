---
title: "Use Bot Framework Composer adaptive cards in chatbots"
description: "Use Bot Framework Composer to add Adaptive Cards to your Power Virtual Agents chatbot."
keywords: "composer, adaptive card"
ms.date: 01/06/2022

ms.topic: article
author: iaanw
ms.author: iawilt
manager: shellyha
ms.reviewer: makolomi
ms.custom: "cex"
ms.collection: virtualagent
---

# Example 1 - Show an Adaptive Card in Power Virtual Agents

You can enhance your bot by developing custom dialogs with [Bot Framework Composer](/composer/) and then adding them to your Power Virtual Agents bot.

In this example, you'll learn how to show an Adaptive Card in Power Virtual Agents by using Composer.

Before you begin, ensure you read [Extend your bot with Bot Framework Composer](advanced-bot-framework-composer.md) to understand how Composer integrates with Power Virtual Agents.

> [!IMPORTANT]
> Bot Framework Composer integration is not available to users who only have the [Teams Power Virtual Agents license](requirements-licensing-subscriptions.md). You must have a [trial](sign-up-individual.md) or full Power Virtual Agents license.

## Prerequisites

- [Extend your bot with Bot Framework Composer](advanced-bot-framework-composer.md)
- [Introduction to Bot Framework Composer](/composer/introduction)
- [!INCLUDE [Medical and emergency usage](includes/pva-usage-limitations.md)]

## Show an Adaptive Card

Go to **Topics** in Power Virtual Agents and create a new topic called **Meal delivery options**. Add the following trigger phrases for this new topic:

- what meals can I order
- what meal options do you have
- what dishes do you deliver
- entrees available for delivery

In the **Authoring canvas**, select the default **Message** node. Select the three vertical dots, then select **Delete**.

Select the **Add node** (+) button under the **Trigger phrases** node, and then select **Ask a question**.

For **Ask a question** , enter "What city are you in?".

In the **Identity** list, select **City**.

In **Save response as** , select the variable for city,
For **Name**, enter **user_city**.  For **Usage**, select **Bot (any topic can access)** then select **Save**.

:::image type="content" source="media/Composer_Example1/E1_Dialog2.png" alt-text="Power Virtual Agents variable.":::

Next, we'll instruct the topic, **Meal delivery options**, to display meal choice images that are available in the user’s city. We'll retrieve the images from Bot Framework Composer content.

On the left-hand menu, select **Topics**. Select the down-arrow symbol next to **+ New topic**, and then select **Open in Bot Framework Composer**.

After you open, the Bot Framework Composer project, you'll see the list of all Power Virtual Agents topics in your bot. However, you won't be able to edit these PVA topics. **Recognizer Type** is set to **Default Recognizer**, which is **Power Virtual Agents NLU**.

> [!TIP]
> The **LUIS** service is not supported as a Recognizer for Power Virtual Agents in Composer. The **Default Recognizer** is set to **Power Virtual Agents NLU** instead. You do not need to have an additional subscription to use **Power Virtual Agents NLU** because it is included in your Power Virtual Agents license.

Go to the **Create** tab in Composer and select **Add a dialog** in the dropdown menu:

:::image type="content" source="media/Composer_Example1/E1_Meals_creatNewDialog.png" alt-text="Composer Create tab.":::

Name your new dialog **Meals**. Select **OK** to create a new dialog, **Meals**, in Composer. You will use this **Bot Framework dialog** to display an Adaptive Card.

:::image type="content" source="media/Composer_Example1/E1_Meals_newDialog.png" alt-text="Composer Create tab new dialog.":::

In Composer, go to the **Bot Responses** tab and, in the **Meals** section, select **Show code**.

:::image type="content" source="media\Composer_Example1\E1_Meals_showCode.png" alt-text="Composer show code button.":::

In the code window, copy and paste the following bot response. Then replace the three example image URLs with your own.

```lg
# Chicken()
-Chicken

# Steak()
-Steak

# Tofu()
-Tofu

# SteakImageURL()
-https://www.example.com/steak.jpg

# ChickenImageURL()
-https://www.example.com/chicken.jpg

# TofuImageURL()
-https://www.example.com/tofu.jpg

```

:::image type="content" source="media/Composer_Example1/E1_Meals_BotResponse_data.png" alt-text="Composer Bot Responses tab with strings.":::

Next, add the Adaptive Card by adding the following code to the same window. This Adaptive Card takes a parameter and displays a set of three images based on the image URLs.

````lg
# adaptivecardjson_meals(location)
- ```
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.1",
    "body": [
            {
            "type": "TextBlock",
            "text": "Meal delivery options for ${location}:",
            "size": "Medium",
            "weight": "Bolder"
        },
        {
            "type": "ColumnSet",
            "columns": [
                {
                    "type": "Column",
                    "width": "stretch",
                    "items": [
                        {
                            "type": "Image",
                            "url": "${SteakImageURL()}",
                            "size": "Stretch",
                            "spacing": "Medium",
                            "horizontalAlignment": "Center"
                        }
                    ]
                },
                {
                    "type": "Column",
                    "width": "stretch",
                    "items": [
                        {
                            "type": "Image",
                            "url": "${ChickenImageURL()}",
                            "horizontalAlignment": "Center"
                        }
                    ]
                },
                {
                    "type": "Column",
                    "width": "stretch",
                    "items": [
                        {
                            "type": "Image",
                            "url": "${TofuImageURL()}",
                            "horizontalAlignment": "Center"
                        }
                    ]
                }
            ]
        },
        {
            "type": "ColumnSet",
            "columns": [
                {
                    "type": "Column",
                    "width": "stretch",
                    "items": [
                        {
                            "type": "TextBlock",
                            "text": "${Steak()}",
                            "wrap": true,
                            "horizontalAlignment": "Center"                            
                        }
                    ]
                },
                {
                    "type": "Column",
                    "width": "stretch",
                    "items": [
                        {
                            "type": "TextBlock",
                            "text": "${Chicken()}",
                            "wrap": true,
                            "horizontalAlignment": "Center"
                        }
                    ]
                },
                {
                    "type": "Column",
                    "width": "stretch",
                    "items": [
                        {
                            "type": "TextBlock",
                            "text": "${Tofu()}",
                            "wrap": true,
                            "horizontalAlignment": "Center"
                        }
                    ]
                }
            ]
        }
    ]
}
```
````

:::image type="content" source="media/Composer_Example1/E1_Meals_BotReponse_JSON.png" alt-text="Composer Bot Responses tab - Adaptive Card JSON.":::

Add the **Activity** that will display this Adaptive Card in the Bot Framework dialog to the same window in Composer:

```lg
# AdaptiveCardMeals(location)
[Activity
    Attachments = ${json(adaptivecardjson_meals(location))}
]

```

:::image type="content" source="media/Composer_Example1/E1_Meals_BotResponse_Activity.png" alt-text="Composer Bot Responses tab - Activity.":::

Go back to the **Create** tab in Composer and select the **Meals** dialog. Select **BeginDialog** and add **Send a response** to your dialog. We'll use this node to display the Adaptive Card we have created in the **Bot Responses** tab.

Select the new **Send a response** action to open the **Properties pane**. Under **Bot responses**, select **Show code**. Add the following expression to this window to show the Adaptive Card, and pass the Power Virtual Agents global variable `user_city` as a parameter:

```lg
- ${AdaptiveCardMeals(virtualagent.user_city)}
```

:::image type="content" source="media/Composer_Example1/E1_Meals_AddResponse.png" alt-text="Composer Begin Dialog - add Send a response action.":::

> [!TIP]
> You can [access Power Virtual Agents global variables in Composer](advanced-bot-framework-composer.md#use-and-update-power-virtual-agents-variables-in-bot-framework-composer) by referencing the scope **virtualagent**. For example, **${virtualagent.user_city}** will refer to the value of a variable that was created in the Power Virtual Agents bot.

You're now ready to upload the **Meals** dialog to your Power Virtual Agents bot. Select the **Publish** tab, and then select the checkbox next to your bot. Select **Publish selected bot**. Add an optional comment, and select **Okay** in the confirmation window.

:::image type="content" source="media/Composer_Example1/E1_Meals_Publish.png" alt-text="Composer Publish Example 1 publish.":::

The Composer content will be validated by Power Virtual Agents and a successful publish will be reported in Composer.

[!INCLUDE [Publish Composer](includes/composer-publish-note.md)]

Go to the Power Virtual Agents **Topics** page to see your new Bot Framework content. Your new **Meals** Bot Framework dialog is now shown on the **Topics** page as part of your Power Virtual Agents bot.

:::image type="content" source="media/Composer_Example1/E1_Meals_in_PVA_Topics.png" alt-text="Power Virtual Agents Topics page - new Bot Framework dialog.":::

In Power Virtual Agents, open the **Meal delivery options** topic in the **Authoring canvas**. Under the **Question** node, add a new **Redirect to another topic** node, and select the Bot Framework dialog **Meals** from the list of available topics.

> [!NOTE]
> You can continue building your dialog in Power Virtual Agents after calling a Bot Framework Composer dialog if you wish.

Your Power Virtual Agents topic **Meal delivery options** will call the Bot Framework dialog **Meals** to display an Adaptive Card. Select **Save** to save the changes to your topic.

:::image type="content" source="media/Composer_Example1/E1_MealsDelivery_RedirectToMeals.png" alt-text="Power Virtual Agents - redirect to Bot Framework dialog.":::

To test your changes in Power Virtual Agents, open the **Test pane** and make sure **Track between topics** is turned on. Type in the following text to start your conversation:

- **What meals do you deliver?**

:::image type="content" source="media/Composer_Example1/Example1_cropped.png" alt-text="Power Virtual Agents Example 1 test.":::

[!INCLUDE [Publish Composer](includes/composer-publish-note.md)]

[!INCLUDE[footer-include](includes/footer-banner.md)]
