# prompt

Analyze the selected API end-to-end and generate a Markdown document named `<API_NAME>_OVERVIEW.md`.

## Security Guidelines

* Do **not** reveal or copy any secrets from the codebase, including API keys, passwords, tokens, certificates, private keys, connection strings, or credentials.
* Mask or omit any sensitive configuration values.
* Focus only on application architecture, code flow, and implementation details.
* Do **not** make assumptions. If a detail cannot be determined from the code, explicitly state **"Not found in the analyzed code."**

---

# 1. API Overview

Provide a brief overview of the selected API.

Include:

* API endpoint
* HTTP method
* Purpose of the API
* Request DTO
* Response DTO
* Controller class and method

---

# 2. Complete Execution Flow

Trace the **entire execution flow** of this API by following the actual method calls across the codebase.

Do not stop at the Controller or Service layer.

Continue tracing until the final response is returned.

Include every significant step such as:

Client

↓

Controller

↓

Validation

↓

Service

↓

Helper/Utility methods

↓

Repository

↓

MongoDB

↓

Kafka Producer/Consumer

↓

External Clients

↓

Response Mapping

↓

Response

For every important step include:

* Class name
* Method name
* File name
* Approximate line number
* Short description of what happens

If a method invokes another internal method, continue tracing it until the flow ends.

---

# 3. Business Logic

Explain the business logic implemented by this API based **only** on the source code.

Describe:

* Validations performed
* Data transformations
* Decision points
* Important conditions
* Any calculations
* Any business rules that are explicitly implemented

If part of the logic is delegated to an external library or service and cannot be determined from the code, mention that instead of making assumptions.

---

# 4. MongoDB Usage

Identify every MongoDB interaction for this API.

Include:

* Database (if identifiable)
* Collection name(s)
* Repository used
* Entity/Document class
* Operations performed (find, insert, update, delete, aggregate, etc.)
* What data is stored
* What data is retrieved
* Which API step performs each operation

---

# 5. Kafka Flow

If Kafka is involved, explain:

* Whether this API is a Producer or Consumer
* Kafka topics used
* Message payload
* Where the message is published or consumed
* Which class and method performs the Kafka operation
* What happens after publishing or consuming the message

If Kafka is not used, explicitly mention that.

---

# 6. External Dependencies

Identify every external dependency or service used by this API (for example, Experian or any REST/HTTP client).

For each dependency explain:

* Why it is called
* Which class and method invoke it
* Request object
* Response object
* Error handling or retry mechanism (if present)

Do not infer behavior that is not visible in the code.

---

# 7. API Sequence Diagram

Generate a Mermaid sequence diagram showing the end-to-end request flow, including:

* Client
* Controller
* Service
* Repository
* MongoDB
* Kafka (if used)
* External Services (if used)
* Response

---

# 8. Summary

Provide a concise end-to-end explanation of how this API works.

The summary should enable a new developer to understand:

* The purpose of the API
* How the request flows through the application
* Which database collections are used
* Whether Kafka is involved
* Which external services are called
* The major classes responsible for the implementation

---

## Analysis Rules

* Inspect all related files, including Controller, Service, Repository, DTOs, Models, Configurations, Kafka components, Mongo repositories, Utilities, and External Clients.
* Follow the actual method call hierarchy instead of stopping at the first level.
* Reference important classes, methods, file names, and approximate line numbers wherever possible.
* Base every statement on the source code.
* If information cannot be determined from the code, explicitly state **"Not found in the analyzed code."**
* Do not speculate or invent missing implementation details.
