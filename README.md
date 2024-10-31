# MuleSoft IDP Universal 🌐 Callback API

See https://github.com/composableforce/MuleSoft-IDP-Universal-Service for Implmentation Example in the form of a example project jar

Break the Cycle of Polling

The IDP platform supports webhooks for callbacks, allowing you to eliminate costly polling. Instead, delegate the responsibility to the IDP to notify you when an event occurs with your document submission while harnessing the robust nature of AsyncAP

It's important to consider a few potential challenges, which the MuleSoft IDP Universal 🌐 Callback API  is designed to mitigate:

📍 Submission Context
Challenge: Upon submitting a document to the IDP, the only returned information is an Execution ID. Without the Action and Version details, it's impossible to determine the context or the specific process to which the Execution ID pertains.	Solution: The Universal REST Connector consolidates these actions, significantly reducing the number of connectors required.

📍 Security
Challenge: Official docs state noAuthUrl	Solution: A legitimate way is to add security via apikey query parameter which is better than an open api 

📍 Enterprise Scale:
Challenge: How to manage 100 doc action webhooks? How to persist notifications?	Solution: This connector allows for the rapid onboarding of new document actions, enabling your enterprise to scale efficiently and effectively.

  ###  [IDP Callback URL MuleSoft Documents](https://docs.mulesoft.com/idp/automate-document-processing-with-the-idp-api#callback-url).

  You can define a callback URL when you call IDP to execute your document actions. If defined, IDP calls the callback URL when the document action execution finishes.

  To specify the callback URL, include the `callback` field in your API call and define a JSON value with the callback URL. The following example adds a callback to the previous `curl` command example:

    Dataweave:
  ```
    %dw 2.0
    output java
    ---
    {
      parts: {
        callback: {
          content: '{"noAuthUrl": "'++ vars.callbackUrl ++'"}'
        },
        file: {
          headers: {
            "Content-Disposition": {
              name: "file",
              filename: vars.filenameAndExtension,
              subtype: "form-data"
            }
          },
          content: payload
        }
      }
    }
  ```



YES you can add Authentication to your Callback!

     ### Adding API Key to Query Parameters

        Use Client ID Enforcement policy with API Manager

        Custom Expression

        Client ID Expression
        DataWeave Expression to be used to extract the Client ID from API requests

              ```
                #[%dw 2.4 import fromBase64 from dw::core::Binaries import * from dw::core::Strings output application/java --- substringBefore(fromBase64(attributes.queryParams.apikey as String), ':')]

              ```
        Client Secret Expression
        DataWeave Expression to be used to extract the Client Secret from API requests

              ```
                #[%dw 2.4 import fromBase64 from dw::core::Binaries import * from dw::core::Strings output application/java --- substringAfter(fromBase64(attributes.queryParams.apikey as String), ':')]

              ```
        Your apikey becomes ClientId:ClientSecret then Base64

 

Implementation: 

Step1 - Create your own version of the RAML Spec in Design Center
![image](https://github.com/user-attachments/assets/fa9f89be-202a-4ff8-b976-042c0680f12a)

Step2 - Make changes where applicable
![image](https://github.com/user-attachments/assets/513b7e56-a477-4a11-adcc-c618a78b56fb)

Step3 - Publish to your Exchange and add colour to your exchange asset:
  - Add Exchange Icon ![image](https://github.com/user-attachments/assets/a5edf91c-a30d-41ef-bcb0-1b82a30cd91a)

  - Change Title to “MuleSoft IDP Universal 🌐 Callback API”
  - Add Description “One Authenticated Callback to rule them All”
  - Add following markdown to Exchange home page
      ![https://blogs.mulesoft.com/wp-content/uploads/IDP-Blog-Image-1.png](https://blogs.mulesoft.com/wp-content/uploads/IDP-Blog-Image-1.png)

