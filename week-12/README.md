# Week 12: Deploying and Managing APIs

## Learning Goals
- Deploy Mule applications to CloudHub using Runtime Manager.
- Use API Manager to apply security and traffic control policies.
- Configure auto-discovery to link a deployed app to an API definition.
- Create and deploy API proxies from Anypoint Platform.
- Monitor applications and APIs through Analytics and Logs.

## Business Context
MuleCart is ready for production. You’ll deploy it to the cloud, enforce rate-limiting and authentication, and enable real-time visibility into API usage and errors. This prepares the system for actual consumers and future scaling.

## Project Structure
```
/projects/week12-deployment/
  /src/main/mule/
    - catalog-experience-api.xml
    - catalog-processing-flows.xml
    - catalog-error-handlers.xml
    - global-config.xml
  /src/main/resources/config/
    - application-dev.properties
    - application-prod.properties
  mule-artifact.json
  pom.xml
  README.md
```

## Deployment & Management Tasks

### 1. Prepare for Deployment
- Add CloudHub-specific properties to application-prod.properties
- Use secure:: prefix for any sensitive values (e.g., DB credentials)
- Package the project as a deployable .jar using Anypoint Studio or mvn clean package

### 2. Deploy to CloudHub
- Log in to Runtime Manager
- Deploy the .jar with:
    - Correct environment
    - CPU/Memory allocation
    - Logging level set to DEBUG or INFO

### 3. Enable API Auto-Discovery
- In Anypoint Studio:
    - Set the api.id property for your API from API Manager
    - Add API Autodiscovery component to the main flow
- In API Manager:
    - Configure the API instance and link it to the deployed app using auto-discovery ID

### 4. Apply Policies
- In API Manager, apply:
    - Client ID enforcement for security
    - Rate Limiting (e.g., 1000 requests/hour per app)
    - Optional: CORS policy, IP whitelisting

### 5. Create & Deploy API Proxy
- If needed (e.g., for externally exposed APIs), create a proxy:
    - Upload the RAML spec
    - Use Anypoint CLI or Platform UI to deploy it
    - Route requests to the CloudHub-hosted backend

### 6. Monitor and Analyze
- Use API Analytics to view:
    - Usage patterns
    - Top consumers
    - Failed requests and error types
- Use Runtime Logs to debug CloudHub issues in real time

## README Highlights
- Include deployment instructions and config:
    - How to package and deploy to CloudHub
    - How to link to API Manager
    - API security policy settings
    - Example analytics views or links