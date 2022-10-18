## Solving Microservice Challanges with Spring Cloud and other tools.

• Bounded Context:

  C: Instead of one big monolith application, we would build five small microservices or ten, how do you
     identify the boundry of the each of the microservices and how do we decide what a microservice do and
     shoud not do. For, new application is is quite difficult to seperate out the boundry.

  S: Deciding boundry is a evolutionary process, it is not something that we get at the first place. 
     Try to follow the domain driven design based on the knowledge that you have at that point of time.
     

• Configuration Management:
  
  C: In microservice, multiple service configuration needs to be maintained. It would be tedious to maintain
     configuration of each microservice in different place.

  S: Spring-cloud-config-server provides an approach to store all the configuration of all the environment
     of all the microservice in Git repository. Help us to keep configuration in one place which makes it
     easy to maintain the configuration for all microservices.  
     

• Dynamic Scale Up and Scale Down:

  C: Multiple instance of a service may need to be added in and removed out as load and distribute the
     load among different instances. 

  S: With Naming server like Eureka, all the instance of microservices are registered in the naming server
     Eureka. Naming server has two important feature one is service registration and second one is service
     discovery. Naming server provides URL information of the instance of a different service. We also need
     client-side load balncer like Ribbion. We also need Feign to write simple REST client.

  E: In this example below, CurrencyCalculatroService can ask Eureka naming server, give me the current instance of 
     CurrencyExchangeService and the naming server would provide URL of the current CurrencyExchangeService,
     this helps to establish dynamic relation between CurrencyCalculatorService and CurrencyExchangeService
     by providing the URL of the active instance of CurrencyExchangeService.

    Regarding client-side load balancig with Ribbion, CurrencyCalculatorService hosts Ribbon and Ribbon 
    would make sure the load is equally distributed.

            
     Digram: 1.0
                                ┌───────────────────────────┐
                                │Currency Calculator Service│
                                └────────────┬──────────────┘
                                             │
                                             │           ┌─────────────┐
                                             │     ─ ─ ─ │Naming Server│
                                             │   /       └─────────────┘
                                             │  /
                                         ┌───┴───┐
                      ┌──────────────────┤Ribbion├──────────────────┐
                      │                  └───┬───┘                  │
                      │                      │                      │
                      │                      │                      │
    ┌─────────────────┴───────┐    ┌─────────┴───────────────┐    ┌─┴───────────────────────┐
    │CurrencyExchangeService1 │    │CurrencyExchangeService2 │    │CurrencyExchangeService3 │
    └─────────────────────────┘    └─────────────────────────┘    └─────────────────────────┘



• Visibility and Monitoring:
 
  C: When the functionality is distributed among different microservices, it would difficult to identify where
     the bug is. we also need automatically identify different microservices which are down, slow, are with 
     less disk-space etc. 

  S: We need to have a centeralized log to track which request or microservice caused the problem. We can achieve
     it using Spring Cloud Sleuth which assigns ID to request across multiple components and we can use Zipkin
     disriubuted tracing to ttracce a request across multiple componens. 


• Pack of Cards: 

  C: If microservice are not well-designed it can be like a pack of cards. Basically in microservice architecture
     one service calling another and another calling another and if one of the microservice goes down then like
     a pack of card building, if one fails then it can bring all the microservice can collapse.

  S: We need well-design microservice architecture and it should be fault tollerant. We can achieve it 
     providing fallback options. We can use Hystrix to achieve it.



`Note`: Also read microservice-spring-cloud-v2.md
