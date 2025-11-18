# Microservices Configuration Repository

Ce dépôt contient les fichiers de configuration centralisés pour tous les microservices de notre architecture, gérés par Spring Cloud Config Server.

## 🚀 Vue d'ensemble

Dans une architecture de microservices, la gestion de la configuration peut devenir complexe. Ce dépôt résout ce problème en centralisant toutes les configurations dans un seul endroit, permettant ainsi une gestion et un déploiement facilités. Le Spring Cloud Config Server lit les fichiers de ce dépôt et les fournit aux microservices clients au démarrage ou lors d'un rafraîchissement à chaud.

## 📁 Structure des Fichiers

Chaque microservice (ainsi que les composants Spring Cloud comme la Gateway) a son propre fichier de propriétés :

-   `application.properties`: Contient les propriétés globales ou par défaut qui s'appliquent à tous les microservices.
-   `microservice-commandes.properties`: Configurations spécifiques au service de gestion des commandes.
-   `microservice-produits.properties`: Configurations spécifiques au service de gestion des produits.
-   `spring-cloud-gateway.properties`: Configurations spécifiques à l'API Gateway.

## 🔑 Accès et Sécurité

Ce dépôt est configuré pour être accessible par le `spring-cloud-config-server`. Si ce dépôt était privé, des informations d'authentification (nom d'utilisateur et Personal Access Token GitHub) seraient configurées dans le `application.properties` du Config Server.

## ⚙️ Comment ça marche ?

1.  Le `spring-cloud-config-server` démarre et est configuré pour pointer vers l'URL de ce dépôt Git.
2.  Les microservices clients (comme `microservice-commandes`) incluent la dépendance `spring-cloud-starter-config` et sont configurés via leur `bootstrap.properties` pour se connecter au Config Server.
3.  Au démarrage, chaque client demande ses propriétés au Config Server en utilisant son `spring.application.name`.
4.  Le Config Server récupère le fichier correspondant (`<nom_du_service>.properties`) depuis ce dépôt et le renvoie au client.
5.  Grâce à `@RefreshScope` et l'Actuator `/refresh` endpoint, les configurations peuvent même être rechargées à chaud sans redémarrage de l'application.

---

*Ce dépôt fait partie d'un projet de microservices développé pour le module JEE.*
