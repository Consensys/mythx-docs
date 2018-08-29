# Quick Start to Using Mythril API
`

__Note: API key behavior will be changing shortly__

After you get your Mythril API key, you can use it to:

* Submit EVM bytecode for analysis, and
* Review the results of previous submissions

Without an API key you can query the latest
API version, or retrieve the Mythril-API specification.

We will use [curl](https://curl.haxx.se/) commands here, but there
will be language binding for various programming languages.

To follow the examples below, set the environment variable `$MYTHRIL_API_KEY`
to your Mythril Platform API key.

## Submitting EVM bytecode

To start an analysis, you need to submit the EVM bytecode of one or multiple
smart contracts. Send a HTTP POST request to the `mythril/v1/analysis` endpoint:

```console
$ EVM_BYTECODE='0x3f'  # replace with a real contract
$ curl -i -X POST https://api.mythril.ai/mythril/v1/analysis \
  -H "Authorization: Bearer $MYTHRIL_API_KEY" \
  -H 'Content-Type: application/json' \
  -d "{ \"type\": \"bytecode\",  \"contract\": \"$EVM_BYTECODE\" }"
```

This should return the response:

```console
HTTP/1.1 200 OK
Access-Control-Allow-Origin: *
Content-Type: application/json; charset=utf-8
Date: Tue, 28 Aug 2018 21:07:22 GMT
ETag: W/"41-IC6lt17lHup/pxONgTVPHzOnYKQ"
Server: nginx/1.12.1
Strict-Transport-Security: max-age=15552000; includeSubDomains
X-Content-Type-Options: nosniff
X-DNS-Prefetch-Control: off
X-Download-Options: noopen
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
Content-Length: 65
Connection: keep-alive

{"result":"Queued","uuid":"df946130-a25c-4268-b2d0-e3ccc592f7c0"}
$
```

## Checking the Status of a Submission

In the previous section we kicked off an vulnerability analysis job
which is run asynchronously. To check the status of the analysis job
use the uuid returned in the HTTP response. The uuid received in the
last section was `df946130-a25c-4268-b2d0-e3ccc592f7c0`. Send an
HTTP GET request to `/mythril/v1/analysis/$UUID`:

```console
$ UUID=df946130-a25c-4268-b2d0-e3ccc592f7c0
$ curl -i -X GET https://api.mythril.ai/mythril/v1/analysis/$UUID \
  -H "Authorization: Bearer $MYTHRIL_API_KEY"
```
If the job has run successfully, you should get the following response:

```console
HTTP/1.1 200 OK
Access-Control-Allow-Origin: *
Content-Type: application/json; charset=utf-8
Date: Tue, 28 Aug 2018 21:16:59 GMT
ETag: W/"43-jqZkT/RfYhCeqpXFo7NYY2rqqjM"
Server: nginx/1.12.1
Strict-Transport-Security: max-age=15552000; includeSubDomains
X-Content-Type-Options: nosniff
X-DNS-Prefetch-Control: off
X-Download-Options: noopen
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
Content-Length: 67
Connection: keep-alive

{"result":"Finished","uuid":"df946130-a25c-4268-b2d0-e3ccc592f7c0"}
```

Notice that the status result says "Finished". Another result could have been "Error". For example changing the ending `c0` to `cb` in the UUID returns:

```console
{"result":"Error","message":"Analysis does not exist with id: df946130-a25c-4268-b2d0-e3ccc592f7cb"}
```

## Retrieving Analysis Reports

Once we've verified that the job with our UUID has finished, we can retrieve reports. To
receive the results, send a HTTP GET request with URI `/mythril/v1/analysis/${UUID}/issues`:

```console
$ curl -i -X GET https://api.mythril.ai/mythril/v1/analysis/$UUID/issues \
-H "Authorization: Bearer $MYTHRIL_API_KEY"
```
The returns:

```console
HTTP/1.1 200 OK
Access-Control-Allow-Origin: *
Content-Type: application/json; charset=utf-8
Date: Tue, 28 Aug 2018 21:27:05 GMT
ETag: W/"2-l9Fw4VUO7kr8CvBlt4zaMCqXZ0w"
Server: nginx/1.12.1
Strict-Transport-Security: max-age=15552000; includeSubDomains
X-Content-Type-Options: nosniff
X-DNS-Prefetch-Control: off
X-Download-Options: noopen
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
Content-Length: 2
Connection: keep-alive

[]
```

No issues were detected, so the result is an empty list `[]`.

However, for a real contract like this one:

```solidity
pragma solidity ^0.4.23;

contract IntegerOverflow {
    uint public count = 1955;

    function run(uint256 input) public {
        count *= input;
    }
}
```

Which produces the EVM bytecode:

```
"0x60806040526107a360005534801561001657600080fd5b5060e4806100256000396000f3006080604052600436106049576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806306661abd14604e578063a444f5e9146076575b600080fd5b348015605957600080fd5b50606060a0565b6040518082815260200191505060405180910390f35b348015608157600080fd5b50609e6004803603810190808035906020019092919050505060a6565b005b60005481565b806000808282540292505081905550505600a165627a7a72305820ebde511764d3e81b205e4cd886a3996c87262aff0d4aedbfc501ab93c761b2b80029"
```

You should get the following result (formatted with [jq](https://stedolan.github.io/jq/):


```json
[
  {
    "address": 174,
    "contract": "MAIN",
    "debug": "calldata_MAIN[4]: 0xf005c0ffff870000000000000000000000001fffffffffffffffffffffffbde7\nstorage_0: 0x7d18af89c36b8e2a88e90ad37012dedc916f009ecb9b9a648c567a6508469000\ncalldata_MAIN[0]: 0xa444f5e900000000000000000000000000000000000000000000000000000000\ncalldatasize_MAIN: 0x4\ncallvalue: 0x0\n",
    "description": "A possible integer overflow exists in the function `_function_0xa444f5e9`.\nThe addition or multiplication may result in a value higher than the maximum representable integer.",
    "function": "_function_0xa444f5e9",
    "title": "Integer Overflow",
    "type": "Warning"
  }
]
```

## Getting the Mythril API version number

If you want to see what the current Mythril API version string is, issue a HTTP GET request to
the URL `mythril/vi/version`:

```console
$ curl -X GET https://api.mythril.ai/mythril/v1/version
```

This will return a version string such as `v1.02` (you don't need to supply an API key in order to run this).


## More Information

You can download the [openapi specification](https://en.wikipedia.org/wiki/OpenAPI_Specification) for the Mythril API via `mythril/vi/openapi.yaml`:

```console
$ curl -X GET https://api.mythril.ai/mythril/v1/openapi.yaml
```

See also [Mythril API (v1)](https://mythril.ai/docs) and the [Mythril Home Page](https://mythril.ai/).
