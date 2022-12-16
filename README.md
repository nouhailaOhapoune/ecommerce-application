# Ecommerce application avec Java JEE
Objectif :  
Créer une application basée sur une architecture micro-service qui permet de gérer les factures 
contenant des produits et appartenant à un client.

## Partie Backend :
<img width="412" alt="video2" src="https://user-images.githubusercontent.com/82985419/208115624-72d543f7-3a95-44f1-978b-def96e9b83fd.png">

### Les dépendences de Spring Boot utilisées pour les micro-services:
Lombok, pour créer une application web spring MVC: Spring Web et Rest Repositories, pour le SQL : Spring Data JPA et H2 DATABASE, 
Pour faire le monitoring des micro-services: Spring Boot Actuator,
Pour Spring Cloud Discovery: Eureka Discovery Client
Pour faire communiquer les micro-services : OpenFeign,
et aussi la Spring HATEOAS.


### Les dépendences de Spring Boot utilisées pour Discovery:
Eureka Server et  Spring Boot Actuator

### Les dépendences de Spring Boot utilisées pour Gateway:
Spring Boot Actuator et Eureka Discovery Client


### 1.La création du micro-service customer-service qui permet de gérer les client:

###### Création de 2 packages:

-> Package entities qui contient la classe  Customer et l'interface  CustomerProjection
-> Package repository qui contient l'interface CustomerProjection

###### Présentation de la base de données customers-db (h2-console): 

<img width="274" alt="h211" src="https://user-images.githubusercontent.com/82985419/208118971-c1e925e8-5c16-4901-8a55-fa1a39c55df4.png">
 
 ###### Le résultat sous forme de fchier JSON de micro-service CUSTOMER-SERVICE: 

<img width="514" alt="customer-service" src="https://user-images.githubusercontent.com/82985419/208116502-4f11d913-fd8c-48da-afd0-4f84ec0f5101.png">

### 2.La création du micro-service inventory-service qui permet de gérer les produits:

###### Création de 2 packages:

-> Package entities qui contient la classe Product
-> Package repository qui contient l'interface ProductRepository

###### Présentation de la base de données customers-db (h2-console): 

<img width="298" alt="h233" src="https://user-images.githubusercontent.com/82985419/208122936-4244cce8-e858-4808-bc46-f4ff6ed77379.png">

 ###### Le résultat sous forme de fchier JSON de micro-service CUSTOMER-SERVICE:
 
 <img width="572" alt="inventory-service" src="https://user-images.githubusercontent.com/82985419/208123123-d18dad1b-1133-47de-b887-46e9e2094762.png">

### 3.La création de la Spring cloud Gateway avec une configuration statique:

Pour faire la configuration des propriétés de la Gateway,
on crée un fichier yml dans le package resources , on l'a appelé "application .yml"
Et pour les routes ,on les ajoute dans application .yml ou bien dans le fichier  GatewayApplication.java en créant l'objet routes de RouteLocator.

 ###### Le résultat sous forme de fchier JSON de la Gateway  avec une configuration statique:
 
 -> Pour le micro-service CUSTOMER-SERVICE:

<img width="519" alt="gateway-statique1" src="https://user-images.githubusercontent.com/82985419/208125559-012dd818-485a-42ab-a4c2-bbabf99c9b35.png">


-> Pour le micro-service INVENTORY-SERVICE:

<img width="506" alt="gateway-statique2" src="https://user-images.githubusercontent.com/82985419/208125796-070cffad-e550-402c-872a-cda19983e18e.png">
### 4. La création de l'annuaire Eureka Discovery Service:

On ajoute l'annotation @EnableEurekaServer qui permet d'activer le service discovery.
Et si on écrit dans le navigateur : http://localhost:8761 
on obtient le résultat suivant

<img width="899" alt="discovery-service" src="https://user-images.githubusercontent.com/82985419/208130063-f1b5579a-e97b-4b3a-9569-d3e7e700078c.png">

### 5. La configuration dynamique des routes de la gateway:

En utilisant le service Discovery , on crée l'objet dynamicRoutes de la classe DiscoveryClientRouteDefinitionLocator. Donc on peut communiquer avec les micro-services seulement avec leurs noms .

###### Par exemple:
 
<img width="539" alt="gateway-dynamique" src="https://user-images.githubusercontent.com/82985419/208133028-5d88e24c-4a98-4814-80a9-6de52c512842.png">

### 6. La création du service de facturation Billing-Service en utilisant Open Feign:
Ce micro service est réservé à la facturation , et il relie les micro-services CUSTOMER-SERVICE et INVENTORY-SERVICE avec la relation ### ManyToMany .

###### Création de 5 packages:
-> entities : pour les 2 classes(Bill et ProductItem) et l'interface BillProjection pour le frontend.
-> model : pour les 2 classes Customer et Product
-> repository : pour BillRepository et ProductItemRepository
-> service : CustomerRestClient et ProductRestClient pour la communication avec les micro-services.
-> web : BillRestController qui fait la création d'un web service de type REST avec un restController (@RestController)














