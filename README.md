# Shopify Order System API
This repository contains a system API for unlocking Shopify order data. The Shopify Order System API is a reusable asset that enables developers to access Shopify order data without any need to learn the underlying systems. In other words, it provides a means of insulating developers from the complexity of integrating with Shopify.

## Table of Contents
1. [Technology Stack Overview](#technology-stack-overview)
2. [Implementation Overview](#implementation-overview)
3. [Instructions](#instructions)
4. [Sample Request Messages](#sample-request-messages)
5. [Reporting Issues](#reporting-issues)
6. [Additional Resources](#additional-resources)

## Technology Stack Overview
We implemented this system API using the following technology stack:
- MuleSoft Anypoint Studio 7.11
- Mule Server 4.3.0
- Shopify REST Admin API version 2022-04

Although not formally tested, you could easily use earlier versions these components.

## Implementation Overview
As of this writing, the Shopify Order System API implements a single operation for creating orders in a Shopify store. We limited the current implementation intentionally, as the requirement was to show how to leverage the Shopify REST Admin API in the content of a proof of concept. However, you could easily extend it to create, retrieve, update, and delete orders in a Shopify store.

As it is common practice at MuleSoft, we leverage RAML to specify our API. We also utilized (RAML) API fragments to promote reusability where it made sense. Primarily for convenience and to make sharing the Anypoint Studio project easier, we included the RAML files in the project (`src/main/resources/api`) rather than having a dependency to its published specification in Anypoint Exchange.

We designed and organized the implementation using three Mule flows:
1. `shopify-order-sapi.xml` represents the interface.
2. `shopify-order-sapi-impl.xml` is the actual API implementation (e.g., business logic and rules).
3. `global.xml` contains all global configuration elements.

## Instructions
1. Download this repo or clone it to your Anypoint Studio workspace.
    ```sh
    git clone https://github.com/abelisle-mulesoft/shopify-order-sapi.git
    ```

2. Edit `src/main/resources/configuration.yaml` and configure the following properties:
   - `shopify.https.host` - the URL of your Shopify Store.
   - `shopify.https.port` - the port of your Shopify Store.
   - `shopify.admin_api.version` - the version of the Shopify REST Admin API.
   - `shopify.https.access_token` - your Shopify Store access token.
    
    <br/>
    Optionally, revise or update other properties as you see fit.

<br/>
3. Compile and run the project in Anypoint Studio as a smoke test. Optionally, test the Shopify Order System API using the API Console in Anypoint Studio, or your preferred API testing tool (e.g., Postman).

## Sample Request Messages
We tested and demoed the Shopify Order System API using the following sample request message.
```json
{
  "customer": {
    "firstName": "Paul",
    "lastName": "Norman",
    "email": "paul.norman@mail.com",
    "phone": "+16135551111"
  },
  "email": "paul.norman@example.com",
  "phone": "+16135551111",
  "billingAddress": {
    "firstName": "Paul",
    "lastName": "Norman",
    "address1": "PO Box 212",
    "city": "Drayton Valley",
    "state": "Alberta",
    "country": "Canada",
    "zip": "T0E 0M0"
  },
  "shippingAddress": {
    "firstName": "Paul",
    "lastName": "Norman",
    "address1": "2259 Park Ct",
    "address2": "APT 5",
    "city": "Drayton Valley",
    "state": "Alberta",
    "country": "Canada",
    "zip": "T0E 0M0"
  },
  "lineItems": [
    {
      "title": "12-1/2 Thickness Planer With Three Knife Cutter-Head",
      "price": 549,
      "quantity": 1
    }
  ]
}
```

> :memo: As implied in the sample request message above, we created basic products for our Shopify (i.e., without variants). Furthermore, we did not include taxes and used the product title when creating orders.

## Reporting Issues
You can report new issues at this link https://github.com/abelisle-mulesoft/shopify-order-sapi/issues.

## Additional Resources
Following are references and additional resources:
- Shopify Admin API: https://shopify.dev/api/admin
- Shopify REST Admin API reference: https://shopify.dev/api/admin-rest
- Shopify REST Order API (version 2022-04): https://shopify.dev/api/admin-rest/2022-04/resources/order
