# Week 7: Processing Records

## Learning Goals
- Use For Each, Batch Job, and Async scopes to process collections.
- Apply streaming strategies and understand how record processors differ in behavior.
- Understand when to use Batch Job vs. For Each based on use case.
- Use VM queues or JMS to decouple flows for asynchronous processing.
- Persist processed records and log successes/failures.

## Business Context
The MuleCart product team needs a way to bulk upload product data (e.g., during seasonal onboarding of new inventory) and process records efficiently. In the future, this may also support importing inventory files or synchronizing products with a supplier feed.

This week, you’ll implement a bulk product upload API that accepts a file (e.g. CSV or JSON array) and processes each record to be inserted or updated in the product database.

## Project Structure
```
/projects/week07-record-processing/
  /src/main/mule/
    - catalog-experience-api.xml
    - catalog-processing-flows.xml
    - catalog-batch-flows.xml         # New: batch job definition
    - global-config.xml
  /src/main/resources/
    - config/
        - application-dev.properties
    - examples/
        - bulk-products.json
  mule-artifact.json
  pom.xml
  README.md
```

## API Addition
- Endpoint: POST /products/bulk
- Input: JSON array of product objects
- Behavior:
    - Validate each product structure
    - Insert or update each product record
    - Return a processing summary

## Processing Strategy
- Use For Each scope for lightweight inline record handling
- Use Batch Job to enable chunking, streaming, and error handling
- Demonstrate Async scope by calling a logging subflow in parallel
- Optionally simulate JMS queue with VM Connector to offload processing to another flow

## Workflow
- In catalog-experience-api.xml, add POST /products/bulk endpoint.
- In catalog-processing-flows.xml, create a subflow to:
    - Validate product fields (e.g. name, price, category)
    - Set up payload for DB insertion or update
- In catalog-batch-flows.xml, define a Batch Job with:
    - Input phase to split the array
    - Batch steps to insert records into the DB
    - On-complete phase to log and summarize results
- Optionally add a VM queue between the POST endpoint and the batch trigger to simulate async processing
- Add Logger or Object Store to track failures or duplicates
- In your README:
    - Show example input and curl command
    - Explain when and why to use each record processing strategy
    - Include screenshots or logs showing batch summary