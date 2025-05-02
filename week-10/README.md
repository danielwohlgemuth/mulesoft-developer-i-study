# Week 10: Handling Errors

## Learning Goals
- Use On Error Continue and On Error Propagate to handle exceptions in flows.
- Define global error handlers for shared behavior (logging, alerts, fallback responses).
- Create custom error types and map internal errors to friendly API responses.
- Apply Try scopes for localized error control.
- Use reconnection strategies for transient system errors.

## Business Context
MuleCart has begun onboarding external clients and internal stakeholders are reviewing API logs. Errors need to be more predictable, consistent, and user-friendly. Your goal this week is to implement standardized error handling for API requests and ensure failures are clearly communicated — both internally and externally.

## Project Structure
```
/projects/week10-error-handling/
  /src/main/mule/
    - catalog-experience-api.xml
    - catalog-processing-flows.xml
    - catalog-error-handlers.xml      # New: global error definitions
    - global-config.xml
  /src/main/resources/
    - config/
        - application-dev.properties
  mule-artifact.json
  pom.xml
  README.md
```

## Use Cases & Error Handling Patterns

### 1. Global Error Handler (catalog-error-handlers.xml)
- Add a <global-error-handler> to:
    - Catch unexpected system exceptions (e.g. DB down)
    - Log technical details
    - Return consistent HTTP 500 with a friendly message

### 2. Flow-Specific Error Handling

- In catalog-processing-flows.xml, use On Error Continue for:
    - Recoverable issues (e.g. one bad product in bulk upload)
    - Log and continue batch or For Each execution
- Use On Error Propagate for:
    - Serious failures that must abort the request (e.g. missing DB connection)

### 3. Try Scope Example
- In GET /products/:id, wrap DB lookup in a Try scope
- If product not found, return a 404 error with custom JSON body
- If other DB error occurs, return 500 from global handler

### 4. Custom Error Types
- Create a PRODUCT_NOT_FOUND type and map to 404
- Define reusable error mappings in a Choice router within error handlers

### 5. Reconnection Strategies
- Configure reconnection on HTTP and DB connectors (e.g. 3 attempts with 1s delay)

## Workflow
- Add a global error handler file (catalog-error-handlers.xml) and import into global-config.xml.
- Refactor existing flows to use:
    - Try scopes around error-prone operations
    - On Error Continue and On Error Propagate as appropriate
    - Implement custom errors using Raise Error processor with metadata
    - Log errors to the console and structure JSON error responses like:
        ```json
        {
        "error": {
            "type": "PRODUCT_NOT_FOUND",
            "message": "The product with ID 1234 was not found."
        }
        }
        ```
- In your README:
    - Describe error handling philosophy (e.g. fail-fast vs. fail-soft)
    - Document all custom error types
    - Show example requests that trigger each type of error

