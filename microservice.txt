### Microservice

"Small autonomous services that work together" - Sam Newman

"In short, the microservice architectural style is an approach to developing a single application as 
a suite of small services, each running in its own process and communicating with lightweight mechanisms, 
often an HTTP resource API. These services are built around business capabilities and independently deployable 
by fully automated deployment machinery. There is a bare minimum of centralized management of these services,
which may be written in different programming languages and use different data storage technologies."
- https://www.martinfowler.com/articles/microservices.html

• REST
• Small well chosen deployable units
• Cloud enabled



### Challenges of Microservices

• Configuration Management
• Dynamic Scale Up and Scale Down
• Visibility (monitoring, identify fault etc)
• Pack of Cards (fault tolerance)



### Advantage of Microservice architecture

• Quickly Adapt New Technology:
  C: When a system is build using microservice, different service can communicate with each other using simple
     messages. Each microservice can be build in different technologies. In future, some language, tool does
     the work more efficiently then new microservice can be build using it and integrate with the other microservice
     eaisly.

• Dynamic Scalling:
  C: Consider application like Amazon they don't have same amount of load all the time but in holiday season the load
     can be huge, so the load on the application will be lot on the holiday season then the rest oof the season. In
     such case, if the microservice are cloud enabled they can dynamically scale up and down based on the load.

• Faster Release Cycles:
  C: Smaller service are easy to develop and change the large monolith application, it is much eaiser to release
     microservice appliccaction compared to monolith applications. This means that featuree can be bring faster 
     in the market
