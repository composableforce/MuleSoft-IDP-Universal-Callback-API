protocols: HTTPS

  securedBy: 🛡️ MuleSoft Client ID Enforcement Policy (query parameter)

  | Author | Date | Description
  | -------- | ------- | ------- |
  | G.Jeffcock | 23rd June 2024 | Launched| 
  |||| 
  ||||

  ### MuleSoft IDP Universal 🌐 Callback API
Making the Composable IDP a reality
<img width="929" alt="mulesoft-idp-universal-process" src="https://github.com/composableforce/MuleSoft-IDP-Universal-Callback-API/assets/21179972/b2d2d16d-80b7-4b82-8860-f7f60d95f46a">


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


  ```
  curl --location 'https://idp-rt.{region}.anypoint.mulesoft.com/api/v1/organizations/{orgId}/actions/{actionId}/versions/{actionVersion}/executions' \
  --header 'Authorization: Bearer {token}' \
  --form 'file=@"{pathToFile}"' \
  --form 'callback="{\"noAuthUrl\":\"{callbackURL}\"}"'
  ```
