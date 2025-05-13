# Week 3: API Implementation Interfaces

## Learning Goals
- Manually implement a REST API in MuleSoft using APIkit based on a OAS specification.
- Understand how APIkit Routers map requests to flows automatically.
- Implement mocked or partial logic for endpoints using flow components and Transform Message.
- Learn to synchronize changes between the OAS spec and implementation in Anypoint Studio.

## Business Context
You will implement the Product Catalog Experience API that was designed in Week 2. This is the first functional API that the frontend team can call. Initially, the implementation will use mocked or static responses, but will follow the real contract to ensure the structure is production-ready.

## Project Structure
```
/projects/week03-product-api-implementation/
  /src/main/mule/
    - catalog-experience-api.xml
  /src/main/resources/
    - examples/
        - product-example.json
        - category-example.json
  catalog-experience-api.json
  pom.xml
  README.md
```

## API Implementation
- Endpoints implemented (same as in OAS):
  - GET /products
  - GET /products/{id}
  - GET /products/featured
  - GET /products/search
  - GET /products/categories

### Mock Behavior:

Use Transform Message to return static JSON from examples for now.

Apply basic logic: `search` filters the static list, `featured` returns a subset.

## Workflow
- Import the OAS into Anypoint Studio and generate scaffolding using APIkit Router.
- For each endpoint:
  - Connect to a Transform Message component that outputs a static response.
  - Store responses in separate JSON files or inline for simplicity.
  - Set up HTTP Listener, configure base path, and test each route in Postman or the API Console.
- Ensure endpoint consistency with the OAS spec — update OAS or implementation if mismatched.
- In your README:
  - Describe how APIkit maps flows
  - Explain current mock implementation and future data source plans
  - Include test curl/Postman commands for each route