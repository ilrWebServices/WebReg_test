# How to test WebReg

- Install the [Rest Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) extension for Visual Studio Code.
- Copy `.env.example` to `.env` and set the `TOKEN` value to an valid OAuth token.
- Open `WebReg_test.http`, adjust the payload as needed, and click 'Send request'.

## Example 200 response:

```
HTTP/1.1 200 OK
Date: Tue, 06 Jun 2023 16:06:44 GMT
Strict-Transport-Security: max-age=63072000; includeSubDomains
X-Content-Type-Options: nosniff
X-XSS-Protection: 1; mode=block
X-Robots-Tag: none
Cache-Control: no-cache,must-revalidate,max-age=0,no-store,private
Content-Type: application/octetstream
Transfer-Encoding: chunked
Connection: close

{"pos_order_id":5632,"sf_order_id":a0M0500000CpulPEAR}
```

### Issues:

- Content-Type should be `application/json`
- `sf_order_id` should be wrapped in quotes.

## Example error response

Removed `order_id` from the payload.

```
HTTP/1.1 500 Server Error
Date: Tue, 06 Jun 2023 16:09:58 GMT
Strict-Transport-Security: max-age=63072000; includeSubDomains
X-Content-Type-Options: nosniff
X-XSS-Protection: 1; mode=block
X-Robots-Tag: none
Cache-Control: no-cache,must-revalidate,max-age=0,no-store,private
Content-Type: application/octetstream
Transfer-Encoding: chunked
Connection: close

{"status": 500,"timestamp" : "2023-06-06 12:09:58","error" : "Internal Server Error","message" : "Argument cannot be null.",}
```

### Issues

- Content-Type should be `application/json`
- Trailing comma after `message`
- Error message is a bit vague. Which argument?
