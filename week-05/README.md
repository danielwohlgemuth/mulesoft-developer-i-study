# Week 5: Structuring Mule Applications

## Learning Goals
- Understand how to organize Mule applications into multiple files and folders.
- Use global configuration files for shared resources (e.g. error handling, HTTP listeners).
- Use properties files for environment-specific configuration.
- Create modular flows and subflows to separate concerns and enable reuse.
- Pass data and control between flows using Flow Reference and VM connectors.

## Business Context
MuleCart’s product catalog API is growing in complexity. To support new features like promotions, inventory, and personalization, the application must be refactored for modularity. This week you’ll restructure the implementation to use clean separation of concerns, reuse logic, and set the stage for environment-based deployment.

## Project Structure
```
/projects/week05-application-structure/
  /src/main/mule/
    - catalog-experience-api.xml                # Entry point flows
    - catalog-processing-flows.xml              # Subflows for logic
    - global-config.xml                         # Listeners, error handlers, shared configs
  /src/main/resources/
    - product-dataset.json
    - config/
        - application-dev.properties
        - application-prod.properties
  mule-artifact.json
  pom.xml
  README.md
```

## Refactor Targets

### Global Configuration File
- Move:
    - HTTP Listener config
    - error handler definitions
    - object store config (if used)
- Add global default error handling strategy if not already in place

### Main Flow File (catalog-experience-api.xml)
- Only contains:
    - Listener + router
    - Flow references or logic orchestration
    - No business logic or transformation

### Supporting Flow File (catalog-processing-flows.xml)
- Add subflows:
    - lookupProductById
    - filterProductsBySearchQuery
    - getFeaturedProducts
- Include all Transform Message logic here

### Properties and Application Configuration
- Replace hardcoded values (like port, basePath, etc.) with ${config.property}
- Create application-dev.properties for local testing (e.g. http.port=8081)
- Modify mule-artifact.json to use dev profile by default

### Workflow
- Move reusable components and error strategies into global-config.xml
- Extract all business logic from experience flows into named subflows
- Replace inline transformations with references to reusable subflows
- Configure mule-artifact.json and application-dev.properties for environment-aware builds
- Test end-to-end flow behavior to ensure functionality remains intact
- In your README:
    - Document structure and rationale for file breakdown
    - List the configuration properties used and how to override them
    - Describe how to add a new flow cleanly following this structure