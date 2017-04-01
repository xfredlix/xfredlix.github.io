# REST API
- REpresentational State Transfer
- 6 constraints: Uniform Interface, Stateless, Cacheable, Client-Server, Layered System, Code on Demand (optional)
- Violating any constraint other than Code on Demand means the service cannot strictly be referred to as RESTful, ex: three-legged OAUTH2
- Compliance with REST constraints allow: scalability, simplicity, modifiability, visibility, portability, reliability

### Resource Based
- Things instead of actions
- Nouns instead of verbs
- URI identifies resource in each request using HTTP verb
- Multiple URIs can refer to the same resource
- Representation is separate from resource

### Representation
- How resources get manipulated
- Represents part of the resource state, which is transferred between client and server
- Typically JSON or XML
- Example:
  resource: person (todd)
  service: contact information (get)
  representation: name, address, phone number
  JSON or XML

### Uniform Interface
- Defines the interface between client and server
- Use HTTP verbs (GET, POST, PUT, DELETE)
- Clients deliver state via body contents, query-string parameters, request headers and the requested URI (the resource name). Services deliver state to clients via body content, response codes, and response headers. This is technically referred-to as hypermedia

### Stateless
- Server contains no client state
- Each request is self descriptive and contains enough information for the server to process the message
- If there is state, it is kept on the client side

### Client Server
- RESTful architecture is a client server architecture
- Assume a disconnected system
- Separation of concerns
- Uniform interface is the link between the two

### Cacheable
- Server responses (representations) are cacheable
- Implicitly: if it's not denoted
- Explicitly: server specifies
- Negotiated: client server negotiates

### Layered System
- Could have multiple layers of software/hardware
- Improves scalability

### Code on Demand
- Server can temporarily extend client by transferring logic to the client
- Executable JavaScript snippets
- Optional constraint

### GET
- GET parameters are included in the URL
- Used for fetching documents
- Has a maximum URL length
- OK to cache
- Shouldn't change the server

### POST
- POST parameters are included in the body
- Used for updating data
- No max length
- Not OK to cache
- OK to change the server
