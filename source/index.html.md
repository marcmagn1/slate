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

## Send single SMS requests

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

### HTTP Request

`POST https://api.wavecell.io/sms/v1/{subAccountId}`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

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

