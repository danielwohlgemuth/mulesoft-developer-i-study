# Week 4: Accessing and Modifying Mule Events

## Learning Goals
- Understand the structure of a Mule event: payload, attributes, and variables.
- Use Set Variable, Set Payload, and Transform Message components to enrich or alter event data.
- Access and modify event attributes from HTTP requests or other sources.
- Create and use flow variables to pass state or data between steps in a flow.

## Business Context
The MuleCart frontend team needs dynamic behavior in the Product Catalog Experience API. For example, a search request should return filtered results based on query parameters. This requires logic in the flow that inspects the incoming request, sets variables, and builds a customized response.

You’ll refactor the Experience API implementation from Week 3 to:
- Read query parameters
- Set and use variables for intermediate logic
- Update payloads dynamically using DataWeave expressions

## Project Structure
```
/projects/week04-event-modification/
  /src/main/mule/
    - catalog-experience-api.xml
  /src/main/resources/
    - examples/
        - product-dataset.json
  README.md
```

## Event Use Cases

### Use Case 1 – Search Products
- Read query param q from event attributes
- Filter a hardcoded product list using containsIgnoreCase(payload.name, q)
- Set a flow variable searchResults and return it as the new payload

### Use Case 2 – Return Product Details
- Read path parameter id from attributes
- Filter the product list by id
- If not found, return a 404-style response with a custom error payload

### Use Case 3 – Log Request Metadata
- Extract request headers and method from event attributes
- Log a formatted message like:
    - "GET /products/search?q=laptop from IP 192.168.1.1"

## Workflow
- In catalog-experience-api.xml, locate flows for:
    - GET /products
    - GET /products/{id}
    - GET /products/search

### Modify each using:
- Set Variable to store search criteria, product subsets
- Transform Message to build filtered payloads with DataWeave
- Access attributes.queryParams and attributes.uriParams for logic
- Add a Logger at the start of each flow to output useful metadata
- Replace static Transform Message components with dynamic logic based on input
- In your README:
    - Explain how event structure was used
    - Include key examples of DataWeave used to manipulate data
    - List caveats and what’s mocked vs. real