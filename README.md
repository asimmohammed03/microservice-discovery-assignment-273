**Microservice Service Discovery using Eureka**


**Project Overview**


This project demonstrates Service Discovery in a Microservices Architecture using:

-Spring Boot
-Netflix Eureka
-Spring Cloud LoadBalancer
-Maven

The system consists of:
-Eureka Server → Service Registry
-Service-A → Two running instances (Ports 8081 & 8082)
-Client-Service → Discovers Service-A dynamically and performs client-side load balancing

The client calls Service-A using its service name, not a hardcoded port. Eureka resolves available instances automatically.

**Architecture**
**Architecture Explanation**

-Both Service-A instances (8081 & 8082) register with the Eureka Server.

-The Eureka Server (8761) maintains a registry of all active services.

-The Client-Service (8090) calls Service-A using:

http://service-a/hello

-Eureka returns available instances.

-Spring Cloud LoadBalancer selects one instance randomly.

-The response alternates between ports 8081 and 8082.

**How to Run the Application**
Prerequisites
-Java 17
-Maven
-IntelliJ IDEA (or any IDE)
-Internet connection (for Maven dependencies)

**Step 1** — Start Eureka Server

Open the eureka-server project and run:
EurekaServerApplication

Verify in browser:
http://localhost:8761

**Step 2**— Start Service-A (Two Instances)

Run first instance normally:
ServiceAApplication
Port: 8081

Run second instance using VM option:
-Dserver.port=8082

Now the Eureka dashboard should show:

SERVICE-A  UP (2)
<img width="1454" height="827" alt="Screenshot 2026-03-18 at 3 38 15 PM" src="https://github.com/user-attachments/assets/bcdc581d-3e15-4283-b197-8599d4a7e91a" />

**Step 3 **— Start Client-Service

Open the client-service project and run:

ClientServiceApplication

It runs on:

http://localhost:8090

**Test Load Balancing**

Open in browser:

http://localhost:8090/call

Refresh multiple times.
You will see alternating responses:

Hello from Service-A running on port 8081
Hello from Service-A running on port 8082

<img width="389" height="125" alt="Screenshot 2026-03-18 at 3 38 45 PM" src="https://github.com/user-attachments/assets/1a72d502-2694-4f5f-aba5-bb97c279e609" />


This confirms:

-Service Discovery is working

-Multiple instances are registered

-Client-side load balancing is functioning

-Random instance selection is occurring

Important Code Snippet (Client-Side Discovery)
restTemplate.getForObject("http://service-a/hello", String.class);

Notice:

-No hardcoded port

-No localhost usage

-Service name is used

-Eureka handles instance resolution
**Technologies Used**

-Java 17

-Spring Boot 3.x

-Spring Cloud Netflix Eureka

-Spring Cloud LoadBalancer

-Maven

-REST APIs

