---
title: ChatrHub Assistant Tutorials

language_tabs: # must be one of https://git.io/vQNgJ

toc_footers:
  - <a href='https://chatrhub.com/signup/index.html'>Sign Up for an Account Here</a>

search: true
---

# Introduction

Welcome to the ChatrHub Assistant Documents! Use the tutorials to familiarize yourself with ChatrHub assistants by building a simple demo.  Use the reference guides to get a deeper understanding of how all the assistant features work.  Finally, use the FAQ if you have a specific question to be answered.

This document is fairly large so make sure you use the document menu and search feature in the left side panel.

The tutorial and reference guide in this document are tailored specifically for building chat assistants and not for usage of the tightly integrated chat.  Some chat information can be found in the FAQ.  Tutorials and reference guide documentation will be arriving soon for the chat.  

If you need programmatic access to your chat and chatbot data see our [API](https://chatrhub.com/api)

# Tutorials

## Hello World

For our first tutorial, we will create a simple assistant that replies with a single response regardless of user input.

After this tutorial your bot should respond like this:

Actor | Message
----------- | -----------
User | Hello Bot
Bot | Hi! I am a bot!

### Open Assistants Tab

Click the “Assistants” tab on the left menu screen.

![Tab Location](https://resource.chatrhub.com/assistant_docs/assistants_tab.jpg)

### Assistant Name

Give your assistant a name.  Here we will name our assistant "Hello World"

<aside class="notice">
Click “Change Bot” then “New Bot” if you already created a bot previously to load up another assistant.
</aside>

![Tab Location](https://resource.chatrhub.com/assistant_docs/bot_name.jpg)

### Open Category

Edit your default category by clicking “Edit” then “Edit Category”

<aside class="notice">
Category definition: A category is a basic building block of logic in your dialog which when triggered, generates a text output based on a users input. (See category in the reference guide)
</aside>

![Tab Location](https://resource.chatrhub.com/assistant_docs/edit_category.jpg)

### Edit Category Name

Give your default category a name.  This is optional, but will organize your assistant.  Here we named our first category “Default Category”

![Tab Location](https://resource.chatrhub.com/assistant_docs/edit_category_name.jpg)

### Add Template

Click “Add template”.

<aside class="notice">
Template definition: A template contains the structure of a response from the AI.  Templates include variations in the response, triggers for when a template should be active and connections to other categories.  (See the template section in the reference guide.)
</aside>

![Tab Location](https://resource.chatrhub.com/assistant_docs/add_template.jpg)

### Edit Template

Click “Add variation”.  Then type in a string you would like the bot to respond with.  Here we typed in “Hi! I am a bot!”

![Tab Location](https://resource.chatrhub.com/assistant_docs/edit_variation.jpg)

### Exit Template

Once you are done editing your template you can click the “X” in the top right hand corner to exit out of the template.

![Tab Location](https://resource.chatrhub.com/assistant_docs/exit_category.jpg)

### Open Test

You just finished your first bot!  Save your bot by first clicking “Save”. Then connect to XMPP by clicking "offline" in the top right hand corner, then "Click to Connect".  Then start testing by clicking "Test".  This will open the test console where you can start communicating with your bot.

![Tab Location](https://resource.chatrhub.com/assistant_docs/open_testing.jpg)

### Test Bot

The test console should be open where you can now start communicating with your bot!

![Tab Location](https://resource.chatrhub.com/assistant_docs/test_bot.jpg)


## Add Triggers

To add complexity to your conversation you need to direct the conversation into different paths.  We do this by using triggers.  Triggers can be made up of goals (Intent of the conversation), patterns (Specific word matches or regular expressions), system_patterns (NLP based searches such as determining whether or not an english name was mentioned), or system_conditions (Ex. Always true, always false, etc.)

Triggers will activate either a template or a category based on criteria setup within them.  They work from top to bottom which means the triggers are evaluated sequentially and the first trigger that is matched will prevent subsequent triggers from being evaluated.

This tutorial expands on the "Hello World" tutorial.  If you are new to building chatbots, start there instead then move to this tutorial.

<aside class="notice">
You can add triggers to a category or templates.
</aside>

After this tutorial your bot should respond like this:

Actor | Message
----------- | -----------
User | I am looking for 5 robots.
Bot | A number was mentioned.
User | I am not going to mention a number.
Bot | ***No response***

### Open Category

Open the category form by clicking "Edit" -> "Edit Category" under your default category.  Edit the category name to "Integer Mentioned".  Also edit the variation under the template to "A number was mentioned."  See the previous tutorial if you do not know how to edit variations or template names.

![Edit Category](https://resource.chatrhub.com/assistant_docs/edit_category.jpg)

### Add Trigger

In the category form, click "Add Trigger" then from the dropdown select sys-integer.

This will be used to determine if an integer was mentioned in the input. For example, you may want to use a trigger like this to determine if a user wants a reservation for a specific number of people.

<aside class="notice">
sys-integer is a system_pattern that will match when a number is mentioned.  See "System Patterns" in the reference guide for a list of all the system patterns and their descriptions.
</aside>

![Add Trigger](https://resource.chatrhub.com/assistant_docs/add_trigger.jpg)

### Test

Click "Save" then "Test" to open the test portal.  You will notice that the assistant will only respond when a number is present in the input.  To ensure the bot will always respond with a message, you need to add a "Catch All" category to your bot.  To do that, see the next tutorial "Catch All"

<aside class="notice">
You MUST click save to ensure the latest dialog data is available before testing.
</aside>

![Test Integer Trigger](https://resource.chatrhub.com/assistant_docs/test_integer_trigger.jpg)

## Catch All

A catch all is not a specific feature within ChatrHub, but instead it is a principal that you should always keep in mind when creating categories.  Because all AI chats are bounded in terms of what conversations it can handle, you need a way to gracefully respond to users when they ask it something the bot is not prepared for.. Thats the job for a "Catch All"

This tutorial expands on the "Add Trigger" tutorial above.  If you are new to building chatbots please start there.

After this tutorial your bot should respond like this:

Actor | Message
----------- | -----------
User | I am looking for 5 robots.
Bot | A number was mentioned.
User | I am not going to mention a number.
Bot | You didn't mention a number.  Please mention one so I can use my triggers!

### Add Category

Click the "Add Category" button to add a category below the "Number Mentioned" category. Notice this will add a category below the current one.  This will be a sibling and not a child to the default category.

Click "Edit" -> "Edit Category" to open up and edit that new category.  You may drag and drop categories as you see fit.

Do not add a trigger to this category.  "Catch Alls" will typically not have a trigger in them.

Name your new category "Catch All"

![Test Integer Trigger](https://resource.chatrhub.com/assistant_docs/add_category.jpg)

### Add Template

Add in a generic message to the template variation saying that the bot can only recognize integers to guide the user through the conversation.  For example: "You Didn't mention a number.  Please mention one so I can use my triggers!"

![Test Integer Trigger](https://resource.chatrhub.com/assistant_docs/add_catch_all.jpg)

### Test

After adding the catch all, test your conversation.  If a user provides an input other than a number then the dialog will send the catch all response.

![Test Integer Trigger](https://resource.chatrhub.com/assistant_docs/test_catch_all.jpg)

## Goals

At this point you are only prepared to direct the conversation based on a specific pattern (Ex. Was a integer mentioned in the input?).  To make the bot more human like, you can utilize goals.  Goals can be thought of as intentions of the conversation.  For example, does the user want to pay a bill or does the user want to make a reservation.

A goal is made up of a list of utterances.  These utterances will be used in future conversations to determine what the user wants to do.

After this tutorial your chat bot should respond like this:

Actor | Message
----------- | -----------
User | I want to test drive a car.
Bot | Looks like you want to test drive a car.  Which one would you like to drive?

### Goals Tab

We will navigate outside of the "Bot" tab into the "Goals" tab.  Once there, click on the "Add Goal" button to add a goal.

![Test Integer Trigger](https://resource.chatrhub.com/assistant_docs/add_goal.jpg)

### Edit Goal

Give your goal a name.  In this case we will create a conversation for a car dealership so we will name it "test_drive".  Note, you may not use spaces so instead use underlines to make it clear.

Give your goal a description so others can understand what the goal is intended to do.

Finally give examples of how a user may ask for a test drive under utterances.  Examples include "Hi I want to test drive a car of yours." or "I am looking for a new car."

The more utterances you provide in goals the better the AI will be able to understand a future conversation.  Make sure the utterances are somewhat different and you cover all of your bases.

![Test Integer Trigger](https://resource.chatrhub.com/assistant_docs/edit_goal.jpg)

### Edit Category/Trigger

Go back to the "Bot" tab and edit your first category.  Rename the category "Test Drive", remove all category triggers if there are any and then re-add the test_drive trigger.

Edit the variation to say. "Looks like you want to test drive one of our cars.  Which one would you like to test drive?"

Add or edit your "Catch All" category's variation to say: "Sorry we can only handle scheduling test drives." (See previous tutorial for more information on catch alls.)

![Test Drive Trigger](https://resource.chatrhub.com/assistant_docs/test_drive_trigger.jpg)

### Test

Test your dialog to make sure that when you ask for a test drive it responds with the variation you added and not the catch all.

<aside class="notice">
Remember, you MUST click save to ensure the latest dialog data is available.
</aside>

![Test Test Drive](https://resource.chatrhub.com/assistant_docs/test_test_drive.jpg)

## Custom Patterns

Custom patterns allow the dialog to recognize when a user is talking about a specific object or noun.  An example of a custom pattern is car_brand.  Within the car_brand pattern are a list of all the possible car brands and all the possible synonyms for each value.  As an example, Ford and Mazda are card brands and Ford Motor Company and Mazda Corporation are its synonyms.

After this tutorial your bot should respond like this:

Actor | Message
----------- | -----------
User | Hi I would like to test drive your cars
Bot | Looks like you want to test drive one of our cars. Which one would you like to test drive?
User | I would like to test drive a Mazda
Bot | Mazda is a good choice.  What time can I schedule the test drive?

### Patterns Tab

Navigate outside of the "Bots" tab and into the "Patterns" tab.  Once there click the "Add Pattern" button.

![Patterns Tab](https://resource.chatrhub.com/assistant_docs/add_pattern.jpg)

### Edit Pattern

Add the name of the pattern.  In this case add car_brand as the name.  Make sure that you do not use spaces, but instead use underscores for the name.

Add a description of the pattern that will make it easy for someone new to understand what it is for.

Click "Add Value" and add "Ford" as a value and "Ford Motor Company" as a Synonym.  Do not add anything for the regexs.  Click "Add Value" again and do the same thing for "Mazda" and "Mazda Corporation"

![Edit Pattern](https://resource.chatrhub.com/assistant_docs/edit_pattern.jpg)

### Add Child Category

Navigate back to the "Bots" tab and add a child category to your "Test Drive" parent category.  Do this by clicking "Edit" -> "Add Child".  Please follow the previous tutorial if you don't know how to setup a parent category that triggers off of a custom test_drive goal.

![Add Child Category](https://resource.chatrhub.com/assistant_docs/add_child_category.jpg)

### Add Ford Trigger

After adding the child category, edit that category and name it "Obtain Car Brand".  Instead of adding the trigger to the category itself, we will be instead adding the pattern trigger to the templates.

Click "Add Template", then under that template click "Add Variation" and type in "Ford is a good choice.  What time can I schedule the test drive?"  Then click "Add Trigger" within that template and add in the car_brand pattern and select "Ford" to the right.

![Add Ford Trigger](https://resource.chatrhub.com/assistant_docs/add_ford_trigger.jpg)

### Add Mazda Trigger

Below the Ford template, click "Add Template" again.

In that template do the same thing as the Ford setup, but instead for Mazda.  Obviously change the variations from "Ford" to "Mazda".

![Add Mazda Trigger](https://resource.chatrhub.com/assistant_docs/add_mazda_trigger.jpg)

### Add Catch All

Below the Mazda template, click "Add Template" again to add a "Catch All" template.

The catch all template will ensure that if a user mentions something other than Mazda or Ford, then the user will be directly as such.  See the "Catch All" tutorial for more information.

### Test

If you followed this tutorial and the previous one, you should be able to have the following conversation:

<aside class="notice">
Play with the second response.  What if you don't mention Ford or Mazda?  In that case your "Catch All" should trigger mentioning something like "We only offer Fords Mazdas."
</aside>

Your network of categories should look like this:

![Test Drive Categories](https://resource.chatrhub.com/assistant_docs/test_drive_categories.jpg)


## Questionnaires + Variables

A questionnaire is a mechanism that gives you the ability to obtain visitor information from their input messages.  The questionnaire form allows you to store specific information into variables such as custom patterns (Ex. car brand), system patterns (Ex. english names), or simply set variables by default.

Variables allow the assistant to "remember" user or dialog information during the conversation and in some cases forever for that visitor.

<aside class="notice">
System variables exist to describe each visitor.  As an example, sys_name is a persistent storage of the visitors name and can be updated during the dialog.  Custom variables only persist during the conversation but can be used in tasks or webhooks (Actions) for future or real time processing respectively.  For a complete list of system variables see "Variables" and "System Variables" in the reference guide.
</aside>

This tutorial is an extension of the previous tutorials.   After this tutorial your bot should respond like below:

Actor | Message
----------- | -----------
User | Hi I would like to test drive your cars
Bot | Looks like you want to test drive one of our cars. Which one would you like to test drive?
User | I would like to test drive a Mazda
Bot | I stored Mazda into the $car_brand variable

### New Variable

Navigate to the "Variables" tab, click "Add variable", then add "brand", finally click save.

This tutorial expands on the previous example.

![Variable Tab](https://resource.chatrhub.com/assistant_docs/new_variable.jpg)

### Open Child category

Under the "Obtain Car Brand" child category, click "edit" -> "edit category".

![Test Integer Trigger](https://resource.chatrhub.com/assistant_docs/edit_car_brand_category.jpg)

### Save Variable

Now we are going to save your custom pattern, "car_brand", to your custom variable, "brand", so that you can use it later to display back to the user, send as a queue task, or send to a custom action (Webhook).

1. In the category form, under "Input / Output" click the "Questionnaire" radio button.

2. Make sure the "Custom" checkbox is clicked.

3. Under the pattern dropdown, select the "car_brand" pattern you created earlier.

4. Add the "brand" variable to the "Save as Variable" dropdown you created earlier.

5. Finally update the "Not Found Template" -> "Variation" to "Sorry we only carry Ford and Mazdas.  Which one would you like to choose from?"

<aside class="notice">
The final step will gracefully handle the situation when a car brand is not mentioned or a car brand that you do not carry is mentioned.  You can also use overrides to give more information during the questionnaire.
</aside>

### Test and Next Steps

The final step is to test your simple car dealership demo.  This chatbot is obviously very simple and needs a lot of refinement.  Please use the next section to get a deeper dive into all the functionality and features of ChatrHub.

# Reference Guides

## Category

Categories represent the basic unit of knowledge in the dialog flow.  All categories consist of an input from the user and an output message back to the user.  The triggers are evaluated for each category from top to bottom in a dialog flow.

Property | Description | Required?
----------- | ----------- | -----------
Triggers | Determines when a category is active. Triggers are not required.  See triggers to get more information. | No
Require All Triggers | By default only 1 trigger needs to match to activate a category.  If "Require all Triggers" is selected then all triggers in the category need to match to activate the category. | Default No
Templates | A template outlines how the chatbot should respond to an incoming message.  Multiple templates can be used in a single category.  The template triggers will be evaluated from top to bottom.  See templates below to get more information.  | Yes
I/O Questionnaire | Get information from your users and store that information into variables.  See the questionnaire section below to get more information. | No
I/O Action | When an action needs to be performed such as updating a users account, you can queue a task using "Send to Queue", update backend systems in real time using webhooks, or schedule time dynamically and automatically on a calendar. See the action section below to get more information. | No

![Category Reference](https://resource.chatrhub.com/assistant_docs/category_reference.jpg)

## Trigger

Triggers can be added to categories or templates and they determine when to activate that part of the conversation.  Triggers can consist of goals, patterns, system patterns, conditions, or variables.

Multiple triggers can be added to either categories or templates.  When multiple categories or templates are present triggers are evaluated from top to bottom.  The first category or template to match the triggers will be evaluated.

![Trigger Reference](https://resource.chatrhub.com/assistant_docs/trigger_reference.jpg)

## Template

Templates contain all the information used to respond back to the user.  It can contain a variety of information which will be used to tailor the response message.  You can use the "Move Up" and "Move Down" buttons to change which template is evaluated first to last.

Templates most importantly contain the variations of ways to respond to a user.  Variables can be injected into the variations by prepending a dollar sign in front of the variable.  As an example: "Hello $name, what can I do for you?" will be converted to "Hello Joe, what can I do for you?." if the variable called *name* has the value of "Joe" in it.

Property | Description | Required?
----------- | ----------- | -----------
Variations | The various ways to respond to a user.  To make the chatbot seem more human, multiple variations of responses can be used to say the same thing differently if the user encounters the same part of the chat conversation multiple times.  See the description above to inject variables into your variations. | One required
Random Variations | When selected, a random variation is selected as the reply message.  When unselected, the variations will be chosen sequentially. | Default false
Triggers | Determine when this template is active. | No
Require All | If selected, all the triggers listed must evaluate to true for the template to be active. | Default False
Fast Forward | If selected, the next level of categories will be evaluated with the same message automatically. | Default False
Connect to Category | Often times, a user will want to move the conversation to a different set of categories.  In that case, this tool can be used to move the user to the new categoires.  As an example, if a user is updating of their billing information, but during that conversation, the user wants get get their account number, you can use this tool to bounce the user around different parts of the conversation. | No
Evaluate Base of Category? | When selected the Connect to Category's templates, questionnaires and actions will be evaluated, however, when not selected, the children of the Connect to Category will be evaluated. | Default false
Safety Driver | When selected, a message will be sent to one or more agents in the chat console (Depending on routing rules setup in the chat settings) which will notify the agent(s) to "watch" the conversation for issues.  The agent will be able to visually see the bot interacting with the visitor in real time and can interject and/or take over the conversation if needed.  If the safety driver / agent does take over the conversation, it can direct it back to the bot for further processing after the problem conversation has been resolved.  | Default false

![Template Reference](https://resource.chatrhub.com/assistant_docs/template_reference.jpg)

## Questionnaire

A questionnaire is always contained within a category and is a mechanism used to obtain information from visitors.  Questionnaires are made up of one or more questions which collects a piece of information from the visitor either in bulk (Ex. My name is Joe Schmo and my phone number is 555-555-555) or one at a time.  The question allows you to store specific information into variables such as custom patterns (Ex. car brand), system patterns (Ex. english names), or simply set variables by default.

Property | Description | Required?
----------- | ----------- | -----------
Custom? | This checkbox will determine if you want to collect a system pattern (Unchecked) such as "sys-english-name" (See system patterns below) or a custom pattern (Checked - See custom pattern below) | Default false
Pattern | Based on the "Custom?" checkbox, you can select either a system or custom pattern.  If this pattern is present in the inbound message it will be stored in the variable you provide. | Yes
Required | If checked, the question will not ask for this pattern specifically. | Default true
Not Found Template | These template variations will be sent to the user if the question cannot obtain the correct information from the user.  See max attempts below. | Yes
Skip Question | If checked and greater than zero, the question will be skipped and the conversation will move on without fulfilling the question. | Default false
Max Attempts | If checked, and the bot asks for a specific question this many times, the "Not Found Template" variations will be sent to the visitor and the conversation will be reset back to the start. | Default 3
Save as Variable | When a pattern is found in the inbound message that specific piece of information (Ex. Restaurant's table number) will be stored in this variable for later use in the conversation. | Yes
Skip if Variable Already Set | If the variable has already been set prior to this questionnaire, this question will be skipped.  This can be useful if for example the user provides all the information up front when it is not asked for specifically. Note, a questionnaire would need to be available at the start of the conversation with non-required patterns to check / store information if the user provided it without being asked. | Default false
Set By Default | You can use this option to set a variable by default automatically regardless of the users input.  You may specify an pattern name in the text field by prepending the pattern name with an @ symbol which will save the value of the last previously identified pattern. (Can be from a trigger or previous questionnaire.) Example \@sys-english-name or \@sys-datetime or \@your_custom_pattern. (If the pattern was not previously evaluated, the variable will be saved as 'Unknown') | Default false
Questionnaire Overrides | These overrides will interject with a template during the questionnaire if the user responds with a message that triggers the override. (See template)  An example of when this would be used is if a user asks what time the store is open when scheduling service. | No
Questionnaire Fail Template | This template will be sent to the visitor when a questionnaire fails to fill a question. (See Max Attempts) | Suggested
Questionnaire Fail to Category | After sending the fail template (See above), instead of resetting the conversation to the beginning instead the conversation is sent to a different part of the conversation as specified by this category dropdown.  The option "Force Reset" is another way of simply resetting the conversation back to the beginning. | Default Reset.

![Trigger Reference](https://resource.chatrhub.com/assistant_docs/questionnaire_reference.jpg)

## Schedule Action

The scheduling action can be created in the "Actions Tab" and applied to a conversation in a category form under "Custom Actions".  The schedule action utilizes google calendar to schedule an event automatically with a user by first collecting the preferred date and time of the appointment, then suggesting date and times based on the current events and open and closed times.  The bot will keep on suggesting times until a date and time can be agreed to by both parties.

Property | Description | Required?
----------- | ----------- | -----------
Action Type | Action type must be "schedule". | Yes
Calendar Provider | The calendar you would like to use when scheduling an appointment automatically.  Currently "google" is the only available calendar provider but more are coming soon. | Yes
Calendar Authorize | This button will give ChatrHub authorization to schedule events on your behalf. | Yes
Event Duration | This field will determine how long the typical session or appointment is. The field is in seconds (Note: 3600 seconds is equivalent to 1 hour) | Yes
Event Summary | This field will used as the event summary in the calendar.  Conversation variables will be replaced with their value.  Use a dollar sign to specify the variable (Example: "Appointment with $full_name".  Remember full_name needs to be setup under the variables tab and needs to be collected during the conversation.) | Yes
Event Location | This field will be used as the event location in the calendar. Conversation variables will be replaced with their value.  Use a dollar sign to specify the variable (Example: "Meet at $checkpoint".  Remember checkpoint needs to be setup under the variables tab and needs to be collected during the conversation.) | Yes
Event Description | This field will be used as the event description in the calendar. Conversation variables will be replaced with their value.  Use a dollar sign to specify the variable (Example: "Call $name at $phone or contact via email at $email".  Remember name, phone and email variables needs to be setup under the variables tab and needs to be collected during the conversation.) | Yes
Additional Attendee | A list of emails that will be added to the calendar event. (Separated by a space)  You can specify multiple emails and even variables that contain emails.  These users will also automatically receive emails when the calendar event is scheduled.  Example: "test@example.com $email" | No
Datetime Variable | The variable used to initially collect the preferred date and time of the appointment during the conversation and prior to scheduling the appointment.  If this variable is not set prior to the scheduling action, an error will be spit back to the end user.  Note: Make sure that when you collect the "Datetime Variable" that you use "Required" in the questionnaire to make sure the variable is set prior to.  (See questionnaire) | Yes
Calendar ID | This identifies the calendar used with the calendar provider.  The default calendar for google is primary | Default: "primary"
Lookaround Range | This value identifies how many seconds around the current time that the bot can use to suggest appointment times.  It defaults to 12 hours.  As an example for restaurants this should be relatively low since someone asking for a dinner reservation shouldn't be suggested a time in the morning and conversely, for a dentists office, this variable should be high since the user won't care if a suggested time is weeks from their preferred time.  The default value is 43200 seconds which is half a day.  | Default: 43200 seconds
Hours | Use this tool to identify when your establishment is open for appointments. The bot will not suggest appointments when you are busy or when you are closed. | Default: Open M-F 9AM to 5PM

![Schedule Action Reference](https://resource.chatrhub.com/assistant_docs/schedule_action_reference.jpg)

## Actions

An action is custom integration to a backend system using webhooks.  Variables can be selected as a mechanism to send information back to these systems.  After the webhook has completed is process, the webhook can send variables back to the dialog.  Both sent and returned variables must be specified beforehand during the creation of the action.

For your convenience, we created a simple Python library which stands up a webservice for your webhook: [chatendpoint](https://github.com/ChatrHub/chatendpoint).

Property | Description | Required?
----------- | ----------- | -----------
Action Name | Description of the action | Yes
Action Type | use "custom" for custom actions | Yes
Http Method | Either "GET" or "POST" depending on you webhook | Default "GET"
Endpoint URI | The web address of your endpoint | Yes
Variables | Variables that should be sent to the webservice.  These variables will be sent as a JSON payload if using "POST" or as parameters if using "GET" | No
Return Variables | Variables that should be returned form the webserice.  These variables should be sent back as a JSON payload. | No

## System Actions

System actions are pre-defined actions that can be used to either send tasks to a queue for later processing or to forcefully transfer a visitor to an agent.

System actions are defined by default and are used in categories under "Input / Output" -> "Action" radio button.

Property | Description
----------- | -----------
sys-transfer-to-human | This action will transfer a visitor to a human agent.  If group matching is turned on in the chat settings, the visitor will be transferred to the respective agents in that group.  If no humans are available, the system will present an offline form.  This system action is DIFFERENT from **safety-driver** in that it requires the visitor be transferred at that point and will stop the conversation with an offline form if no human is available.  (The user will be prompted to send an email to a predefined agent when no humans are available) See **safety-driver** in the templates section for a more subtle way of transferring to an agent.
sys-send-queue | This action will create a task in the backend queuing system for later processing.  All variables will be collected and sent to this queue.


## System Patterns

System patterns utilize the latest in Natural Language Processing to identify and store various pieces of information from the user's input messages.   An example of a system pattern is **sys-datetime** which will identify a date and time from the input message and format it into a date-time object.

A system pattern can be used in the following scenarios:

1. In a questionnaire to pull out information from the users message. *Most common usage*
1. In a trigger. For example, to activate a category or template if a name is mentioned.
2. In the template variation (Output message) by using the @ symbol in front of the pattern.

See a list of all the system patterns and a description of how they can be used below:

System Pattern | Identifies and Extracts | Example
----------- | ----------- | -----------
sys-english-name | Human name | Hi my name is **joe johnson**
sys-english-organization | Name of an organization | I work for **Walmart** and I love it!
sys-address | Postal address | My address is **555 N Pkwy Minneapolis MN**.  Thanks!
sys-us-phone | Phone number | You can reach me at **555123-1234**
sys-email | Email | You can reach me at **test@example.com** okay?
sys-credit-card | Credit Card | Yeah my credit card is **4242-4242-4242-4242**.  Thanks!
sys-number | Integer or floating number | I would like **2.5** ounces of that stuff!
sys-integer | Integer only | I would like a table for **two** or maybe **3**
sys-decimal | Floating number only | I would like **2.5** of those but not 3
sys-datetime | Datetime or relative datetime | I can come in **tomorrow morning at 6am**
sys-datetime-time | Unstrict date.  Can be activated by a simple integer.  Should be used when asking for date and time specifically | Lets do **5** or maybe **tomorrow at 3:45**
sys-date | Will trigger on a date only | Lets do **tomorrow** or maybe **Monday**
sys-time | Time of day | I can do **4:45PM**

When you use a simple system pattern such as *sys-integer* or *sys-datetime-time* (Simple meaning it can be triggered by an integer only, compared to *sys-datetime* which is more complex), it is better to include these at the bottom of a questionnaire to allow the more complex patterns to be matched first before the simple ones.  This will ensure, for example, that the number in a *sys-datetime* will not mistakenly trigger a *sys-integer*

***Correct Setup:***

Setup | Input Message | *sys-datetime* | *sys-integer*
----------- | ----------- | ----------- | -----------
*sys-datetime* first then *sys-integer* in a questionnaire | "**Tomorrow at 3** for a table of **5**. thanks" | Tomorrow at 3 | 5

***Incorrect Setup:***

Setup | Input Message | *sys-datetime* | *sys-integer*
----------- | ----------- | ----------- | -----------
*sys-integer* first then *sys-datetime* in a questionnaire | "**Tomorrow** at **3** for a table of 5. thanks" | Tomorrow | 3

## Patterns

Patterns are used to identify objects within a conversation such as a brand of car or style of shoe.  They are different from system patterns because they do not use NLP, but instead simply match the pattern value and pattern synonyms, or use regular expressions to make the match.

To create a pattern, go to the Patterns tab under Assistants, then fill out the resulting form:

Property | Description | Required?
----------- | ----------- | -----------
Name | Name of the pattern such as "car_brand".  Do not use spaces. Instead replace spaces with underscores. | Yes
Description | Describe the pattern you are creating | No
Correct Spelling | Use this option to correct spelling on input messages before processing.  This is helpful when trying to identify a miss-spelled pattern.  For example "Frod" instead of "Ford".  Do not use this option on patterns that contain short values / synonyms as it will incorrectly identify patterns as it will try to correct the spelling incorrectly. | Default False
Add Value | Button to add a value to your pattern.  | One required
Value | The name of the value such as "Ford"
Synonyms | Different ways to mention the value such as "Ford Motor Company" | No
Regexs | You can also use regular expressions to identify the pattern. | No

![Patterns Reference](https://resource.chatrhub.com/assistant_docs/patterns_reference.jpg)

## Goals

Goals can be thought of as intentions of the conversation.  For example, does the user want to pay a bill or does the user want to make a reservation?  A goal will determine what the user wants to do.

A goal is made up of utterances or examples of what the conversation might contain.  These utterances are used to identify the goal of future conversations.

Goals are used in triggers to activate a category when mentioned.  Lets say you create a category that has a questionnaire which will request the address from the visitor.  You would use a "Visitor wants to change address" goal to trigger that category.

Goals have the following properties:

Property | Description | Required?
----------- | ----------- | -----------
Name | Name of the goal. Do not use spaces, but instead replace with underscores | Yes
Description | Describe what the purpose of this goal is | No
Utterances | Examples of how a user might request this intent.  As an example: "Hi I want to update my address" or "My address is wrong!" would be good examples of utterances for a "Update Address" goal. | Yes

![Goals Reference](https://resource.chatrhub.com/assistant_docs/goals_reference.jpg)

## Variables

Variables can be thought of as storage bins for various pieces of information that you collect throughout the conversation.  Essentially they allow the bot to "remember" what happened during the conversation and what information it was given.

Variables must first be created in the "Variables Tab" in the assistants portal.  They are different from *System Variables* (See system variables section) because they need to be explicitly created.

The only way to update a variable during the conversation is to include them in a questionnaire.  (See the Questionnaire section)

Variables can be used to:

1. Display its value back to the user  (See templates section)
2. Send its value to a backend server (See custom actions section)
3. Send to a task queue (See actions section)

![Variables Reference](https://resource.chatrhub.com/assistant_docs/variables_reference.jpg)

## System Variables

System variables are much like normal variables (See variables section), but instead of explicitly creating them in the variables tab, they are already created for you.  They can be updated during the dialog as well in a questionnaire (See questionnaire section)

System variables store persistent information about the visitor.  They include such things as a visitors name, email, phone, address, etc.

See below for a list of all the system variables:

System Variable | Description
----------- | -----------
sys_email | Visitor's email address
sys_ip_address | The last known ip address for this visitor (Only applicable to website visitors)
sys_phone | Visitor's phone number
sys_company_name | Visitor's company name
sys_city | Visitor's city
sys_state | Visitor's state (ISO short code)  Ex. "MN"
sys_zip_code | Visitor's zip code
sys_current_url | Visitor's current url
sys_referrer_url | Visitor's last known referrer url
sys_country | Visitor's country (ISO Short Code) Ex. "US"
sys_name | Visitor's name

# FAQ

## General

Q: Who can I email for help?
A: You may email admin@chatrhub.com for help.

Q: Is there a support phone number I can call for help?
A: You may call 866-239-5842 for assistance.

Q: How do I upgrade my account?
A: To upgrade your account, click the orange “Upgrade” button at the top of the portal. You may also upgrade by clicking “Settings” on the left side menu, followed by “Billing.”  If you would like to inquire about an enterprise plan please contact us at admin@chatrhub.com

Q: How do I reset my password?
A: On the Login page, press “Forgot Password?” and enter the email you signed up with. Click the link in your email to set up a new password.

## Talk

Q: How do I connect to ChatrHub and go online?
A: To change your status from “Offline” to “Available,” either press the green “Click Here to Connect” button that is displayed in the chat screen on the “Talk” tab, or click the red “Offline” button in the upper right hand side of the screen and select “Click Here to Connect.”

Q: How do I know if a Visitor is available for chat?
A: If a Visitor is available to chat, the Visitor’s name (listed on the right hand side of the screen) will appear with a green halo and “Online” will be displayed below the Visitor’s name. If a Visitor is not available to chat, the Visitor will have an orange halo and it will say “Offline” beneath it.

Q: How do I search for a Visitor?
A: To search for a visitor, click the “Talk” button on the left side menu. Search for a visitor in the “Search” field in the upper right hand side of the screen.

Q: How do I attach and send a file or image from ChatrHub to a Visitor?
A: To attach a file or image, click the “Talk” button on the left side menu. Select the visitor to whom you wish to send the Patterns, and click the blue icon of a sheet of paper in the lower left hand corner of the chat window. Select “Choose File” to browse your computer for the Pattern you would like to send. Once you have selected the image, click the green “Send Image” button.

Q: How do I hide myself so I am not visible as an online Agent (but without disconnecting from ChatrHub)?
A: To change your status from “Available” to “Hidden,” click the green “Available” button in the upper right hand side of the portal. Select the “Click to Hide” button to make yourself unavailable.

Q: How do I disconnect from ChatrHub and go offline?
A: To change your status from “Available” to “Offline,” click the green “Available” button in the upper right hand side of the portal. Select the “Click to Disconnect” button to go offline.

## Agents

Q: How do Agents work?
A: Agents are members of your company with ChatrHub accounts. They have access to the portal and are able to talk with Visitors.

Q: How do I add a new company Agent?
A: To add a new company Agent, select “Agents” from the left side menu. Click the blue “Add Agent” button and complete the required fields. Input the individual’s full name, e-mail address, role (Agent, Supervisor, or Administrator), and Assistant Task selections. See the descriptions of the Assistant Tasks for details. Also, after you have invited a new Agent to join the platform, you have the option to add the Agent to a pre-created Group.

Q: How are the three Agent roles differentiated (Agent, Supervisor, and Administrator)?
A: An Agent can chat. However, he or she cannot update settings, add agents, or view transcripts. A Supervisor can chat, update/add users, and view all reporting. However, he or she cannot update settings. An Administrator can chat, update/add users, view all reporting, and update all settings.

Q: How do I choose or edit the role of an Agent?
A: You will select an Agent’s role when you add a new Agent to the system. To edit the role of an existing Agent, go to the “Agents” tab on the left side menu and select the name of the Agent whose role you wish to edit. Make your selection and click the blue “Update” button at the bottom of the window.

Q: How do I choose or edit Assistant Tasks for an Agent?
A: You will select an Agent’s Assistant Tasks when you add a new Agent to the system. To edit the Assistant Tasks for an existing Agent, go to the “Agents” tab on the left side menu and select the name of the Agent whose Tasks you wish to edit. Make your selections and click the blue “Update” button at the bottom of the window.

Q: How do I view which company Agents are available to talk with Visitors?
A: To view online company Agents, click the “Talk” tab on the left-side menu. Look at the right side of the screen to see the “Company Agents” section. If the list is hidden, click “Show.” Here, you will see company Agents (if any) and whether they are online.

Q: How do I delete an existing Agent?
A: To delete an existing company Agent, select “Agents” from the left side menu. Click the name of the Agent you wish to delete, and select the red “Delete Agent” button in the lower left hand side of the window.

Q: How do Groups work?
A: To edit Groups, click the “Agents” tab on the left-side menu. Then, click the “Groups” tab on the top of the window. Click “Add Group.” Here, you may create Agent groups that determine how incoming conversations are routed. You may create groups based on phone numbers; company name; city; state; zip code; current URL; referrer URL; and/or email. These factors may be based on partial or complete matches, depending upon how you input the information. For instance, you may route conversations based upon phone number area code and referral URL.

Q: What are the benefits of creating Groups?
A: Groups are beneficial because they allow you to set routing rules for conversations. You may create groups to be as specific as you would like. For example, groups may establish rules for conversations to be routed to either Sales or Service agents, based upon current URL. Alternatively, you may have conversations routed based on very specific rules. There may a certain agent group created to handle conversations from visitors viewing a specific piece of merchandise on your e-commerce site, who live in Chicago, IL, who were referred to your page by Campaign XYZ, and who lives in zip code 60602.

Q: How do I create a new Group?
A: To create a new Group, click the “Agents” tab on the left side menu. Select the “Groups” tab on the upper left hand side of the page. Click the blue “Add Group” button on upper right hand side of the screen. Create a Group Name, and then choose which of the Matches you would like to institute for the Group (Phone, Company, City, State, Zip Code, Current URL, Referrer URL, and/or E-Mail). See the descriptions for details about each of the Match options. When you have made your selections, click the blue “Update” button in the bottom right hand corner of the window.

Q: How do I edit an existing group?
A: To edit an existing Group, click the “Agents” tab on the left side menu. Select the “Groups” tab on the upper left hand side of the page. Locate the Group you wish to update, and click the “Edit/View” button the right of the group name. Make your selections, and click the blue “Update” button in the bottom right hand corner of the window. To delete an existing Group, click the “Agents” tab on the left side menu. Select the “Groups” tab on the upper left hand side of the page. Locate the Group you wish to delete, and click the “Edit/View” button the right of the group name. Select the red “Delete Group” in the bottom left hand corner of the window.

## Visitors

Q: How do I add a new Visitor to the ChatrHub system?
A: To add a new visitor to the system, click the “Visitors” tab on the left side menu. Select the blue “New Visitor” button in the upper right hand corner of the screen. Complete the desired fields Name, E-Mail, Phone Number, Company Name, Street Address, City, State, and Zip Code), and click the blue “Create” button in the bottom right hand corner of the window.

Q: How do I search Visitors using filters?
A: To search your Visitors using filters, click the “Visitors” tab on the left side menu. Click “Add Filter,” and choose your desired search filter (Name, Email, Phone Number, Company Name, State, City, Zip Code, IP Address, and/or Visitor ID).

Q: Can I employ multiple filters at one time?
A: Yes, you may employ multiple search filters at once. To do so, simply select a filter and then click “Add Filter.” To remove any filter, click the “X” next to the filter after it has been applied.

Q: How do I update details for an existing Visitor?
A: To update the details for an existing Visitor, click the “Visitors” tab on the left-side menu. Locate the Visitor whose details you would like to update. Then, click the “View/Edit Visitor” to the right of the Visitor’s information. Edit the details, and click “Update.”

## Assistants

### General

Q: What are Assistants?
A: Think of Assistants as “employees” whose AI you train to interact with your customers. Assistants can be as simple or complex as you would like.

Q: How does the system use logic?
A: See the tutorial and reference guides in this document to get a good understanding of how it all works.

Q: How do I name my Assistant/Dialog?
A: You may name your Assistant/Dialog however you wish. The chat name is the name that web Visitors will see when interacting with your chatbot.

Q: Do you have Assistant templates I can use?
A: Yes. When you create a new ChatrHub account, you will have the opportunity to apply certain pre-built Dialog templates. If you choose to use one, you may have the choice to decide whether or not you would like to include some Categories (depending upon the template designer’s preferences). Once you add the template to the account, you may go in and make edits if desired.

Q: How do I make my Assistant seem more human?
A: A great way to make Assistants seem more human is to add multiple variations to each template. This way, the Assistant does not reply the same way to every question. It is best to thoroughly test and check your Assistant and make edits to increase the “natural” feel.

Q: How do I save changes?
A: To save changes, click the “Save” button at the top of the “Assistants” tab. When you click “Save,” the model will be updated with new changes. When the model is finished updating, it will say “Models Complete” in green text in the upper right hand corner of the page.

Q: How do I test my Assistant?
A: To test your Assistant, click the “Test” button at the top of the “Assistants” tab. When you click “Test,” a new window will popup in which you can test out your Assistant. Interact with your Assistant as though you are a visitor. To simulate a new Visitor on your site (and to test automated initial outbound messages start conditions), enter the command: “start_conversation !%!admin”. Note that you must be online in order to test an Assistant. If you are offline, click the red “Offline” button along the top right of the screen and select “Click to Connect.”

Q: How do I delete a Category, Goal, Pattern, etc.?
A: To delete a Category, go to the “Dialogs” tab on the “Assistants” page. Click the blue “Edit” button on the right side of the Category. Then, choose “Delete Category.” To delete a Goal, go to the “Goals” tab on the “Assistants” page and click “Edit/View” next to the Goal you would like to delete. Then, delete individual examples using the red trash can icon to the right of the example or, to delete the entire Goal, click the “Delete Goal” button at the bottom of the window. To delete a Pattern, go to the “Patterns” tab on the “Assistants” page and click “Edit/View” next to the Pattern you would like to delete. To delete individual Pattern examples, use the red trash can icon to the right of the Pattern. To delete an entire value (including all Patterns beneath that value), click the “Delete Value” button. To delete an entire Pattern, including all examples, click the “Delete Pattern” button at the bottom of the window. To delete an Action, go to the “Actions” tab on the “Assistants” page and click “Edit/View” next to the Action you would like to delete. Click “Delete Action” at the bottom of the window. To delete a Variable, go to the “Variables” tab on the “Assistants” page. Click the red trash can icon at the right of the Variable you wish to delete.

### Dialogs

Q: What are Dialogs?
A: Dialogs define the structure and flow of a conversation. They are constructed from a network of Categories that contain, at a minimum, a trigger and a response. In a conversation, each Dialog will appear as an Agent.

Q: How do I add a new Dialog?
A: To add a new Dialog and build from scratch, go to the “Assistants” tab on the left hand side menu. Type the name of your Dialog into the field to the left of the blue “Change Dialog” button. You may edit this name at any time. Click the light blue “Save” button to create the new Dialog. To add a new Dialog using a template, select the template from the options after you create a new account. If you want to add a Dialog template after you already created a new account, contact ChatrHub at admin@chatrhub.com or 866-239-5842.

Q: How many Dialogs should I create?
A: Dialogs are designed to work on the basis of one dialog per company.

Q: How do I edit a Dialog?
A: To edit a Dialog, simply select the Dialog on the “Assistants” tab and edit as desired.

Q: How do different Dialogs interact?
A: Different Dialogs do not interact. When a conversation is in one Dialog, it should not switch to another. Remember, however, that there should only be one Dialog per company.

Q: How do I collapse or expand my Dialogs?
A: To collapse or expand your Dialogs, click the “Assistants” tab on the left hand side of the screen. Choose the blue “Collapse” or “Expand” buttons. The purpose of these buttons is to make viewing and working with your dialogs easier. Collapsing or expanding dialogs does not impact the functionality of the Dialogs in the system.

Q: How do I switch from one Dialog to another?
A: Although you will typically have only one Dialog, to switch from one Dialog to another, go to the “Assistants” tab on the left side menu. Then click “Dialogs” from the top menu. Click the blue “Change Dialog” button and select the desired Dialog name from the drop down menu.

### Categories

Q: How do Categories work?
A: Categories are the basic building block of Dialogs. To add a new Category, click the light blue “Add Category” button. Click “Edit” at the right side and add content to your Category. You have now created what is called a “Parent Category.”

Q: What are Child Categories?
A: Child Categories are Categories beneath a Parent Category.

Q: What are Sibling Categories?
A: Sibling Categories are different Categories at the same layer.

Q: What are Category Triggers?
A: Category Triggers may be comprised of Goals, Patterns, Conditions, and/or Variables. Category Triggers signal a Category to fire.

Q: Can I stack multiple Triggers? How does this work?
A: Yes. You may include multiple triggers within one Category or Template. You may set all of the Category triggers to be required in order for the Category to fire, or you may select set it so that any one of the triggers fires a Category.

Q: What are Templates?
A: Templates forms that contain information about how to reply to a visitor. You may set different triggers within each.

Q: What are Variation Responses?
A: Variation Templates are different responses to the same Category response. For example, you could set “What’s your name?” “Do you mind sharing your name?” and “Can I please get your name?” as three variation responses. You may set these to fire in a random order, or you may set them to fire in the order they are listed in the system.

Q: How do Questionnaires work?
A: Questionnaires serve to collect information from a web visitor. Examples of information to collect via Questionnaire are Name, Email, Phone Number, Appointment Date and Time, Budget, Car Make, Car Model, Car Color, New or Used, etc.

Q: What does “Update Visitor Info” mean?
A: “Update Visitor Info” is a Questionnaire option. Select this if you want to update the “Visitors” data with the information collected in this question. For example, name, email, and phone number are good options of info to update visitor info with. Appointment date and time and budget, however, are not good options since this info may change from time to time within the same person.

Q: What are Questionnaire Fail Responses?
A: A Questionnaire Fail Response is the message that sends if a web Visitor does not complete the Questionnaire within the specified requirements.

Q: When do Jump To’s come into play?
A: Jump To’s allow you to set your Assistant to jump from Category to Category. If a certain Category is reached and a “Jump To” is set, then the visitor will be jumped to the specified Category.

### Goals

Q: What are Goals?
A: Goals are inquiries or questions a web visitor may have. It is helpful to think of these as type of conversations or initial messages. Please note that the system creates an AI model for each Goal based on the examples provided.

Q: How do I add a new Goal?
A: To add a new Goal, go to the “Assistants” tab and click the “Goals” tab along the top menu. Click “Add Goal.” Create a name for the Goal using only letters, numbers, and/or underscores. Make sure the name is identifying and clear. Next, add a description for the Goal. Now, add as many examples as possible of ways that a web visitor may signal this Goal.

Q: What is an example of content that should not be added as a Goal?
A: Content such as “Model Number” would not work well as a Goal. Because this consists of specific information, it works better as a Pattern, where the system looks just to match the term and not the concept.

### Patterns

Q: What are Patterns?
A: Patterns are specific terms or phrases that may serve as a Category trigger or be included in a Questionnaire. Patterns are unlike Goals in that an AI model is not created based on the values or synonyms within a Pattern. Patterns are objects within the conversation. An example of a Pattern is “Car Brand” which can be broken down into values such as “Ford,” “Volvo, “Chevy,” etc.

Q: How do I add new Patterns?
A: To add a new Pattern, go to the “Assistants” tab and click the “Patterns” tab along the top menu. Click “Add Pattern.” Create a name for the Pattern using only letters, numbers, and/or underscores. Make sure the name is identifying and clear. Next, add a description for the Pattern. Select whether you would like Fuzzy Match on or off. When fuzzy match is enabled (checked), words similar to the value and its synonyms will be matched. This may be useful if a visitor misspells a word. It is not good, however, for short Pattern values or synonyms. Now, add one or more values. For each value, add synonyms if desired. An example of two values within a single Pattern are “Yes” and “No.” Synonyms beneath “Yes” could include “Yeah,” “Yup,” “Okay,” “Sure,” etc. Synonyms beneath “No” could include “Nah,” “Nope,” “Never,” etc. Fuzzy match should not be turned on for this Pattern.
Another option within Patterns is regular expressions (regex). This is a code that signals a Pattern. You may contact ChatrHub at admin@chatrhub.com or 866-239-5842 for information on how to create a regex. This is helpful when there are many values that you would like included within a specific Pattern – and when a pattern exists amongst these values. For example, it is helpful to create a regex for a car parts inventory list with 2,000+ different parts numbers.

Q: What is an example of content that should not be added as a Pattern?
A: An example of content that should not be added as a Pattern is “Where are you located?” or “I’m interested in scheduling a demo.” Because there are many ways that a web visitor could initiate these topics, these instances are better suited for Goals. Again, Goals vary from Patterns because models are created for Goals while, with Patterns, the system just looks for a keyword match.

### Actions

Q: What are Actions?
A: Actions are pre-built or custom measures that you would like the Assistant to take. For example, you may build out a Custom Action that allows the ChatrHub system to connect with your backend database. This is helpful in providing real-time inventory or account information to web Visitors. There are two pre-built Actions in the ChatrHub system. One is the “Transfer to a Human” command. This transfers the web visitor to a human (when available). The other pre-built action is the Google Calendar integration. This allows you to integrate the ChatrHub system with a Google Calendar. In the Actions tab, you will select your preferences. Then, if you add this Action to a Category, the Assistant can help the visitor to schedule an appointment with you and automatically create the invite based upon your hours, availability, etc.

Q: How do I add a new Action?
A: To add a new Action, go to the “Assistants” tab and click the “actions” tab along the top menu. Click “Add Action.” Transfer to a Human system action is pre-programmed, so it will always appear as an action option within Categories. You can’t edit this system action in the “Actions” tab. You can, however, set the “Schedule” system action or custom actions. When you click “Add Action,” the form will default to the schedule action type. Select “custom” from the action type dropdown to change this.

Q: What are System Actions?
A: System Actions are pre-built Actions. These are Transfer to a Human (cannot edit details of this in the Actions tab) and Schedule (set this up in the Actions tab). Any other actions are considered Custom Actions.

Q: How do I create a Custom Action?
A: Contact ChatrHub at admin@chatrhub.com or 866-239-5842 for information specific to your situation.

Q: How do I send Visitor information to the Queue?
A: To send Visitor information collected in a Questionnaire to the Task queue, select “Send to Queue” in a Category at the end of the conversation. Depending upon settings, Agent(s) may receive email notification of new queue Tasks.

Q: How do I transfer the conversation to an Agent from the Assistant?
A: To transfer the conversation to an Agent from the Assistant, create the option in a Category for the System Action “Transfer to Agent.” If this triggers, it will pass the conversation from the Assistant to an Agent, if available.

### Variables

Q: What are Variables?
A: Think of Variables like drawers in which you can store visitor data. For example, it is helpful to create Variables for information such as name, phone number, email, and demo date. Only letters, numbers, and underscores are allowed. Variables contain any type of custom information that is obtained from the conversation and that subsequently can be used in the Assistant’s message or to update visitor information and internal systems.

Q: How do I add a new Variable?
A: To add a new Variable, go to the “Assistants” tab and click the “Variables” tab along the top menu. Click “Add Variable” at the bottom of the page. Navigate back to the “Dialog” tab and click “Save Assistant” often.

Q: How do I teach the Assistant to use information provided by the web Visitor at later points in the conversation?
A: To use information provided by the web Visitor earlier in a conversation at a later point in the conversation (or in a future conversation with the same Visitor), you must use a Questionnaire to collect the information and save it as a Variable. For a regular variable, type “$VariableName” into the response in order for the Assistant to use that information. For example, say the Assistant collected the Visitor’s name earlier in the conversation and saved the name to the variable called “Name”. In order to call the Visitor by name later in the conversation, type “$Name” into the field. Ex: “Thanks for chatting today $Name. Have a great day!” If the Visitor’s name is John, he will receive a message that states, “Thanks for chatting today John. Have a great day!”

## Tasks

Q: What are Operational Tasks?
A: Tasks are “To Do” messages stored in the system. These are created after a conversation in which the System Action “Send to Queue” was set. This sends all variable information from the conversation to the Tasks window. Depending on your settings, you may receive email notification each time a new Task is created. To view these in the portal, login and click “Tasks” on the left side menu. Make sure you are on the “Operational” tab on the top menu. View your Unresolved tasks here. To switch to Resolved tasks, click the “Resolved” tab. When you address a Task, change the status from Unresolved to Resolved using the red button to the right of the Task information.

Q: What are Machine Learning Tasks?
A: Machine Learning Tasks are automatically created by the system. Depending upon your settings, you may receive email notification of these Tasks. They ask that you provide information to the system to strengthen the machine learning capabilities.

## Reports

Q: How do I view Reports?
A: To view a report, click “Report” on the left-side menu. Here, you may filter by dates and view information such as chat reviews and ratings, total chats, missed chats, etc.

Q: How do I adjust the date range on Reports?
A: To adjust the date range, click the gray field in the upper right hand corner of the “Reports” window. Choose one of the pre-set date options (Today, Yesterday, Last 7 Days, This Month, Last Month) or select a Custom Range. Then, hit the green “Apply” button to adjust the date range.

## Transcriptions

Q: How do I view Transcriptions of conversations?
A: To view Transcriptions of conversations, click “Transcriptions” on the left side menu. Then, click “View Transcription” to read the conversation.

Q: Can I apply filters to Transcriptions?
A: Yes. To do so, click “Transcriptions” on the left side menu. Then, click “Add Filter” and make your selection. Note that you can stack filters on top of each other. To delete a filter, click the “X” to the right of the filter name.

## Account Settings

Q: How do I integrate ChatrHub with Salesforce?
A: To integrate ChatrHub with Salesforce, click “Settings” on the left side menu. Then, click “Salesforce” under “Integrations.” Follow the prompts to complete the integration.

Q: How do I integrate ChatrHub with RingCentral?
A: To integrate ChatrHub with Salesforce, click “Settings” on the left side menu. Then, click “RingCentral” under “Integrations.” Follow the prompts to complete the integration.

Q: How do I integrate ChatrHub with Twilio?
A: To integrate ChatrHub with Salesforce, click “Settings” on the left side menu. Then, click “Twilio” under “Integrations.” Choose your settings, and follow the prompts to complete the integration.

Q: How do I update my Appearance settings?
A: To update your Appearance settings, click “Settings” on the left side menu. Then, click “Appearances,” and make your selections.

Q: How do I update my Behavior settings?
A: To update your Behavior settings, click “Settings” on the left side menu. Then, click “Behavior,”and make your selections.

Q: How do I update my Titles and Headers settings?
A: To update your Titles and Headers settings, click “Settings” on the left side menu. Then, click “Titles and Headers,” and make your selections.

Q: How do I access my mobile settings?
A: To access your mobile settings information, click “Settings” on the left side menu. Then, click “Mobile,” and make your selections.

Q: How do I update my billing settings?
A: To update your Billing settings, click “Settings” on the left side menu. Then, click “Billing,” and make your selections.

## Individual Settings

Q: How do I update my profile image?
A: To update your profile image, you may click on your username in the upper right hand corner of the portal. Click “choose file,” select the image you want to use, then click “Upload.” Alternatively, you may click “Agents” on the left side menu, select your name, and update your profile photo this way. Depending upon your account access, you may also be able to update other Agents’/Assistants’ profile photos here.

Q: How do I change my chat name?
A: To change your chat name, click on your username in the upper right hand corner of the portal. Change your chat name to the desired name. Alternatively, you may edit your chat name by clicking on “Agents” on the left side menu, selecting your name, and editing your chat name. Depending upon your account access, you may also be able to update other Agents’ chat names here. Additionally, for Assistants, some agents can edit chat names by changing the name of the dialog under the “Assistants” tab on the left side menu.

Q: How do I unsubscribe from emails?
A: To unsubscribe from emails, click on your username in the upper right hand corner of the portal. Click the box next to “Unsubscribe from Emails.”

Q: How do I update my email?
A: To update your email, click on your username in the upper right hand corner of the portal. Change your email as desired. Alternatively, you may edit your email by clicking on “Agents” on the left side menu, selecting your name, and editing your email address. Depending upon your account access, you may also be able to update other Agents’ email addresses here.

Q: How do I log out?
A: To log out, click your username in the upper right hand corner of the portal. At the bottom of the popup window, click “Logout.”

Q: How do I update my username?
A: You cannot update your username. For assistance, please contact ChatrHub at admin@chatrhub.com or 866-239-5842.
