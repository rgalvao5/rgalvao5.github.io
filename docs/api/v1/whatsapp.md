## Whatsapp Api V1
To get access token and set webhook url to receive, access:

    https://app.omnize.com.br

Go to:

    Menu > Settings > Integrations > ClientSDK

Click on 'Generate Token' to obtain a new one, after that set the 'Webhook URL' to receive the triggers events.

#### For homolog environment

    Omnize platform: https://homolog.app.omnize.com.br

    Api endpoint: https://homolog.services.omnize.com.br

#### Get Departments
Make HTTP request:

    GET https://services.omnize.com.br/api/v1/departments?token=jh2kj3k12j3hk1j


#### Send message
Make HTTP request:

    POST https://services.api.omnize.com.br/api/v1/whatsapp

With body:

    {
      "token": "j23hk4j2h3kj4h...",
      "content": "Test message",
      "department_id": 1,
      "customer": {
        "name": "abcd1234" //Optional
        "email": "abcd1234" //Optional
        "phone": "abcd1234" //Optional
        "cpf": "abcd1234" //Optional
        "external_id": "abcd1234" //Required
      },
      "extra" : { // Optional, returned on webhook
        "clientId": "12",
        "botId": "1111"
      },
	  "external_history": "chathistory.example.org" // Optional
    }

Response:

    {
      "message": "Message sent successfully",
      "data": {
        "message_hash": "3110a5da-87c7-4f6d-a4ab-2b1ed5edfd46"
      }
    }

#### Notify when client typing
Make HTTP request:

    PUT https://services.omnize.com.br/api/v1/whatsapp/typing

With body:

    {
      "token": "j23hk4j2h3kj4h...",
      "customer": {
        "external_id": "abcd1234" //Required
      }
    }

#### Notify when client stop typing
Make HTTP request:

    PUT https://services.omnize.com.br/api/v1/interactions/cleared

With body:

    {
      "token": "j23hk4j2h3kj4h...",
      "customer": {
        "external_id": "abcd1234" //Required
      }
    }

## Triggers

####  Agent finish interaction:

    {
      "external_id": "abcd1234",
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "finished"
    }

####  Agent typing:

    {
      "external_id": "abcd1234",
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "typing"
    }

####  Agent stop typing:

    {
      "external_id": "abcd1234",
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "cleared"
    }

#### Agent new message:

    {
      "external_id": "abcd1234",
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "message": {
        "content": "Message",
        "type": "text"
      }
    }