# Week 2: API Design (OAS)

## Learning Goals
- Learn to define APIs using OpenAPI Specification (OAS) 3.0 specification syntax.
- Design RESTful endpoints using resources, methods, parameters, and response types.
- Structure a OAS project with data types, examples, and traits for reuse.
- Validate and test APIs using Mocking Service in Anypoint Design Center.

## Business Context
You will expand MuleCart’s Product Catalog API by fully designing the Experience API in RAML. This API will be used by the web and mobile teams to display products, search, and retrieve details, so it must be clean, well-documented, and reusable.

This layer is also the public-facing contract that will later be backed by implementation logic in MuleSoft.

## Project Structure
```
/projects/week-02/
  - catalog-experience-api.json
  - dataTypes/
    - Product.json
    - Category.json
  - examples/
    - product-example.json
    - category-example.json
  - traits/
    - pagination.json
    - error-response.json
  README.md
```

### Endpoints:
- `GET /products` – Returns a paginated list of products
- `GET /products/{id}` – Returns detailed information about a specific product
- `GET /products/featured` – Returns promoted products for the homepage
- `GET /products/search?q=...` – Full-text product search
- `GET /products/categories` – Returns all product categories

### Data Types:
- Product: includes id, name, price, description, image, inventoryStatus
- Category: includes id, name, description

### Traits:
- paginated: query parameters like page, limit
- error-response: standardized error response with code, message, timestamp

## Workflow
- Define the main OAS spec for the Experience API using Anypoint Design Center.
- Create modular OAS components:
    - Reusable data types (Product, Category)
    - Common traits (e.g. paginated, secured)
    - Realistic examples in JSON
- Mock the API and test each endpoint with sample requests/responses.
- Document and annotate endpoints (descriptions, response codes, media types).
- Publish to Exchange and link it to the API portal created in Week 1.
- In your README:
    - Explain design decisions (e.g. why traits were used)
    - Outline usage for frontend/mobile devs