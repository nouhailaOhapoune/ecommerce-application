# ecommerce-application
Objectif :  
Créer une application basée sur une architecture micro-service qui permet de gérer les factures 
contenant des produits et appartenant à un client.
## Partie Backend :
<img width="212" alt="video2" src="https://user-images.githubusercontent.com/82985419/208115624-72d543f7-3a95-44f1-978b-def96e9b83fd.png">

### Les dépendences de Spring Boot utilisées pour les micro services:
Lombok, pour créer une application web spring MVC: Spring Web et Rest Repositories, pour le SQL : Spring Data JPA et H2 DATABASE, 
Pour faire le monitoring des micro-services: Spring Boot Actuator,
Pour Spring Cloud Discovery: Eureka Discovery Client
Pour faire communiquer les micro-services : OpenFeign,
et aussi la Spring HATEOAS.

### Les dépendences de Spring Boot utilisées pour Discovery:
Eureka Server et  Spring Boot Actuator
### Les dépendences de Spring Boot utilisées pour Gateway:
Spring Boot Actuator et Eureka Discovery Client


### 1.La création micro-service customer-service qui permet de gérer les client:


