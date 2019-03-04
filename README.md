# Cloud-Native Applications  with Microservices Architectures | Red Hat DO092

This are my notes about the course *Developing Cloud-Native Applications with Microservices Architectures*. By Burr Sutter, developer advocate from Red Hat.

How to combine different frameworks and tools into a microservices architecture that fits your organizational needs.

The source files are in: https://github.com/burrsutter/kube4docker

## 1 - Microservices Overview: What and Why?

#### Your Jorney to Microservices
1) Re-org to DevOps
2) Self-service, on demand, elastic, infra as code
3) Automation puppet, chef, ansible and/or kubernets
4) Continuous integration & Continuous delivery Deployment pipeline
5) Advanced deplyment techniques (blue/green deployment or canary deployment)
*) be like Super Cool Silicon Valley DotCom Startup \o/

https://martinfowler.com/bliki/MicroservicePrerequisites.html

If you're not mature enough, and you're not big enough, 
and you not skilled enough, you probably don't want to get the microservices ride.
|_ How many days/weeks to provision a new VM?
|_ Who is on the pager for production app outage?
|_ Who is the own of the application? The person who architect and created it?
|_ phoenix vs snowflake?

#### Books to read:
- The Phoenix project
- Refactoring databases - Livro por Scott W. Ambler
- Migrating to Microservice databases - Edson Yanaga

#### Microservice Principles/Characteristics
1. Deployment *Independence* - updates to an individual microservice have no negative impact to any other component of the system. Optimzes for replacement;
2. Organized around *business* capabilities
3. *Products* not projects
4. *API* Focused
5. *Smart* endpoints and dumb pipes
6. Decentralized Governance
7. Decentralized Data Management (for example each team choose your db)
8. Infrastructure Automation (infra as code)
9. Design for failure
10. Evolutionary Design
@burrsutter


## 2 - API: Building and Deploying a Microservice (and demonstration)

The easiest part is make a API. The other things are complex.

Hot Tip: Fabric8 Maven Plugin. For instrumenting your spring boot, wf swarm, vert.x or java ee project's pom.xml.
Hot Tip 2: go to https://start.spring.io/ and just add web dependencies

#### Main commands
* mvn clean compile package
* docker build -t burr/myvertex:v1 .
* docker run -it -p 8080:8080 burr/myvertex:v1
* curl http://192.168.99.101:8080/hello

* kubectl get namespaces
* kubectl create -f ./kubedemo-namespace.yaml
* kubectl --namespace=kubedemo create -f kubedemo-deployment.yaml --record --validate=false
* kubectl get pods --namespace=kubedemo

* kubectl --namespace=kubedemo expose deployment --port=8080 myvertx --type=LoadBalancer
* kubectl --namespace=kubedemo scale deployment myvertx --replicas=3

**update**
* docker build -t burr/myvertx:v2 .
* kubectl --namespace=kubedemo set image deployment/myvertx myvertx=burr/myvertx:v2

**others**

show history
* kubectl --namespace=kubedemo rollout history deployment myvertx

undo 
* kubectl --namespace=kubedemo rollout undo deployment/myvertx

run spring
* mvn spring-boot:run

configure fabricate
* mvn io.fabric8-maven-plugin:3.3.5:setup 

deploy fabricate
* mvn fabric8:deploy

## 3- Discovery & Invocation

How does Service A find and then invoke service B??

It's possible use NetFlixOSS Eureka and Ribbon.

When you are inside the cluster, just refer to it by its service name.

For exemple:
producer -> http://producer:8080/

````
String url = "http://producer:8080/";
ResponseEntity<String> response  = restTemplate.getForEntity(url, String.class);
System.out.println(response.getBody());
````
## 4 - Microservices Patterns (and demonstration)

With microservices you always have to think about failure.

When a failure ocours, you need think in the fallback scenario.

**API Gateway**

Agregate the businics logic on the server-side, also reducing network traffic to the client.

**Chaining**

The requests will be deep. It means to call A, B, C and D. On fail happens a cascading fail.

**Mixed**

The requests will be assincronous/sincronous.

## 5 - Circuit Breakers (and demonstration)

Netflix OSS gave us a specific circuit breaker and bulkhead implementation called Hystrix.
