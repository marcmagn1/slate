---
title: Wavecell API Reference

toc_footers:
  - <a href='https://www.wavecell.com/customer/Account/Register'>Sign up to get a Wavecell account</a>
  - <a href='https://wavecell.com'>Check-out Wavecell products</a>
  - <a href='http://support.wavecell.com/anonymous_requests/new'>Contact support</a>
includes:
  - errors

search: true
---

# Introduction

- Welcome to the **Wavecell SMS API documentation**!
- You can use our API to **send single SMS requests or batch SMS requests to deliver your text messages to any country or operator in the World** using your Wavecell account.
- If you do not already have a Wavecell account, create one in minutes on our website: <a href="https://www.wavecell.com">https://www.wavecell.com</a>
- To configure your account, credit your Wavecell balance, check your consumption and see a detailed pricing, head over to <a href="https://www.wavecell.com/customer/Account/Login">your account dashboard</a>
- If you need any assistance with our service or if you need some help with the API integration, you can open a <a href="http://support.wavecell.com/anonymous_requests/new">support ticket</a>
- If you need to contact our account management team for any commercial requests regarding your Wavecell account, you can reach out to them by email at <a href="mailto:sales@wavecell.com">sales@wavecell.com</a>


# Authentication

- Wavecell SMS API uses **HTTP/HTTPS basic authentication**. 
- The authentication uses the following credentials:
  - **username**: *your Wavecell AccountId*
  - **password**: *your Wavecell Password (it can be modified from your account dashboard)*

<aside class="notice">
- You can register a new Wavecell account from Wavecell <a href="https://www.wavecell.com/customer/Account/Register">website</a>.
</aside>

# Endpoints overview

Using Wavecell API, you can use 3 different methods to send SMS to your end-users, each method is specific and best-suited for well-defined use-cases:

- <a href="index.html#send-sms-single">**Send SMS - Single**</a> allows to send one SMS per requests and is the most simple endpoint: you submit a JSON object with the SMS properties to the API, it is most suited for transactional SMS.
- <a href="index.html#send-sms-many">**Send SMS - Many**</a> allows to submit an array of SMS to the API, it should be used for broadcasting personalized content when each message needs a certain amount of unique personalization.
- <a href="index.html#send-sms-many-compact">**Send SMS - Many (Compact)**</a> allows to submit an array of SMS to the API in a simplified format compared to the previous endpoint. With this endpoint, you can specify common parameters for the array of SMS and thus, only specify the unique parameter(s) for each SMS in the request. It should be used for broadcasting messages requiring less personalization.

# Send SMS - Single

- This endpoint is used to **send SMS individually (1 request per SMS)**.
- It is ideal to send single personalized messages for use-cases like notifications or alerting for example.

## URL

- The Wavecell subaccountid to use is defined in the URL where you send your POST request as shown below:

`https://api.wavecell.com/sms/v1/{subAccountId}/single`

<aside class="notice">
You must replace <code>{subAccountId}</code> in the URL above with the subaccountid that you want to use.
</aside>

## Request structure


> The single SMS request expects to receive a JSON with the following structure of names/values

```json
{
  "source": "Developer",
  "destination": "+6512345678",
  "clientMessageId": "MyBd00001",
  "text": "Hellow World",
  "encoding": "AUTO",
  "scheduled": "2016-11-03T08:24:20.332Z",
  "expiry": "2016-11-03T18:24:20.332Z"
}
```


- To send a single SMS using the Wavecell SMS API you need to submit a JSON object to the url defined above.
- The JSON object takes the following properties:


| Name | Type | Description | Required |
|:---------------:|:---------:|-----------------------------------------------------------------|:--------:|
| **source** | string |  Alphanumeric or numeric string used as Sender ID for the SMS | Optional |
| **destination** | string | Destination phone number | Required |
| **clientMessageId** | string | Unique id that you want to associate with the SMS | Optional |
| **text** | string | SMS body (ie: text of the message) | Required |
| **encoding** | string | Character set to use for this SMS - The possible values are `AUTO` - `GSM7bit` - `UNICODE` | Optional |
| **scheduled** | timestamp | Pre-defined date and time for this SMS to be sent in the future | Optional |
| **expiry** | timestamp | Maximum date and time for this SMS to be sent at | Optional |

## Request body 

Below is a more detailed description of the parameters in the SMS request body (JSON object submitted to the API)

### Source

The source value can also be called senderID or TPOA.  
It is the from address that will be used when delivering the SMS to the handset.  
It can take different formats:

