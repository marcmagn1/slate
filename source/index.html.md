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

| Name            | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Required | Example                    |
|-----------------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------------------------|
| source          | string | This is the sender Id the message will appear from (ie: TPOA).  The source can be an alphanumeric string that can contain both upper- and lower-case ASCII letters,  digits from 0 to 9 and the space character. The maximum length for alphanumeric sources is 11 characters. Alphanumeric sources are mainly used for sending branded SMS.    According to the country where you send your SMS, this value might be overwritten by a value forced by the mobile network to ensure delivery. | Optional | DarkVador                  |
| destination     | string |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Required | +6512345678                |
| clientMessageId | string |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Optional | DkVd0001                   |
| text            | string |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Required | I am your father           |
| encoding        | string |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Optional | AUTO                       |
| scheduled       | string |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Optional | "2016-11-03T08:24:20.362Z" |
| expiry          | string |  

> The single SMS request expect to receive a JSON with the following structure of names/values

```json
{
  "source": "string",
  "destination": "string",
  "clientMessageId": "string",
  "text": "string",
  "encoding": "AUTO",
  "scheduled": "2016-11-03T08:24:20.332Z",
  "expiry": "2016-11-03T08:24:20.332Z"
}
```

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

