## Circuit Breaker

┌────────────────┐    ┌────────────────┐    ┌───────────────┐    ┌────────────────┐
│ Microservice 1 ├───>│ Microservice 2 ├──> │ Microservice 3├───>│Microservice X  │
└────────────────┘    └────────────────┘    └───────────────┘    └────────────────┘

• What if one of the service is down or is slow ?
- Impacts entiner chain!

• Question:
- Can we return a fallback response if a service is down?
- Can we implement a Circuit Breaker pattern to reduce load?
- Can we retry requests in case of temporary failures?
- Can we implement rate limiting?


We can solve the above question using the cicuit breaker frameworks like Resilience4j, Netflix Hystrix etc.

Read more about circuit breaker
https://martinfowler.com/bliki/CircuitBreaker.html 

