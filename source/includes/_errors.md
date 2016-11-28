# Errors


> The error codes response model is structured as follow:

```json
{
  "code": 0,
  "message": "string",
  "errorId": "string",
  "timestamp": "2016-11-28T10:32:42.881Z"
}
```


The Wavecell API uses the following **error codes**:

| HTTP Status Code | Reason |
|:----------------:|:-------------------:|
| 204 | No Content |
| 400 | BadRequest |
| 401 | Unauthorized |
| 500 | InternalServerError |