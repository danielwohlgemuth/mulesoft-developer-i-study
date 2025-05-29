# Week 2: API Design (OAS)

There are no [mixins or traits](https://github.com/OAI/Overlay-Specification/issues/38) in OpenAPI 3.0 compared to RAML, but there is an [Overlay Specification](https://github.com/OAI/Overlay-Specification) that allows you to extend OpenAPI 3.0 by defining rules that can act like mixins.

An alternative is to use references to avoid code duplication. The format is `$ref: <pathToFile>/#<pathToSchema>`. For example, if you have a schema defined in `dataTypes/Product.json` and you want to use it in `catalog-experience-api.json`, you can use `$ref: dataTypes/Product.json#/components/schemas/Product`.
