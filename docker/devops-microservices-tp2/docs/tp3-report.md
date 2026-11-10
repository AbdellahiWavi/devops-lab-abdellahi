RAPPORT TP3 – Docker Networking et Docker Compose

Nom : Abdellahi Elwavi

Réponses aux questions du rapport

Q1. Comparaison entre le réseau bridge par défaut et un bridge personnalisé
- Le réseau bridge par défaut est créé automatiquement par Docker.
- Un réseau bridge personnalisé permet la résolution automatique des noms des conteneurs via Docker DNS.
- Il offre une meilleure isolation et une gestion plus simple des communications entre services.

Q2. DNS de service et utilisation de http://product-service:8001
Docker Compose crée un DNS interne permettant à un service de joindre un autre par son nom. Ainsi, Order Service accède à Product Service avec l’adresse http://product-service:8001. L’utilisation de localhost serait incorrecte car localhost désigne le conteneur lui-même.

Q3. Explication des éléments de compose.yaml
- services : définit les conteneurs de l’application.
- build : indique comment construire l’image Docker.
- ports : publie les ports du conteneur vers l’hôte.
- environment : définit les variables d’environnement.
- networks : connecte les services à un même réseau.

Q4. Pourquoi utiliser build context : . ?
Le contexte de construction correspond à la racine du projet. Les Dockerfile.reference utilisent des fichiers situés dans plusieurs dossiers du projet. Le contexte « . » rend tous ces fichiers accessibles lors du build.

Q5. Différence entre docker compose up -d, stop et down
- docker compose up -d : construit et démarre les services en arrière-plan.
- docker compose stop : arrête les conteneurs sans les supprimer.
- docker compose down : arrête et supprime les conteneurs ainsi que les réseaux créés par Compose.
Par défaut, down ne supprime ni les images ni le code source.

Q6. Rôle et limite de depends_on
La directive depends_on impose un ordre de démarrage des services. Cependant, elle ne garantit pas qu’un service soit totalement prêt à recevoir des requêtes HTTP.

Q7. Comportement lors de l’arrêt de Product Service
Lorsque Product Service est arrêté, Order Service reste actif mais ne peut plus récupérer les informations produits nécessaires à la création d’une commande. Les requêtes échouent jusqu’au redémarrage de Product Service.

Q8. Vérification du DNS et inspection du réseau Compose
- docker network inspect <network>
- docker compose exec order-service python -c "import socket; print(socket.gethostbyname('product-service'))"
Ces commandes permettent de vérifier la résolution DNS et la configuration réseau.

Conclusion
Docker Compose simplifie le déploiement d’applications composées de plusieurs microservices. Grâce aux réseaux Docker et au DNS interne, les services peuvent communiquer de manière fiable sans dépendre d’adresses IP fixes.
