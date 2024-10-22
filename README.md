# MuleSoft IDP Universal 🌐 Callback API
Break the Cycle of Polling


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
