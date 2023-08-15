Focus:
- distributed systems
- Design
- threat vectors
- why items were chosen
- knowing how data flows


Requirements
- 300TB of key-value, read-only data
- keys are small
  - keys: 32-bytes data
  - values: 100-bytes data
- 10TB disks
  - 50MB random read rates
- 32GB of RAM

- assuming 4-, 6-, or 8-core CPUs?

- Solution on commodity hardware
- Can't use "cloud-centric" solution choices (i.e. BigQuery)







Why multi-node database?

- Reason: Increased random access performance
- 300TB of data is a lot for a single server to access all at once
    - 30 x 10TB disks
    - Problem: could overload disk head seek times, if data requested isn't sequential

- Reason: increased redundancy
  - We don't want a single point of failure for our entire database


Why multiple instance of API?

- handle more connections to database
- split user demand over webservers



Why API Gateway?

- single point for authN/authZ
  - reduces attack surface for authentication attacks
  - instead of updating, maintaining this service on every API endpoint

- enable serving multiple versions of the API


Why multiple front-end web servers?
- ability for A/B testing
- serve multi-regional users







### Hosts

- Server/webservers
  - OS: https://www.debian.org/

- API Gateway
  - KrakenD: https://www.krakend.io/open-source/



### OWASP Resources

- OWASP Secure Headers Project: https://owasp.org/www-project-secure-headers/

- OWASP API Security Top 10: https://owasp.org/www-project-api-security/


### Other Resources

- Storing user passwords/credentials: https://nakedsecurity.sophos.com/2013/11/20/serious-security-how-to-store-your-users-passwords-safely/
  - avoid DES, MD5, SHA-1
  - explains hashing, salting needs
  - "hash-stretching"


- Cache busting: https://www.keycdn.com/support/what-is-cache-busting
  - Good web development technique
  - Also, can force updates when we patch XSS vulns


CORS vs CSP: https://www.devonblog.com/security/difference-between-cors-and-csp-security-headers/
- (Cross-origin request sharing vs. Content-security policy)
- CORS is about data sharing/communication between domains
- CSP is about defining what content can run on the domain
- further reading: https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP