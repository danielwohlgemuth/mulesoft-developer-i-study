# Week 6: Using Connectors

## Learning Goals
- Use the Database Connector to interact with a relational database.
- Read from and write to a PostgreSQL (or other) DB using parameterized queries.
- Use Transform Message to map query results to API response formats.
- Combine multiple data sources within a flow using Enrich or Scatter-Gather.

## Business Context
The product catalog API currently uses a hardcoded JSON dataset. This week, you’ll replace that with a connection to a real PostgreSQL database that stores products, categories, and featured items. This will allow the frontend to fetch live product data and enable updates later in the project.

## Project Structure
```
/projects/week06-db-connector-integration/
  /src/main/mule/
    - catalog-experience-api.xml
    - catalog-processing-flows.xml
    - global-config.xml
  /src/main/resources/
    - config/
        - application-dev.properties
    - db/
        - setup.sql                    # DB schema and seed data
  mule-artifact.json
  pom.xml
  README.md
```

## Setup: PostgreSQL Database
Sample tables:
```sql
CREATE TABLE products (
  id UUID PRIMARY KEY,
  name TEXT,
  description TEXT,
  category_id UUID,
  is_featured BOOLEAN,
  price NUMERIC
);

CREATE TABLE categories (
  id UUID PRIMARY KEY,
  name TEXT
);
```

Add seed data for products and categories in setup.sql.

## API Changes
Modify these flows to use the DB connector:
- GET /products
    → Query all products: SELECT * FROM products
- GET /products/{id}
    → Parameterized query: SELECT * FROM products WHERE id = :id
- GET /categories
    → Join categories: SELECT * FROM categories
- GET /products/featured
    → Filtered query: SELECT * FROM products WHERE is_featured = TRUE
- GET /products/search?q=shoes
    → Add SQL ILIKE filter on name or description

## Workflow
- Use Database Config to set up PostgreSQL connection in global-config.xml.
- Store connection details in application-dev.properties:
    ```properties
    db.host=localhost
    db.port=5432
    db.user=mule
    db.password=mule123
    db.name=mulecart
    ```
- Replace product list logic with Database connector query operations.
- Use Transform Message to format SQL query results into the API response structure.
- Add logic to return 404 if GET /products/{id} yields no result.
- In your README:
    - Show sample queries and example responses
    - Document how to run the DB and seed the data
    - Include curl/Postman examples for endpoints