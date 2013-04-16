Comfirm AlphaMail Node.js Client
================================
Use this library to connect your Node.js application to the AlphaMail system. 
Start sending transactional e-mail today without the hassle of SMTP and large blocks of unmaintainable HTML.

AlphaMail supports templating (Comlang), DKIM-signatures and reliable delivery. Beside that, we got awesome statistics.

http://amail.io/

### How to start?

1) Install with NPM:

    $ npm install alphamail

2) Sign Up:

    http://amail.io/

3) Send your first mail!
    
    var alphamail = require('alphamail');
    var emailService = new alphamail.EmailService("API-TOKEN");
     
    var data = {
        id: "abc-123-456",
        name: "Some Guy",
        profile_url: "http://domain.com/profile/ABC-123-456/",
        recommended_profiles: [
            {
                id: "abc-222-333",
                name: "Jane Joe",
                profile_url: "http://domain.com/profile/ABC-222-333/",
                profile_image_url: "http://img.domain.com/profile/abc-222-333.jpg",
                age: 24
            }
        ]
    };
    
    var payload = new alphamail.EmailMessagePayload()
        .setProjectId(1235) // ID of your AlphaMail project
        .setSender(new alphamail.EmailContact("My Company", "your@domain.com"))
        .setReceiver(new alphamail.EmailContact("Some guy", "some@guy.com"))
        .setBodyObject(data);
     
    emailService.queue(payload, function(error, result){
        if(error){
            console.log(error);
            return;
        }
        console.log("Email sent! ID = " + result);
    });
    
### Usage

Include the module

    var alphamail = require('alphamail');

Initialize an email service with your token

<sub><i>Don't have a token? Head to http://amail.io/ and signup for a free AlphaMail account.</i></sub>

    var emailService = new alphamail.EmailService(apiToken);
    
Queue an email for sending

    emailService.queue(payload, callback);

<sub><i>Where payload is:</i></sub>

    var payload = new alphamail.EmailMessagePayload()
        .setProjectId(12345) // ID of your AlphaMail project
        .setSender(new alphamail.EmailContact("My Company", "your@domain.com"))
        .setReceiver(new alphamail.EmailContact("Some guy", "some@guy.com"))
        .setBodyObject({/*Data to use in email*/});
        
<sub><i>Where callback is:</i></sub>

    var callback = function(error, result){
        if(error){
            console.log(error);
        }else{
            console.log("Mail successfully sent! ID = " + result);
        }
    };
