# ParaBank API Testing

API test automation practice using **Postman** and the [ParaBank demo REST API](https://parabank.parasoft.com/parabank/api-docs/index.html).

## Coverage

| User story | Request | Checks |
| --- | --- | --- |
| US-01 — Create Account | `POST /createAccount` | HTTP 200, valid account ID, customer ID, account type, initial balance |
| US-02 — Get Account by ID | `GET /accounts/{accountId}` | HTTP 200, account ID, customer ID, account type |
| US-02 — Invalid Account ID | `GET /accounts/99999999` | HTTP 400, account-not-found message |
| US-03 — Get Customer Accounts | `GET /customers/{customerId}/accounts` | HTTP 200, nonempty account list, account ownership |
| US-03 — Invalid Customer ID | `GET /customers/99999999/accounts` | HTTP 400, customer-not-found message |

**Current scope:** 5 requests and 16 Postman assertions. Responses are parsed from XML where necessary.

## Getting started

1. Import `ParaBankAPI.postman_collection.json` into Postman.
2. Open **ParaBank API Testing → Variables** and set the following values **locally**:

   | Variable | Set to |
   | --- | --- |
   | `baseUrl` | The ParaBank API base URL ending in `/parabank/services/bank` |
   | `customerId` | An existing demo customer's ID |
   | `accountId` | An existing account ID belonging to that customer |

3. Run the requests individually and review **Test Results**. For customer/account IDs, consult the [Swagger API docs](https://parabank.parasoft.com/parabank/api-docs/index.html) and the `login` / customer-accounts endpoints.

> **Note:** The exported Collection intentionally leaves variable values blank. Fill them in Postman before sending a request. Do not commit real user credentials or secrets.

## Notes

- `POST /createAccount` creates a **new account each time it is sent**. It is not a read-only test.
- The Create Account tests currently cover **CHECKING** accounts (`newAccountType=0`) with an expected initial balance of `0`, based on the observed demo behavior.
- The negative tests use a deliberately invalid sample ID (`99999999`). They assert the error behavior observed in the demo API. If server behavior changes, review the assertions.
- The ParaBank environment is public demo infrastructure; shared data and service behavior may change.

## Tools

- Postman
- JavaScript assertions via the Postman sandbox
- ParaBank REST API (XML responses)
