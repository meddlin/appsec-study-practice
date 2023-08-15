# AppSec Study Practice

Diagrams I've used to document and study where common AppSec vulnerabilities typically lie within 
an application architecture. This isn't meant to be 1 vuln == 1 line of code. Rather, this details 
what pieces of architecture are involved in mitigating a type of vulnerability.

**Example: SQL Injection**

While using parameterized queries is commonly referred to as the mitigation against SQL injection, 
an injection from client to database reveals multi-layer problems.

- ❌ Use parameterized SQL queries
- ✅ Parameterized queries (ORM), server + client-side input validations

## Scenarios

### OWASP Top 10

Shows possible problem areas for each of the OWASP Top 10 vulnerability categories.

### Logging Structure

Scenario: an application has a key-value store, an API layer, and a web front-end. Then we detail
other pieces of supporting architecture that could be deployed, and determine what potential 
threats may appear across this architecture.