# Ecommerce application avec Java JEE

### Objectif :  

Créer une application basée sur une architecture micro-service qui permet de gérer les factures 
contenant des produits et appartenant à un client.

## Partie Backend :

<img width="412" alt="video2" src="https://user-images.githubusercontent.com/82985419/208115624-72d543f7-3a95-44f1-978b-def96e9b83fd.png">

### Les dépendences de Spring Boot utilisées pour les micro-services :

Pour les getters et les setters: Lombok.

Pour créer une application web spring MVC: Spring Web et Rest Repositories.

Pour le SQL : Spring Data JPA et H2 DATABASE. 

Pour faire le monitoring des micro-services: Spring Boot Actuator.

Pour Spring Cloud Discovery: Eureka Discovery Client.

Pour faire communiquer les micro-services : OpenFeign.

et aussi la Spring HATEOAS.


### Les dépendences de Spring Boot utilisées pour Discovery :
Eureka Server et  Spring Boot Actuator

### Les dépendences de Spring Boot utilisées pour Gateway :
Spring Boot Actuator et Eureka Discovery Client


### 1.La création du micro-service customer-service qui permet de gérer les client :

###### Création de 2 packages :

-> Package entities qui contient la classe  Customer et l'interface  CustomerProjection

-> Package repository qui contient l'interface CustomerProjection

###### Présentation de la base de données customers-db (h2-console) : 

<img width="274" alt="h211" src="https://user-images.githubusercontent.com/82985419/208118971-c1e925e8-5c16-4901-8a55-fa1a39c55df4.png">
 
 ###### Le résultat sous forme de fichier JSON de micro-service CUSTOMER-SERVICE : 

<img width="514" alt="customer-service" src="https://user-images.githubusercontent.com/82985419/208116502-4f11d913-fd8c-48da-afd0-4f84ec0f5101.png">

### 2.La création du micro-service inventory-service qui permet de gérer les produits :

###### Création de 2 packages :

-> Package entities qui contient la classe Product

-> Package repository qui contient l'interface ProductRepository

###### Présentation de la base de données products-db (h2-console) : 

<img width="298" alt="h233" src="https://user-images.githubusercontent.com/82985419/208122936-4244cce8-e858-4808-bc46-f4ff6ed77379.png">

 ###### Le résultat sous forme de fichier JSON de micro-service INVENTORY-SERVICE :
 
 <img width="572" alt="inventory-service" src="https://user-images.githubusercontent.com/82985419/208123123-d18dad1b-1133-47de-b887-46e9e2094762.png">

### 3.La création de la Spring cloud Gateway avec une configuration statique :

Pour faire la configuration des propriétés de la Gateway,
on crée un fichier yml dans le package resources , on l'a appelé "application .yml"

Et pour les routes ,on les ajoute dans application .yml ou bien dans le fichier  GatewayApplication.java en créant l'objet routes de RouteLocator.

 ##### Le résultat sous forme de fchier JSON de la Gateway  avec une configuration statique :
 
  ###### -> Pour le micro-service CUSTOMER-SERVICE :

<img width="519" alt="gateway-statique1" src="https://user-images.githubusercontent.com/82985419/208125559-012dd818-485a-42ab-a4c2-bbabf99c9b35.png">

###### -> Pour le micro-service INVENTORY-SERVICE :

<img width="506" alt="gateway-statique2" src="https://user-images.githubusercontent.com/82985419/208125796-070cffad-e550-402c-872a-cda19983e18e.png">

### 4. La création de l'annuaire Eureka Discovery Service :

On ajoute l'annotation @EnableEurekaServer qui permet d'activer le service discovery.

Et si on écrit dans le navigateur :
###### http://localhost:8761 

On obtient le résultat suivant : 

<img width="899" alt="discovery-service" src="https://user-images.githubusercontent.com/82985419/208130063-f1b5579a-e97b-4b3a-9569-d3e7e700078c.png">

