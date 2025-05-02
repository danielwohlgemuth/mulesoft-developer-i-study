# Week 11: Debugging and Testing with MUnit

## Learning Goals
- Write MUnit tests for individual flows using mocks and assertions.
- Inspect and debug Mule events with logger statements and breakpoints.
- Validate payloads, variables, and attributes in test assertions.
- Use before/after test scaffolding for repeatable test environments.
- Understand how to simulate external services with mocked processors.

## Business Context
MuleCart is beginning to grow its engineering team. To ensure reliability, you need to make the platform testable. This week, you’ll create unit tests for key API flows (e.g., GET /products/:id, GET /products) and simulate error conditions, mocked responses, and validate transformations.

## Project Structure
```
/projects/week11-testing-debugging/
  /src/main/mule/
    - catalog-experience-api.xml
    - catalog-processing-flows.xml
    - catalog-error-handlers.xml
    - global-config.xml
  /src/test/munit/
    - get-product-by-id-test.xml
    - get-all-products-test.xml
    - error-handling-test.xml
  /src/main/resources/config/
    - application-dev.properties
  mule-artifact.json
  pom.xml
  README.md
```

## Use Cases & Test Scenarios

### 1. GET /products/:id (Happy Path)
- MUnit test mocks DB response
- Asserts:
    - HTTP status = 200
    - Payload contains id, name, price
    - Logs expected values at debug level

### 2. GET /products/:id (Not Found)
- Mock DB result as empty
- Asserts:
    - HTTP status = 404
    - Payload contains custom error JSON with PRODUCT_NOT_FOUND

### 3. GET /products (Multiple Products)
- Mock DB to return list
- Asserts:
    - Payload size matches expected
    - Each item matches format (based on DataWeave logic)

### 4. Error Handling
- Simulate a DB connector failure (e.g., raise CONNECTIVITY error)
- Assert that:
    - Global error handler is invoked
    - Response status = 500 with friendly message
    - Log entry includes error trace

### 5. Logging & Debugging
- Add meaningful Logger steps in main flows:
    - Before/after transformation
    - On error
- Use breakpoints in Anypoint Studio to walk through an event during local testing

## Workflow
- Add MUnit dependencies to the project (via pom.xml or Studio UI).
- Create test files inside /src/test/munit/ with:
    - Mock When to replace connector calls
    - Set Event to provide input payloads
    - Assert That to check output
- For each scenario:
    - Simulate input
    - Mock dependencies (e.g. DB, HTTP)
    - Assert final payload or attributes
- In your README:
    - List each test case and what it covers
    - Describe your testing strategy (e.g., unit vs integration scope)
    - Explain how to run tests in Studio or via Maven CLI