- **Alphanumeric** *(example: MyBrand):* this is the case when a source is composed of an alphanumeric string (max 11 characters: letters from the ASCII character set, digits and the space character). Alphanumeric sources are generally used for branded SMS to help the SMS receiver to identify the brand or services which originated the SMS.
- **Numeric** *(example: +6512345678):* this the case when a source is composed of a string made purely of digits (max 17 chars). It can also start with the + sign. Numeric sources ar generally used when the originator intends to receive an answer to the SMS as it is interpreted as a regular phone number by the destination handset.

**NB - Limitations:** According to the country where the SMS is sent to, sources can be overwritten in order to ensure a better delivery. If you have some specific inquiries related to the type of source available for your account towards a specific destination, please <a href='mailto:sales@wavecell.com'>contact your account manager</a>.

### Destination

- This value is the destination phone number for the SMS.
- The destination should be submitted following the international format: it should include the country code (the leading + sign can be omitted but this is not an obligation) and the leading 0 of the local format has to be removed.
- *(Valid examples include: +6512345678, 6512345678)*

### ClientMessageId

- This value is not mandatory.
- If used, the clientMessageId allows you to submit SMS associated to your custom message ID. That way, you are able to match the information contained in the API response  with the ID from your own business logic.

### Text

- The text or the message (or SMS body) is the main part of your SMS: it is what is going to be displayed on the destination handset.
- It can contain characters from the ASCII character or from the UNICODE character set (see next section for more information).
- According to the encoding of the SMS, the number of SMS accounted per message will be proportional to the length of the text:
  - For ASCII messages, 160 characters = 1 SMS (1 part)
  - For Unicode messages, 70 characters = 1 SMS (1 part)
- The maximum length for a text is 10 parts

### Encoding

`AUTO` - `GSM7bit` - `UNICODE`

- **AUTO**: the API will analyze the content of your SMS text and select the correct encoding according to the characters used: if your SMS text contains UNICODE characters, then UNICODE will be selected, otherwise it will be ASCII
- **GSM7bit**: by using GSM7bit, you are forcing the encoding in use to be GSM 7 bit: it will render correctly any of the characters from the character set (See a complete list <a href="https://en.wikipedia.org/wiki/GSM_03.38#GSM_7-bit_default_alphabet_and_extension_table_of_3GPP_TS_23.038_.2F_GSM_03.38">there</a>). Wavecell API considers each block of 160 GSM 7 bit characters as 1 SMS unit.
- **UNICODE**: by using Unicode, you are forcing the encoding in use to be UNICODE: it will render correctly any of the characters from the UNICODE character set (See a complete list <a href="https://en.wikipedia.org/wiki/List_of_Unicode_characters8">there</a>). Wavecell API considers each block of 70 UNICODE characters as 1 SMS unit.

### Scheduled

- The scheduled parameter should be used if you wish to schedule your message up to 7 days in advance. The SMS will be stored on the Wavecell platform and sent out at the predefined time and date. You can specify the scheduling timestamp using the standard ISO 8601 format (which includes and specifies the timezone offset to use):
`"scheduled":"2016-11-07T19:20:30+08:00"`

### Expiry

- The expiry parameter should be used if you wish to specify a maximum time and date for the SMS to be sent. If for any reason the Wavecell platform fails to send the message before the date and time predefined, the SMS will be discarded. You can specify the expiry timestamp using the standard ISO 8601 format (which includes and specifies the timezone offset to use):
`"scheduled":"2016-11-07T19:20:30+08:00"`

## Response

> The above command returns a JSON object structured like this:

```json
{
  "umid": "string",
  "clientMessageId": "string",
  "destination": "string",
  "status": {
    "code": "string",
    "description": "string"
  }
}
```

The response returns the following:

- **umid**: unique message ID automatically generated by Wavecell
- **clientMessageId**: message ID that you submitted (if any)
- **destination**: destination phone number to which the SMS was sent to


A **status** object containing the following information:

- **status code**: the status code can be either:
  + **QUEUED**: the SMS has been accepted by Wavecell API and is queued for processing.
  + **REJECTED**: the SMS has been rejected by Wavecell API and the reason is stated in the description field. It will not be processed. 
- **description**: this field describes the status code and provides additional information explaining the status. It can take the following values: 
  + *SMS is accepted and queued for processing (QUEUED Status)*
  + *Text value is missing (REJECTED Status)*
  + *Invalid Text value. Reached max allowed limit (REJECTED Status)*
  + *Invalid Source value. Reached max allowed limit (REJECTED Status)*
  + *Expiry time already reached (REJECTED Status)*
  + *Invalid MSISDN format (not E.164 international number) (REJECTED Status)*
  + *Internal server error (REJECTED Status)*
 