### 5. La configuration dynamique des routes de la gateway :

En utilisant le service Discovery , on crée l'objet dynamicRoutes de la classe DiscoveryClientRouteDefinitionLocator. Donc on peut communiquer avec les micro-services seulement avec leurs noms .

###### Par exemple :
 
<img width="539" alt="gateway-dynamique" src="https://user-images.githubusercontent.com/82985419/208133028-5d88e24c-4a98-4814-80a9-6de52c512842.png">

### 6. La création du service de facturation Billing-Service en utilisant Open Feign :

Ce micro service est réservé à la facturation , et il relie entre les micro-services CUSTOMER-SERVICE et INVENTORY-SERVICE.

<img width="513" alt="classes" src="https://user-images.githubusercontent.com/82985419/208178960-bf7c7656-4561-47b0-ab3a-6d83b9e11ebb.png">


###### Création de 5 packages:

-> entities : pour les 2 classes(Bill et ProductItem) et l'interface BillProjection pour le frontend.

-> model : pour les 2 classes Customer et Product.

-> repository : pour BillRepository et ProductItemRepository.

-> service : CustomerRestClient et ProductRestClient pour la communication avec les micro-services.

-> web : BillRestController qui fait la création d'un web service de type REST avec un restController (@RestController)

###### Présentation de la base de données bill-db (h2-console) :

 -----> ProductItem table:
 
<img width="371" alt="bill-db2" src="https://user-images.githubusercontent.com/82985419/208180237-83d17f9e-4218-4d07-bd93-fb04f8487b0a.png">

------> Bill table:

<img width="377" alt="16 12 2022_21 07 03_REC" src="https://user-images.githubusercontent.com/82985419/208180513-3b11a4fc-8e88-4f0d-bda6-c7ad6a3068d8.png">


 #### Le résultat sous forme de fichier JSON :
 
 En utilisant le RestController , on a pu créer un web service qui relie tous les micro-services ,et il fait une facture complète qui contient customerId et une liste des  productsItems avec chaque productItem est pour un seul produit (Bill+Customer+ProductItemProduct).
 
 <img width="561" alt="billing-service" src="https://user-images.githubusercontent.com/82985419/208182492-ba8b6ae7-4a98-49d7-91fe-c321b3a1d581.png">

 
##### Après l'ajout du micro-service BILLING-SERVICE ,Spring Eureka devient comme ça :

<img width="760" alt="discovery2" src="https://user-images.githubusercontent.com/82985419/208179444-be8c131d-666b-48e4-a847-080493e65a9d.png">


## Partie Frontend (Le nom de dossier: ecom-web-app) :

### 7. La création d'un client Web Angular:

On a utilisé le framework de Javascript Angular et le framework de CSS Bootstrap pour créer un client Web Angular.

 ##### ---> app.component.html:
 
 Création du navbar
 
 <img width="374" alt="16 12 2022_21 53 56_REC" src="https://user-images.githubusercontent.com/82985419/208187220-7343b9ad-2a79-4469-8621-ee1aead78e9d.png">


##### ---> CustomersComponent (http://localhost:4200/customers) :

<img width="405" alt="16 12 2022_21 56 04_REC" src="https://user-images.githubusercontent.com/82985419/208187507-6a925c0f-3758-4ab0-a83b-56f475ee0161.png">

Mais pour traiter les factures des clients on a ajouter un bouton pour chaque client pour gérer ces commandes.

<img width="431" alt="16 12 2022_21 58 02_REC" src="https://user-images.githubusercontent.com/82985419/208187996-4e3e4d93-c631-44b2-b569-4fd07f1b0c34.png">


##### ---> ProductsComponent (http://localhost:4200/products) :

<img width="459" alt="16 12 2022_21 50 40_REC" src="https://user-images.githubusercontent.com/82985419/208186954-93020ab0-1bc3-4083-8c92-08bc443c8d3a.png">















