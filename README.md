# How to build a chatbot using Watson
We will be creating a bot to take coffee orders.

## Creating an IBM Cloud Account
1. Go to this link and create an account: https://console.bluemix.net/registration/
2. Or, go to https://console.bluemix.net/ and login if you have an account already and login

## Provisioning a Watson Assistant instance
1. Once logged in, click on `Catalog` in the upper right corner of the screen
2. Search for `Assistant`
3. Under the `Watson` Category, click on `Assistant`
4. Scroll down and make sure `Lite` Plan is selected for the free plan
5. Click `Create`
6. Click on `Launch tool`

## Creating a workspace
1. Once in the tooling, click `Create` to add a new workspace
2. Name it something like `Coffee-bot` and select the desired language

## Building Intents
1. Click `Add intent`
2. Name the new intent `order-drink`
3. Add a description of what the intent will do. For this, let's use "User wants to order a drink."
4. Hit `Enter` to create the intent
5. Start adding a few exaxmples of how a user would order a drink (at least 5 examples are recommended). Let's use the following:
  - i would like to order a coffee please
  - I need some caffeine
  - order espresso
  - a cappuccino would be lovely
  - a latte please
6. Open the `Try it Out` panel by clicking on the speech bubble in the upper right corner. This allows you to test how your bot will respond
7. Wait for the bot to finish training, then type `can I order a coffee`. It should classify the intent as `#order-drink`. Even though you didn't train the intent on this exact sentence, Watson can still understand it.
8. Add a few more intents to make your bot more robust. Try creating the following intents and adding a few examples to each:
  - #see-menu (User wants to see what's on the menu)
  - #greetings (User greets the bot)
  - #thanks (User thanks the bot)

## Building Entities
1. Click on the `Entities` tab at the top of the page
2. Click `Add entity` and add the name `drink`
3. Turn `Fuzzy Matching` on if you want Watson to understand misspellings
4. Add a value `coffee` with the synonym of `cafe`. 
5. Add some additional values that you allow your users to order and any synonyms, for example:
  - espresso
  - cappuccino
  - latte
  - tea
6. Exit the page, and click on `System entities` underneath the `Entities` tab
7. Turn on `@sys-number`

## Building Dialog
1. Click on the `Dialog` tab at the top of the page
2. Click `Create`
3. Click on the `Welcome` node if you would like to change the intro message
4. Click `Add node`, and name it `Greetings`
5. Add your `#greetings` intent as the field for `If bot recognizes`
6. Fill in a response that says something like "Hi! How can I help you today?"
7. Create two more nodes for `#thanks` and `#see-menu` and add responses
8. Create another node and name it `Order Drink`
9. To the right of the name, click on `Customize`
10. Turn on `Slots` and hit `Apply`
11. Add the intent `#order-drink`to `If bot recognizes`
12. Under `Check for`, add the entity `@drink`
13. Under `If not present, ask` add a question like "What would you like to drink?"
14. Click `Add slot`, and add a condition and prompt for `@sys-number`: "How many cups of $drink would you like?"
15. Add in the response, "Ok, I have $number $drink coming right up!"

## Test in Slack