# Send SMS - Many


- This endpoint is used to **send SMS by batches (1 request for multiple SMS) with personalized contents/properties**.
- It is ideal to send marketing campaigns or any kind of massive personalized announcement. To send a batch of identical SMS, it is easier to use the many/compact end-point.

## URL

The Wavecell subaccountid to use is defined in the URL where you send your POST request as shown below:

`https://api.wavecell.com/sms/v1/{subAccountId}/many`

<aside class="notice">
You must replace <code>{subAccountId}</code> in the URL above with the subaccountid that you want to use.
</aside>

## Request structure


> The Many SMS request expects to receive a JSON with the following structure of names/values

```json
{
  "clientBatchId": "string",
  "messages": [
    {
      "source": "string",
      "destination": "string",
      "clientMessageId": "string",
      "text": "string",
      "encoding": "AUTO",
      "scheduled": "2016-11-07T10:48:04.873Z",
      "expiry": "2016-11-07T10:48:04.873Z"
    }
  ],
  "template": {
    "source": "string",
    "text": "string",
    "encoding": "AUTO",
    "scheduled": "2016-11-07T10:48:04.874Z",
    "expiry": "2016-11-07T10:48:04.874Z"
  },
  "includeMessagesInResponse": true
}
```


To send many SMS using the Wavecell SMS API you need to submit a JSON-formatted request with the following elements:

| Name | Type | Description | Required |
|:-------------------------:|:-------:|-------------------------------------------------------------------------|:--------:|
| **clientBatchId** | string | Unique ID that you want to associate with the batch of SMS | Optional |
| **messages** | array | Array containing multiple SmsRequest objects (see Single doc) | Required |
| **template** | object | Object applying common properties to the SmsRequest objects in messages | Optional |
| **includeMessagesInResponse** | boolean | Boolean defining if the API response should contain the SMS details | Optional |

## About the template object

- The **many** endpoint incorporates a new logic with the template object. 
- The purpose of this object is to let you specify the common properties of the SMS contained in the messages into a single object. 
- The best practice is **to only incorporate the unique properties of each SMS in the SmsRequest objects** contained in the messages array **while specifying the common properties in the template object.**
- The **template object is optional in the request.**

The template object can take the following parameters:

| Name | Type | Description | Required |
|:---------:|:---------:|:---------------------------------------------------------------:|:--------:|
| **source** | string | Alphanumeric or numeric string used as Sender ID for the SMS | Optional |
| **text** | string | SMS body (ie: text of the message) | Required |
| **encoding** | string | Character set to use for this SMS - The possible values are `AUTO` - `GSM7bit` - `UNICODE` | Optional |
| **scheduled** | timestamp | Pre-defined date and time for this SMS to be sent in the future | Optional |
| **expiry** | timestamp | Maximum date and time for this SMS to be sent at | Optional |

## Response

> The above command returns a JSON object structured like this:

```json
{
  "batchId": "string",
  "clientBatchId": "string",
  "acceptedCount": 0,
  "rejectedCount": 0,
  "messages": [
    {
      "umid": "string",
      "clientMessageId": "string",
      "destination": "string",
      "status": {
        "code": "string",
        "description": "string"
      }
    }
  ]
}
```


- The response returns **two different IDs for the batch**:
  + **batchID**: the unique batch ID generated automatically by Wavecell
  + **clientBatchID**: the batch ID that you submitted in the request (if any)
- It also returns a **summary of the batch submission**:
  + **acceptedCount**: number of SMS accepted by the API
  + **rejectedCount**: number of SMS rejected by the API
- If the **includeMessagesInResponse** boolean has been set to True during the request, it also **returns an array containing individual information for each SMS submitted** to the API in the many request: 
  + **umid**: unique message ID automatically generated by Wavecell
  + **clientMessageId**: message ID that you submitted (if any)
  + **destination**: destination phone number to which the SMS was sent to
  

And a **status object** containing the following:

  - **status code**: the status code can be either:
    + **QUEUED**: the SMS has been accepted by Wavecell API and is queued for processing.
    + **REJECTED**: the SMS has been rejected by Wavecell API and the reason is stated in the description field. It will not be processed. 
  - **description**: this field describes the status code and provides additional information explaining the status. It can take the following values: 
    + *SMS is accepted and queued for processing (QUEUED Status)*
    + *Text value is missing (REJECTED Status)*
    + *Invalid Text value. Reached max allowed limit (REJECTED Status)*
    + *Invalid Source value. Reached max allowed limit (REJECTED Status)*
    + *Expiry time already reached (REJECTED Status)*
    + *Invalid MSISDN format (not E.164 international number) (REJECTED Status)*
    + *Internal server error (REJECTED Status)*

