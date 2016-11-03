---
title: API Reference

language_tabs:
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='https://www.wavecell.com/customer/Account/Register'>Sign up to get a Wavecell account</a>
  - <a href='https://wavecell.com'>Check-out Wavecell products</a>
  - <a href='http://support.wavecell.com/anonymous_requests/new'>Contact support</a>
includes:
  - errors

search: true
---

# Introduction

Welcome to the Wavecell SMS API! You can use our API to send single or bulk SMS to any country in the World using your Wavecell account.

# Authentication

> To authorize, use this code:

```ruby
RUBY CODE FOR AUTHENTICATION GOES HERE
```

```python
PYTHON CODE FOR AUTHENTICATION GOES HERE
```

```shell
SHELL CODE FOR AUTHENTICATION GOES HERE
```

```javascript
JS CODE FOR AUTHENTICATION GOES HERE
```

> Make sure to replace `Accountid`, `Password` and `{subaccountid}` with your API credentials.

Wavecell SMS API uses **HTTP/HTTPS basic Authentication**. The authentication uses the Wavecell AccountId as username and unless you modified it, the password to allow access to the API is your Wavecell password. You can register a new Wavecell account from Wavecell [website](http://www.wavecell.com/customer/Account/Register).

<aside class="notice">
You must replace <code>subaccountid</code> with the subaccountid that you want to use. Accountid and password should also be replaced by your own credentials.
</aside>

# Send SMS

## Send single SMS requests (POST)

```ruby
RUBY CODE FOR SENDING SINGLE SMS REQUESTS GOES HERE
```

```python
PYTHON  CODE FOR SENDING SINGLE SMS REQUESTS GOES HERE
```

```shell
SHELL CODE FOR SENDING SINGLE SMS REQUESTS GOES HERE
```

```javascript
JS CODE FOR SENDING SINGLE SMS REQUESTS GOES HERE
```

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

This endpoint is used to send SMS individually (1 request per SMS).
It is ideal to send single personalized messages for use-cases like notifications or alerting for example.

### URL

The Wavecell subaccountid to use is defined in the URL where you send your POST request as shown below:

`https://api.wavecell.io/sms/v1/{subAccountId}`

*NB: you need to replace {subAccountId} by the subAccountId that you intend to use*

### Request structure

To send a single SMS using the Wavecell SMS API you need to submit JSON object to the url defined above.
The JSON object takes the following properties:

| Name | Type | Description | Required |
|:---------------:|:---------:|-----------------------------------------------------------------|:--------:|
| source | string |  Alphanumeric or numeric string used as Sender ID for the SMS | Optional |
| destination | string | Destination phone number | Required |
| clientMessageId | string | Unique id that you want to associate with the SMS | Optional |
| text | string | SMS body (ie: text of the message) | Required |
| encoding | string | Character set to use for this SMS | Optional |
| scheduled | timestamp | Pre-defined date and time for this SMS to be sent in the future | Optional |
| expiry | timestamp | Maximum date and time for this SMS to be sent at | Optional |

> The single SMS request expect to receive a JSON with the following structure of names/values

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

# SmsRequest Object values

Here below is a more detailed information about the different values that you can assign when submitting SMS using Wavcell API.

##source
The source value can also be called senderID or TPOA. It is the from address that will be used when delivering the SMS to the handset.
It can take different formats:
- **Alphanumeric** *(example: MyBrand):* this is the case when a source is composed of an alphanumeric string (max 11 characters: letters from the ASCII character set, digits and the space character). Alphanumeric sources are generally used for branded SMS to help the SMS receiver to identify the brand or services which originated the SMS.
- **Numeric** *(example: +6512345678):*this the case when a source is composed of a string made purely of digits (max 17 chars). It can also start with the + sign. Numeric sources ar generally used when the originator intends to receive an answer to the SMS as it is interpereted as regular phone number by the destination handset.

**NB - Limitations:** According to the country where the SMS is sent to, sources can be overwritten in order to ensure a better delivery. If you have some specific enquiries related to the type of source available for your account towards a specific destination, please <a href='mailto:sales@wavecell.com'>contact your account manager</a>.
##destination
This value is the destination phone number for the SMS.
The destination should be submitted following the international format: it should include the country code (the leading + sign can be omitted but this is not an obligation) and the leading 0 of the local format has to be removed.
*(Valid examples include: +6512345678, 6512345678)*
##clientMessageId
This value is not mandatory. If used, the clientMessageId allows you to submit SMS associated to your custom message ID. That way, you are able to match the information contained in the API response  with the ID from your own business logic.
##text
The text or the message (or SMS body) is the main part of your SMS: it is what is going to be displayed on the destination handset.
It can contain characters from the ASCII character or from the UNICODE character set (see next section for more information)
##encoding
##scheduled
##expiry
