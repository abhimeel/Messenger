# Messenger
The Send API is the main API used to send messages to users, including text, attachments, structured message templates, sender actions, and more.

## Permissions
A page access token with pages_messaging permission is required to interact with this endpoint.

Apps in Development Mode, are restricted to message people that have a role in the app. Additionally Pages in unpublished status will only be allowed to message people with a role on the Page.

### Steps to get page access token
  1. Create a Facebook page : https://www.facebook.com/help/104002523024878/
  2. Create a Facebook app https://developers.facebook.com/docs/development/create-an-app/
  3. Go to your Facebook app dashboard
  
      ![image](https://user-images.githubusercontent.com/40603380/129201441-7aa55a9a-8657-4948-952f-8ba6f522263b.png)
     
  4. Click on _**Messenger > Settings**_
  5. In the newly opened page, go to the _**Access Tokens**_ section
![image](https://user-images.githubusercontent.com/40603380/129202453-44865b6d-0ae9-40a4-b296-514551b6873b.png)
  6. Add the page created in **Step 1** and generate an _**Access Token**_
  7. Now, go to the _**Webhooks**_ section
![image](https://user-images.githubusercontent.com/40603380/129202747-88244ec5-befd-46ff-9874-10ecac45525e.png)
  8. Edit the **callback URL**, and provide the same _**Verify Token**_ that you have used in your app.
  9. For more details, visit: https://developers.facebook.com/docs/messenger-platform/getting-started/app-setup/
  10. Make sure to select all the fields in the webhooks section
  ![image](https://user-images.githubusercontent.com/40603380/129203109-996f2ee9-db6a-43da-ac4a-00dd176c52e5.png)



## Send API Reference
https://developers.facebook.com/docs/messenger-platform/send-messages#send_api_basics

### Request URI
`
https://graph.facebook.com/v11.0/me/messages?access_token=<PAGE_ACCESS_TOKEN>
`
### Example Request
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

### API Response
A successful Send API request to a PSID returns a JSON string containing identifiers for the message and its recipient.
```sh
{
  "recipient_id": "1008372609250235",
  "message_id": "m_AG5Hz2Uq7tuwNEhXfYYKj8mJEM_QPpz5jdCK48PnKAjSdjfipqxqMvK8ma6AC8fplwlqLP_5cgXIbu7I3rBN0P"
}
```
