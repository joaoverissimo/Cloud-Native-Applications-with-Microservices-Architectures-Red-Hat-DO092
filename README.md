# Cloud-Native Applications  with Microservices Architectures | Red Hat DO092

This are my notes about the course *Developing Cloud-Native Applications with Microservices Architectures*. How to combine different frameworks and tools into a microservices architecture that fits your organizational needs.

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



