# Messenger Send API Reference
The Send API is the main API used to send messages to users, including text, attachments, structured message templates, sender actions, and more.

#### Permissions
A page access token with pages_messaging permission is required to interact with this endpoint.

Apps in Development Mode, are restricted to message people that have a role in the app. Additionally Pages in unpublished status will only be allowed to message people with a role on the Page.

#### Request URI
`
https://graph.facebook.com/v11.0/me/messages?access_token=<PAGE_ACCESS_TOKEN>
`
#### Example Request
```sh
curl -X POST -H "Content-Type: application/json" -d '{
  "messaging_type": "<MESSAGING_TYPE>",
  "recipient": {
    "id": "<PSID>"
  },
  "message": {
    "text": "hello, world!"
  }
}' "https://graph.facebook.com/v11.0/me/messages?access_token=<PAGE_ACCESS_TOKEN>"
```
#### Properties
- ##### messaging_type : String
    The messaging type of the message being sent. 
    https://developers.facebook.com/docs/messenger-platform/send-messages/#messaging_types 

- ##### recipient : Object
    recipient object
- ##### message : Object
    message object. Cannot be sent with sender_action.
- ##### sender_action : Object
    Message state to display to the user:
    
    - typing_on: display the typing bubble
    - typing_off: remove the typing bubble
    - mark_seen: display the confirmation icon
    
    Cannot be sent with message. Must be sent as a separate request.
    
    When using sender_action, recipient should be the only other property set in the request.

