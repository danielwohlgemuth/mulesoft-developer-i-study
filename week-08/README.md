# Week 8: DataWeave Transformations

## Learning Goals
- Use DataWeave to convert between data formats (JSON, XML, Java, CSV).
- Apply core functions for filtering, mapping, coercion, and formatting.
- Define and reuse variables, functions, and modules.
- Create transformations that handle nested or complex data structures.
- Externalize and reuse DataWeave scripts.

## Business Context
MuleCart needs to support multiple client platforms (mobile, web, external affiliates), each requiring a slightly different data shape. This week, you’ll build reusable transformations to shape product data for these clients and introduce versioned formatting options.

## Project Structure
```
/projects/week08-dataweave-transformations/
  /src/main/mule/
    - catalog-experience-api.xml
    - catalog-processing-flows.xml
    - global-config.xml
  /src/main/resources/
    - config/
        - application-dev.properties
    - dwl/
        - transform-product.dwl
        - format-product-compact.dwl
        - format-product-detailed.dwl
  mule-artifact.json
  pom.xml
  README.md
```

## Use Cases & Transformations

### 1: Core Product Normalization (transform-product.dwl)
- Accepts raw DB rows
- Normalizes field names, applies types (e.g. price to number), and adds computed fields (e.g. isDiscounted)
- Reused across multiple flows

### 2: Format: Compact View (format-product-compact.dwl)
- Used by mobile app
- Fields: id, name, price

### 3: Format: Detailed View (format-product-detailed.dwl)
- Used by product detail page
- Fields: id, name, description, price, category, isFeatured, availability

### 4: Conditional Versioning
- Add ?format=compact or ?format=detailed to GET /products/:id
- Use Choice router or when condition in DataWeave to apply correct formatting

## Workflow
- Refactor all existing Transform Message steps to use centralized .dwl scripts in the /dwl/ folder.
- Add transform-product.dwl as the default shape transformer.
- In the GET /products/:id and /products, inspect the query param format, and apply:
    - Compact or Detailed formatter
- Use functions to encapsulate reusable logic (e.g. currency formatting, tag generation).
- Add tests or examples to show input/output transformations.
- In your README:
    - Document each .dwl file’s purpose
    - Include a table showing what fields are returned for each format
    - Show how to add a new format or transform version in the future