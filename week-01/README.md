# Week 1: Application Networks & API-Led Connectivity

## Learning Goals
- Understand the principles of API-led connectivity and how to design with System, Process, and Experience API layers.
- Identify the role of an Application Network in decoupling systems and enabling reuse.
- Learn how to use OpenAPI Specification (OAS) to define APIs, mock endpoints, and publish them to Anypoint Exchange.
- Practice organizing an API project for discoverability and collaboration (portal, tags, documentation).

## Business Context
MuleCart is establishing an API-led backend architecture to power its eCommerce operations. To support flexibility, reuse, and scalability, you'll design the Product Catalog API suite using MuleSoft's recommended System–Process–Experience API model.

## Project Structure
```
/projects/week-01/
  /experience-api/
    - catalog-experience-api.json
  /process-api/
    - catalog-process-api.json
  /system-api/
    - catalog-db-system-api.json
  README.md
```

## API Layers

### System API – Product Database API
Interfaces directly with the internal product database (simulated with static data or mock).
- `GET /products` – List all products
- `GET /products/{id}` – Retrieve product by ID
- `GET /categories` – List product categories

### Process API – Catalog Aggregator API
Combines and filters product data for business needs.
- `GET /products/available` – Return only active/in-stock products
- `GET /products/by-category?category={name}` – Filter by category

### Experience API – Storefront Product API
Tailored for the web/mobile store frontend.
- `GET /products/public` – Minimal product data (name, price, image)
- `GET /products/featured` – Featured or promoted products for homepage

## Workflow
1. Design OAS specifications for each API layer using Anypoint Design Center.
2. Use mocking service to simulate responses and allow parallel frontend/backend development.
3. Publish APIs to Exchange with proper documentation and tags (e.g., System, Process, Experience).
4. Create an API portal for the Experience API with usage instructions for web/mobile teams.
5. Add a README that explains:
    - API-led design reasoning
    - Layer responsibilities
    - Future integration points (e.g., search, promotions)