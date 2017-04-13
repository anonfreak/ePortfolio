# Tutorial for Lottery-API with Apiary
## Create Apiary-Account
The first step to create your API-Documentation is to create an Account on [Apiary.io](http://apiary.io/), which is the Cloud-Platform of API-Blueprint. You could also code your API-Documentation locally by using API-Blueprint itself, which is available [here](https://apiblueprint.org/).
### Sign-In
Go to [Apiary.io](http://apiary.io/) and press Sign Up, which should let you create an account by using your e-mail address or by logging in with your existing GitHub or Google-Account. Logging in with your GitHub-Account will give you automatically sync of your API-Documentation  with your GitHub-Repository.
### Create First API
After you've signed up you're instantly prompted to create your first API-Documentation. Just give it a name you like, but make sure to start you API in *API-Blueprint*. After pressing *Save and Start using Apiary*, you're ready to go.
## Create API-Documentation
### Define Objects
Firstly, you should define some objects, which represent your objects, you communication will be based on. In this particular example, you should start with defining a lottery bill  (6 numbers and one "Super"-Number). Objects have to be defined in the ***Data Structure***-Section, as seen in the following code block:
```Markdown
# Data Structures

## lotteryNumbers (object)
+ numbers: 1, 2, 3, 4, 5, 6 (array[number]) - 6 winning numbers of the lottery
+ superNumber: 42 (number) - Super winning number

## lotteryBill (object)
+ lotteryNumber (lotteryNumbers) - Numbers of the lottery bill
+ date (date) - Datum

## date (object)
+ year: 2017 (number)
+ month: 6 (number)
+ day: 24 (number)
```
*lotteryNumbers* is a subclass of a normal object and should contain an array of 6 numbers, which are stored in *numbers*. You're able to provide sample data as shown above, which will be used to show examples in the real documentation or to mock your API.
### Define Interfaces
After you've defined the object, you should think about the API Endpoints and Interfaces. The standard resource is about the winning numbers, therefore I called the interface */numbers*. This one resource is enough to complete all tasks by using the HTTP-Methods *GET* and *POST*, as well as parameters.
```Markdown
## Submit [POST]
Submit the winning numbers of today.

+ Request (application/json)
    + Attributes (lotteryNumbers)

+ Response 200 (application/json)
    + Headers
            Location: /numbers/10042017

    + Attributes (lotteryBill)

## Request recent [GET]
Get the most recent number

+ Response 200 (application/json)
    + Headers

            Location: /numbers/10042017

    + Attributes (lotteryBill)

## Request specific [GET /numbers/{ddmmyyyy}]
Get specific winning numbers of one date.

+ Parameters
    + ddmmyyyy: 10042017 (required, string) - Date of Winning Numbers

+ Response 200 (application/json)
    + Attributes (lotteryBill)


```
By using your predefined Objects, you save a lots of code, because you can use them in your Response and the Request. For requesting the winning numbers of a specific date, you should directly address the resource without using query parameters, because it's much cleaner.
