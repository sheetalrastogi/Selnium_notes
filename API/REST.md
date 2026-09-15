REST Architecture (Representational State Transfer)

REST (Representational State Transfer) is an architectural style for designing distributed, scalable, and loosely coupled web services. It was introduced by Roy Fielding in his doctoral dissertation in 2000.

REST-based services typically use HTTP protocols and exchange data in formats such as JSON or XML.

REST is an architectural style for building distributed web services where resources are identified by URIs and manipulated using standard HTTP methods such as GET, POST, PUT, PATCH, and DELETE. REST follows key principles like stateless communication, client-server separation, cacheability, layered architecture, and a uniform interface, making APIs scalable, maintainable, and easy to integrate.


### HTTP Methods

REST uses standard HTTP verbs.

- GET 	=> Retrieve data.	=> 200
- POST	=> Create resource.	=> 201 Created
- PUT	=> Update entire resource.
- PATCH	=> Partial update.
- DELETE=> Delete resource.

### REST Constraints

REST architecture is based on six constraints.

**1. Client-Server**

Benefits:
- Independent development
- Better scalability
- Easier maintenance

**2. Stateless**
Each request contains everything needed to process it.  Server does not maintain session state.

- Good
	GET /customers/100
	Authorization: Bearer token
	Every request contains authentication details.

- Bad
	Server remembers previous request context

Benefits:
- Scalability
- Reliability
- Load balancing

**3. Cacheable**
Responses should indicate whether they can be cached.

Example:
Cache-Control: max-age=3600


Benefits:
- Faster response
- Reduced server load

**4. Uniform Interface**
Consistent API design.

Examples:
GET    /customers
GET    /customers/100
POST   /customers
PUT    /customers/100
DELETE /customers/100


Benefits:
- Easier to learn
- Easier integration

**5. Layered System**
Client doesn't know whether it is talking directly to the server or through intermediaries.

```text
Client
   |
Load Balancer
   |
API Gateway
   |
Application Server
   |
Database
```

Benefits:
- Security
- Scalability
- Separation of concerns

**6. Code on Demand (Optional)**
Server can send executable code to clients.

Example:
- JavaScript


### Common HTTP Status Codes
**Success**
- 200 OK
- 201 Created
- 202 Accepted
- 204 No Content

**Client Errors**
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 409 Conflict

**Server Errors**
- 500 Internal Server Error
- 502 Bad Gateway
- 503 Service Unavailable
- 504 Gateway Timeout


### When testing APIs using RestAssured, typical QA View:

```text
RestAssured
      |
      v
REST Endpoint
      |
      +--> Business Layer
      |
      +--> Database
      |
      +--> External APIs
               |
               +--> WireMock (Mocked)
```

**Typical validations**:
- Request payload validation
- Response validation
- Schema validation
- Authentication/Authorization
- Error handling
- Performance checks
- Contract testing
- Retry and timeout behavior


## REST vs SOAP

| Feature | REST | SOAP |
|----------|------|------|
| Protocol | HTTP | HTTP / SMTP / JMS |
| Data Format | JSON, XML | XML Only |
| Performance | Faster | Slower |
| Learning Curve | Easy | Complex |
| Stateless | Yes | Can be Stateful |
| Used In | Microservices, Web APIs | Enterprise Legacy Systems |




