If you do not have an Amazon account, create one and go to Lex in your Amazon console.

Today we are going to build a Temperature conversion bot using Lex & Lambda. Using this bot we will be converting Celsius to Kelvin, Celsius to Farenheit & Vice-versa.

1. Create a new bot and name it “TempConversionBot” or whatever you want.
2. Go to the bot you created and create a new custom intent.
3. When you create a custom intent, you need to provide utterances for invoking the intent. For our bot, the utterances can be Hi, hey, hello, and so on for initial greetings.
4. Now we need to provide a slot for getting the name from the user. We can use the built-in slot type AMAZON.US_FIRST_NAME for this purpose.
5.  Provide the fulfillment as Return parameters to the client for now and save the intent.

 The intent should look something like the below:

![greet](<./Utterances images/greet.png>)

# Introducing Lambda

AWS Lambda lets you run code without provisioning or managing servers. So you can write a Lambda function and hook it up to your intent to send the specific response you expect for that intent. We are using lambda function for ctof intetn as follows:

![greet](<./Utterances images/c_to_f_utterance.png>)
![greet](<./Utterances images/c_to_k_utterance.png>)
![greet](<./Utterances images/f_to_c_utterance.png>)

Let’s create the Lambda we need.

    Go to the lambda console and click Create a new lambda function.

    Select Function from scratch..

    Provide a name for the lamdba and choose the runtime as Python 2.7.

    Copy paste the below code in the editor:

# For Celsius to Farenheit conversion

    import json
    def lambda_handler(event, context):
    x=int(event["currentIntent"]["slots"]["c"])
    y=x*9/5+ 32
    
    return {
        "sessionAttributes":event["sessionAttributes"],
        "dialogAction": {
            "type": "Close",
            "fulfillmentState": "Fulfilled",
            "message": {
                "contentType": "PlainText",
                "content":"the equivalent of "+str(x)+" degree celsius is "+str(y)+ " degree farenheit"
    }
    }
    }

You can create more intent & connect to lambda. We have provided the code above:

Thats it! Our bot is now ready. You can build the bot and test it, and the conversation should go something like this.

![greet](<./output.png>)

<h1> WEATHER CHATBOT </h1>

![weather](https://github.com/Diwas524/AWS-LEX-LAMBDA-CHATBOT/blob/main/weather_output.png)
