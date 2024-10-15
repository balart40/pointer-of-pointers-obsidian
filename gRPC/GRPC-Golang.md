---
tags:
  - Go
  - Golang
---
#### Microservices

There is a need to agree on:
- API to exchange data
- data format
- error patterns
- many other things
#### Building API  is hard
- Payload size
- Latency
- Scalability
- Load Balancing
- Language interop
- Auth, monitoring, log

RPC: Remote Procedure Call

Advanced
Practice
Theory

## gRPC Internals DeepDive
### gRPC: Protocol Buffers and Language Interoperability

Define message
Define services

Example:

```
syntax = "proto3";  
  
package greet;  
  
option go_package = "github.com/Clement-Jean/grpc-go-course/greet/proto";  
  
message GreetRequest {  
  string first_name = 1;  
}  
  
message GreetResponse {  
  string result = 1;  
}  
  
service GreetService {  
  rpc Greet(GreetRequest) returns (GreetResponse);  
  rpc GreetManyTimes(GreetRequest) returns (stream GreetResponse);  
  rpc LongGreet(stream GreetRequest) returns (GreetResponse);  
  rpc GreetEveryone(stream GreetRequest) returns (stream GreetResponse);  
  rpc GreetWithDeadline(GreetRequest) returns (GreetResponse);  
};
```

Proto needs less space than json
Efficiency over Json
- Less cpu intensive
- Is faster
- mobile and microcontrollers

Supported official languages
- C# (Main Implementation)
- C++
- Dart
- Go (Main Implementation)
- Java  (Main Implementation)
- Kotlin
- Node
- Objective-C
- PHP
- Python
- Ruby
- C (Main Implementation)

Efficient Serialization and Deserialization

### HTTP2

Most of the web works with HTTP1

**HTTP1**
- Open connection, make request and wait for response and close connection
- TCP connection per request
- Plaintext headers
- request/response

**HTTP2**
- One TCP connection
- server push
- multiplexing
- Binary
- More secure SSL
- less chatter
- less bandwidth
- more security
- Open source
### GRPC APIs

- Unary
	- One request from client
	- One response from server
- Server streaming
	- HTTP2
	- One request from client
	- Multiple responses from server
- Client streaming 
	- One or multiple request
	- Server one response
- BI directional streaming
	- One or multiple requests
	- One or multiple responses
### Scalability in gRPC
- **Server:** Async
- **Client:** Async or blocking

### Security in gRPC
- Schema-based serialization 
- Easy SSL certificate initialization
- Interceptors for Auth
### gRPC vs REST

| gRPC             | **REST**               |
| ---------------- | ---------------------- |
| Protocol Buffers | Json                   |
| HTTP2            | HTTP1                  |
| Streaming        | Unary                  |
| Bi directional   | Client->Server         |
| Free design      | GET/POST/UPDATE/DELETE |
### why use gRPC
- Code generation
- More secure
- streaming
- API oriented

