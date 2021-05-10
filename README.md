
## Requirements

You will need to install some stuff, if they are not yet installed in your machine:

* [Node.js (v4.3.2 or higher; LTS)](http://nodejs.org)
* [NPM (v3.5+; bundled with node.js installation package)](https://docs.npmjs.com/getting-started/installing-node#updating-npm)

If you've already installed the above you may need to only update **npm** to the latest version:

```bash
$ sudo npm update -g npm
```

---

## Install through Github

Best way to install Project Mulla is to clone it from Github

**To clone/download the boilerplate**

```bash
$ git clone https://github.com/kn9ts/project-mulla.git
```

**After cloning, get into your cloned Project Mulla's directory/folder**

```bash
$ cd project-mulla
```

**Install all of the projects dependencies with:**

```bash
$ npm install
```

__Create `app.yaml` configurations file__

The last but not the least step is to create a `app.yaml` file with your configurations in the root
directory of `project-mulla`.

This is the same folder directory where `index.js` can be found.

Your `app.yaml` should look like the example below, only with your specific configuration values:

```yaml
env_variables:
  PAYBILL_NUMBER: '898998'
  PASSKEY: 'a8eac82d7ac1461ba0348b0cb24d3f8140d3afb9be864e56a10d7e8026eaed66'
  MERCHANT_ENDPOINT: 'http://merchant-endpoint.com/mpesa/payment/complete'

# Everything below is only relevant if you are looking
# to deploy Project Mulla to Google App Engine.
runtime: nodejs
vm: true

skip_files:
  - ^(.*/)?.*/node_modules/.*$
```

*__NOTE:__ The `PAYBILL_NUMBER` and `PASSKEY` are provided by Safaricom once you have registered for the MPESA G2 API.*

*__NOTE:__ The details above only serve as examples*

# Testing

## It's now ready to launch

First run the command `npm test` on your terminal and see if everything is all good. Then run:

```bash
$ npm start

> project-mulla@0.1.1 start ../project-mulla
> node index.js

Your secret session key is: 5f06b1f1-1bff-470d-8198-9ca2f18919c5
Express server listening on 8080, in development mode
```

## Do a test run

Now make a test run using **CURL**:

```bash
$ curl -i -X POST \
  --url http://localhost:8080/api/v1/payment/request \
  --data 'phoneNumber=254723000000' \
  --data 'totalAmount=10.00' \
  --data 'clientName="Eugene Mutai"' \
  --data 'clientLocation=Kilimani' \
```

Or if you have [httpie](https://github.com/jkbrzt/httpie) installed:

```bash
$ http POST localhost:8080/api/v1/payment/request \
  phoneNumber=254723000000 \
  totalAmount=10.00 \
  clientName='Eugene Mutai' \
  clientLocation='Kilimani'
```

Once the request is executed, your console should print a similar structured **response** as below:

```http
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 534
Content-Type: application/json; charset=utf-8
Date: Sun, 22 May 2016 13:12:09 GMT
ETag: W/"216-NgmF2VWb0PIkUOKfya6WlA"
X-Powered-By: Express
set-cookie: connect.sid=s:iWfXH7rbAvXz7cYgmurhGTHDn0LNBmNt; Path=/; HttpOnly

{
  "response": {
    "return_code": "00",
    "status_code": 200,
    "message": "Transaction carried successfully",
    "trx_id": "453c70c4b2434bd94bcbafb17518dc8e",
    "description": "success",
    "cust_msg": "to complete this transaction, enter your bonga pin on your handset. if you don't have one dial *126*5# for instructions",
    "reference_id": "3e3beff0-fc05-417a-bbf2-190ee19a5e58",
    "merchant_transaction_id": "95d64500-2514-11e6-bcb8-a7f8e1c786c4",
    "amount_in_double_float": "10.00",
    "client_phone_number": "254723001575",
    "extra_payload": {},
    "time_stamp": "20160528234142"
  }
}
```


# This project uses GPLv3 LICENSE

__TL;DR__ Here's what the license entails:

```markdown
1. Anyone can copy, modify and distribute this software.
2. You have to include the license and copyright notice with each and every distribution.
3. You can use this software privately.
4. You can use this software for commercial purposes.
5. If you dare build your business solely from this code, you risk open-sourcing the whole code base.
6. If you modify it, you have to indicate changes made to the code.
7. Any modifications of this code base MUST be distributed with the same license, GPLv3.
8. This software is provided without warranty.
9. The software author or license can not be held liable for any damages inflicted by the software.
```

More information on the [LICENSE can be found here](http://choosealicense.com/licenses/gpl-3.0/)

*__DISCLAIMER:__* _All opinions aired in this repo are ours and do not reflect any company or organisation any contributor is involved with._
