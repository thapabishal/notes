### Load balancing
                        ┌─────────────────────────────┐
                        │ CurrencyConversionService   │
                        └────────────┬────────────────┘
                                     │
                                     ▼
                        ┌─────────────────────────────┐      ┌────────────────┐
                        │        LoadBalancer         │----->│  NamingServer  │
                        └─────────────────────────────┘      └────────────────┘
                            /         |              \
                           /          |               \
                          /           |                \
                         /            |                 \
                        /             |                  \
┌─────────────────────────┐  ┌─────────────────────────┐  ┌────────────────────────┐
│CurrencyExchangeService1 │  │CurrencyExchangeService2 │  │CurrencyExchagneService3│
└─────────────────────────┘  └─────────────────────────┘  └────────────────────────┘
 port:8000                    port:8001                    poort:8002




Problem:
We want CurrencyConversionService dynamically call different instance of CurrencyExchangeService
which are running in port 8000, 8001, 8002. We want automatically discover different instance of 
CurrencyExchangeService. We don't want to hard code url of the CurrencyExchangeService in CurrencyConversionService
because there can be new instances of CurrencyExchangeService or existing instance can go down. 

Solution:
To fix the above problem, we need service registry or naming server. In a microservice architecture, all the instance of 
a services would register itself with a service registry. 


E.g If a instace of CurrencyConversion Microservice wants to talk with CurrencyExchangeMicroService then it would ask naming server
or service regsitry URL of the CurrencyExchange.



┌──────────────────────────────────────────────┐  ┌───────────────────────────────────────────┐   ┌───────────────────────────────────────────────┐
│                                              │  │                                           │   │                                               │
│    ┌───────────────────────────────────────┐ │  │ ┌───────────────────────────────────────┐ │   │  ┌───────────────────────────────────────┐    │
│    │     CurrencyConversion Microservice   │ │  │ │     CurrencyExchange Microservice     │ │   │  │            XYZ  Microservice          │    │
│    └───────────────────────────────────────┘ │  │ └───────────────────────────────────────┘ │   │  └───────────────────────────────────────┘    │
│        |              |              |       │  │     |              |              |       │   │      |              |              |          │
│    ┌──────────┐   ┌──────────┐  ┌──────────┐ │  │ ┌──────────┐   ┌──────────┐  ┌──────────┐ │   │  ┌──────────┐   ┌──────────┐  ┌──────────┐    │
│    │Instance-1│   │Instance-2│  │Instance-X│ │  │ │Instance-1│   │Instance-2│  │Instance-X│ │   │  │Instance-1│   │Instance-2│  │Instance-X│    │
│    └──────────┘   └──────────┘  └──────────┘ │  │ └──────────┘   └──────────┘  └──────────┘ │   │  └──────────┘   └──────────┘  └──────────┘    │
│                                              │  │                                           │   │                                               │
│                                              │  │                                           │   │                                               │
└────────────────────────┬─────────────────────┘  └────────────────────┬──────────────────────┘   └────────────────────────┬──────────────────────┘
                         │                                             │                                                   │
                         │                                             │                                                   │
                         │                                             │                                                   │
                         │                                             ▼                                                   │
                         │                                                                                                 │
                         │                               ┌─────────────────────────┐                                       │
                         │                               │                         │                                       │
                         └────────────────────────────►  │      Naming Server      │  ◄────────────────────────────────────┘
                                                         │     Service Registry    │
                                                         └─────────────────────────┘
