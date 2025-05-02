# Week 9: Routing Events

## Learning Goals
- Use Choice routers to route messages based on payload content or attributes.
- Apply Scatter-Gather to call multiple flows/services in parallel and merge results.
- Validate incoming requests and handle fallback logic with Validation and Default routes.
- Route based on header values, query parameters, or user roles.

## Business Context
As MuleCart expands, different client applications (admin dashboard, mobile app, affiliate API) require different responses. You’ll now implement dynamic flow routing and conditional processing based on request context, such as user roles, format type, or even A/B testing scenarios.

## Project Structure
```
/projects/week09-routing-events/
  /src/main/mule/
    - catalog-experience-api.xml
    - catalog-routing-flows.xml        # New: routes & conditional logic
    - catalog-processing-flows.xml
    - global-config.xml
  /src/main/resources/
    - config/
        - application-dev.properties
  mule-artifact.json
  pom.xml
  README.md
```

## Use Cases & Routing Logic

### 1: Role-Based Routing
- For GET /products/:id, use a Choice router to:
    - Return compact view for anonymous/mobile users
    - Return detailed view for authenticated/admin users
- Simulate role via a custom HTTP header: X-User-Role: admin

### 2: Dynamic Recommendations via Scatter-Gather
- GET /products/:id/recommendations
- Use Scatter-Gather to call:
    - "Related by category"
    - "Frequently bought together"
    - "Trending in this category"
- Merge and return all recommendation types

### 3: API Version Routing
- Route requests to different flows or transformations based on a query parameter: ?v=1 or ?v=2
- Default to latest version if param is missing

### 4: Request Validation
- Use Validation module to enforce that required parameters are present in GET /search?q=...
- Return 400 with a useful message if validation fails

## Workflow
- Create a new catalog-routing-flows.xml to separate routing logic from core data flows.
- In catalog-experience-api.xml, define endpoints that delegate to conditional routers.
- Use Choice, Scatter-Gather, and Validation to control the flow path based on:
    - Header (X-User-Role)
    - Query param (?v=1)
    - Payload content
- Use Transform Message after Scatter-Gather to merge results cleanly.
- Handle default or fallback paths with default otherwise conditions in Choice routers.
- In your README:
    - Show how to simulate different routing paths with curl/Postman
    - Include before/after routing examples
    - Document assumptions (e.g. how roles are determined)