# Send SMS - Many (compact)


- This endpoint is **used to send SMS by batches (1 request for multiple SMS)**.
- It is a **derivated method from the many endpoint in a more compact form**. - It only accepts messages with the same properties (source, text, encoding, scheduling time and expiry time). 
- It should be used for use-cases such as announcement, message broadcasting, etc...


## URL

The Wavecell subaccountid to use is defined in the URL where you send your POST request as shown below:

`https://api.wavecell.com/sms/v1/{subAccountId}/many/compact`

<aside class="notice">
You must replace <code>{subAccountId}</code> in the URL above with the subaccountid that you want to use.
</aside>

## Request structure


> The Many - Compact SMS request expects to receive a JSON with the following structure of names/values

```json
{
  "clientBatchId": "string",
  "destinations": [
    "string"
  ],
  "template": {
    "source": "string",
    "text": "string",
    "encoding": "AUTO",
    "scheduled": "2016-11-07T10:48:04.874Z",
    "expiry": "2016-11-07T10:48:04.874Z"
  },
  "includeMessagesInResponse": true
}
```


To send many SMS using the Wavecell SMS API you need to submit a JSON-formatted request with the following elements:

| Name | Type | Description | Required |
|:-------------------------:|:-------:|---------------------------------------------------------------------------------------------------------------------|:--------:|
| **clientBatchId** | string | Unique ID that you want to associate with the batch of SMS | Optional |
| **destinations** | array | Array containing the list of destinations phone numbers to send an SMS to | Required |
| **template** | object | Object defining the properties of the SMS sent to the destination phone numbers contained in the destinations array | Required |
| **includeMessagesInResponse** | boolean | Boolean defining if the API response should contain the SMS details | Optional |

## About the template object

- The **many/compact** endpoint relies entirely on the template object to define the properties of the SMS to send. 
- Contrarily to the **many** endpoint, the **template object is required** when using the end-point.

The template object can take the following parameters:

| Name | Type | Description | Required |
|:---------:|:---------:|:---------------------------------------------------------------:|:--------:|
| **source** | string | Alphanumeric or numeric string used as Sender ID for the SMS | Optional |
| **text** | string | SMS body (ie: text of the message) | Required |
| **encoding** | string | Character set to use for this SMS - The possible values are `AUTO` - `GSM7bit` - `UNICODE` | Optional |
| **scheduled** | timestamp | Pre-defined date and time for this SMS to be sent in the future | Optional |
| **expiry** | timestamp | Maximum date and time for this SMS to be sent at | Optional |

## Response

> The above command returns a JSON object structured like this:

```json
{
  "batchId": "string",
  "clientBatchId": "string",
  "acceptedCount": 0,
  "rejectedCount": 0,
  "messages": [
    {
      "umid": "string",
      "clientMessageId": "string",
      "destination": "string",
      "status": {
        "code": "string",
        "description": "string"
      }
    }
  ]
}
```

- The response returns **two different IDs for the batch**:
  + **batchID**: the unique batch ID generated automatically by Wavecell
  + **clientBatchID**: the batch ID that you submitted in the request (if any)
- It also returns a **summary of the batch submission**:
  + **acceptedCount**: number of SMS accepted by the API
  + **rejectedCount**: number of SMS rejected by the API
- If the **includeMessagesInResponse** boolean has been set to True during the request, it also **returns an array containing individual information for each SMS submitted** to the API in the many request: 
  + **umid**: unique message ID automatically generated by Wavecell
  + **clientMessageId**: message ID that you submitted (if any)
  + **destination**: destination phone number to which the SMS was sent to
  

And a **status object** containing the following:

  - **status code**: the status code can be either:
    + **QUEUED**: the SMS has been accepted by Wavecell API and is queued for processing.
    + **REJECTED**: the SMS has been rejected by Wavecell API and the reason is stated in the description field. It will not be processed. 
  - **description**: this field describes the status code and provides additional information explaining the status. It can take the following values: 
    + *SMS is accepted and queued for processing (QUEUED Status)*
    + *Text value is missing (REJECTED Status)*
    + *Invalid Text value. Reached max allowed limit (REJECTED Status)*
    + *Invalid Source value. Reached max allowed limit (REJECTED Status)*
    + *Expiry time already reached (REJECTED Status)*
    + *Invalid MSISDN format (not E.164 international number) (REJECTED Status)*
    + *Internal server error (REJECTED Status)*
