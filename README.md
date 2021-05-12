
# Alexa Audio Skill

Tutorial on how easily you can create an Alexa Skill calling an external audio file to impress your friends and family.
This tutorial is meant to be the easiest and straightforward possible, allowing anyone - even those who don't know how to code! - to create an audio skill. To achieve that, we are going to simplify using Amazon's Alexa Development Console. 

## First Steps

In order to start, you need an Amazon Developer Account. You can create it by clicking [this link](https://www.amazon.com/ap/signin) and logging with your existing Amazon account, if you already have one, or creating a new account. However, it's important to note that to "test" your skill in your device, you should use the same account as your Amazon Alexa.

After logging in, you should access [Alexa Development Console](https://developer.amazon.com/alexa/console/ask), where we are going to create your first skill. 

## Creating a Skill

To create a new skill, it's easy as just clicking on the button `Create Skill`. Give your skill a name and select your default language. 
At the first settings `Choose a model to add to your skill`, leave it as it is (Custom) and select "Alexa-hosted (Node.js)" as the option in the setting `Choose a method to host your skill's backend resources`, if it's not already selected.
When everything is ready, click on `Create Skill`. The next page will ask you to `Choose a template to add to your skill`, and we should select "Start from Scratch" and click `Continue with template`. Voilà! We have our skill created and ready to be personalized.

## Adding an Invocation Name and Audio Interface

With the skill created, the first step is to create an invocation name. This is the sentence/couple of words that Alexa will use to invoke our code. To configure that, we need to click on `Invocation Name` and type the desired invocation in the field below `Skill Invocation Name` and click in `Save Model`. With that set and ready, there's one more configuration that needs to be done: activate our audio interface. In order to do that, click in the `Interfaces` option which is located at the left menu. After that, check the first toogle called `Audio Player` and save the interface and build model.
The message `Quick build in progress` will show up. Wait until the build is ready and let's go to the next step!

## Editing the code

The next step is to edit the code adding our audio file! We need to specify a URL that contains an audio that plays itself. You can self-host it at AWS or whatever host of your choice, or search the web to find one. In my example, I'll be using a My Instants audio.

To edit the code, click at `Code` in the menu. A web code editor will show up with multiple files. The one that we are going to edit is `index.js`, and it should be open.

The next part is easy: replace the following code:

```
const speakOutput = 'Welcome, you can say Hello or Help. Which would you like to try?';

        return handlerInput.responseBuilder
            .speak(speakOutput)
            .reprompt(speakOutput)
            .getResponse();
```
by this one:

```
const speakOutput = 'Its me, Mario!';

        return handlerInput.responseBuilder
            .speak(speakOutput)
            .addAudioPlayerPlayDirective('REPLACE_ALL', '*', 1, 0, null, null)
            .getResponse();
```

Explaining briefly, the `speakOutput` corresponds to the line that Alexa will say to you when our code is invoked. You can change the  `It's me, Mario!` to whatever you want, just make sure to write it between simple quotation marks.
The magic happens above: at the line `.addAudioPlayerPlayDirective('REPLACE_ALL', '*', 1, 0, null, null)`, the `'*'` is the placeholder for our audio link. I replaced it to be like this:

```
const speakOutput = 'Its me, Mario!';

        return handlerInput.responseBuilder
            .speak(speakOutput)
            .addAudioPlayerPlayDirective('REPLACE_ALL', 'https://www.myinstants.com/media/sounds/its-me-mario.mp3', 1, 0, null, null)
            .getResponse();
```

After you added your audio file to the code, you need to `Save` and `Deploy` your code, wait until the deployment is done and that's it! Or is it? :thinking: 

## Activating Test Mode

To finally call your skill in your personal Alexa, there's one last step: activating the skill testing. To do that, just click at  `Test` located in the menu above your code, and change the option besides `Test is disabled for this skill.` to `Development`. Now you can call your Alexa and say your invocation name to test your skill!


## Final Remarks

This is merely an option to easily create a single-use only skill, to be used locally forever in the development stage. We will not dive into publishing the skill to the world in this tutorial.

