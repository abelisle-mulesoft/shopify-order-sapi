# Shopify Order System API
This repository contains a system API for unlocking Shopify order data. The Shopify Order System API (SAPI) is a reusable asset that enables developers to access Shopify order data without any need to learn the underlying systems. In other words, it provides a means of insulating developers from the complexity of integrating with Shopify.

## Table of Contents
1. [Technology Stack Overview](#technology-stack-overview)
2. [Implementation Overview](#implementation-overview)
3. [Instructions](#instructions)
4. [Sample Request Messages](#sample-request-messages)
5. [Reporting Issues](#reporting-issues)
6. [Additional Resources](#additional-resources)

## Technology Stack Overview
In the current revision, I implemented this system API using the following technology stack:
- MuleSoft Anypoint Studio 7.18
- Mule Server 4.7.0
- Shopify REST Admin API version 2025-01

Although not formally tested, you could easily use earlier versions of these components.

> [!WARNING]
> The Shopify's REST Admin API reference stated, "*the REST Admin API is a legacy API as of October 1, 2024. All apps and integrations should be built with the [GraphQL Admin API](https://shopify.dev/docs/api/admin-graphql).*" 

## Implementation Overview
In the current revision, the Shopify Order SAPI implements the following operations:

- `GET /orders` - Retrieve a list of orders from Shopify.
- `GET /orders/{orderId}` - Retrieve the order with the specified orderId from Shopify.
- `POST /orders` - Create a new order in Shopify.

I intentionally limited the current implementation, as the original requirement was limited to showing how to leverage the **Shopify REST Admin API** in the content of a proof of concept. 

As it is common practice at MuleSoft, I leveraged RAML to specify this API. I also utilized (RAML) API fragments to promote reusability where it made sense. Primarily for convenience and to make sharing the Anypoint Studio project easier, I included the RAML files in the project (`src/main/resources/api`) rather than having a dependency to its published specification in Anypoint Exchange.

I designed and organized the implementation using three Mule flows:
1. `shopify-order-sapi.xml` represents the interface.
2. `shopify-order-sapi-impl.xml` is the actual API implementation (e.g., business logic and rules).
3. `global.xml` contains all global configuration elements.

## Instructions
1. Download this repo or clone it to your Anypoint Studio workspace.
    ```sh
    git clone https://github.com/abelisle-mulesoft/shopify-order-sapi.git
    ```

2. Copy the properties template `src/main/resources/properties/mule-props.template.yaml`  to `src/main/resources/properties/mule-props-dev.yaml`. 

3. Edit the properties file `src/main/resources/properties/mule-props-dev.yaml` and at a minimum, configure the following properties:

   - `shopify.https.host` - the URL of your Shopify Store.
   - `shopify.https.port` - optionally, the port of your Shopify Store.
   - `shopify.admin_api.version` - the version of the Shopify REST Admin API.
   - `shopify.https.access_token` - your Shopify Store access token.

    Optionally, revise or update other properties as you see fit.

4. Compile and run the project in Anypoint Studio as a smoke test. Optionally, test the Shopify Order SAPI using the API Console in Anypoint Studio, or your preferred API testing tool (e.g., Postman).

## Sample Request Messages
I tested the Shopify Order SAPI using the following sample request message.
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

> :memo: As implied in the sample request message above, I created basic products in my Shopify store (i.e., without variants). Furthermore, I did not include taxes, and I used the product title when creating orders (instead of a SKU, for example).

## Reporting Issues
You can report new issues at this link https://github.com/abelisle-mulesoft/shopify-order-sapi/issues.

## Additional Resources
Following are references and additional resources:
- Shopify Admin API: https://shopify.dev/api/admin
- Shopify REST Admin API reference: https://shopify.dev/api/admin-rest
- Shopify REST Order API (version 2022-04): https://shopify.dev/api/admin-rest/2022-04/resources/order
