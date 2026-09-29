TP 4 : Gestion de l'Héritage avec JPA et Hibernate

Ce projet a été réalisé pour étudier et comparer les trois stratégies de mapping d'héritage proposées par JPA et Hibernate, en s'appuyant sur une base de données H2 en mémoire.

Technologies utilisées

Java (version 8 ou supérieure)

Hibernate Core 5.6.5.Final

JPA 2.2 (javax.persistence-api)

Hibernate Validator 6.2.0.Final

H2 Database

SLF4J pour la gestion des logs

Maven pour la gestion des dépendances

Objectifs du TP

Mettre en place un projet Maven complet avec JPA, Hibernate et H2.

Implémenter et comparer les trois stratégies d'héritage : SINGLE_TABLE, JOINED et TABLE_PER_CLASS.

Tester les opérations d'insertion et observer les requêtes SQL générées pour chaque stratégie, notamment lors des requêtes polymorphiques.

Organisation du projet
Le code source est structuré dans les packages suivants :

com.example.model.singletable : contient la classe abstraite Vehicule ainsi que les sous-classes Voiture et Moto.

com.example.model.joined : contient la classe abstraite Employe ainsi que les sous-classes Developpeur et Manager.

com.example.model.tableperclass : contient la classe abstraite Produit ainsi que les sous-classes Livre et Electronique.

com.example.App : classe principale qui initialise l'EntityManagerFactory et exécute les tests pour chaque hiérarchie.
Le fichier de configuration JPA (persistence.xml) est situé dans src/main/resources/META-INF/.

Synthèse des stratégies implémentées

Stratégie SINGLE_TABLE (Exemple des Véhicules) :
Toute la hiérarchie est enregistrée dans une seule et unique table nommée vehicules. Une colonne de discrimination (type_vehicule) permet à Hibernate de savoir quel objet instancier.

Avantage : Très rapide en lecture car aucune jointure SQL n'est requise.

Inconvénient : Les colonnes propres aux sous-classes doivent accepter les valeurs nulles (nullable).

Stratégie JOINED (Exemple des Employés) :
Une table principale (employes) contient les champs communs, et des tables séparées (developpeurs, managers) stockent les champs spécifiques. La liaison s'effectue via la clé primaire partagée.

Avantage : Modèle relationnel parfaitement normalisé, sans colonnes superflues à NULL.

Inconvénient : Les requêtes nécessitent des jointures SQL (JOIN), ce qui impacte les performances quand les données augmentent.

Stratégie TABLE_PER_CLASS (Exemple des Produits) :
Chaque classe concrète possède sa propre table (livres, electroniques) contenant l'intégralité de ses champs, y compris ceux hérités.

Avantage : Tables totalement indépendantes les unes des autres.

Inconvénient : Les requêtes polymorphiques sur la classe mère sont lourdes car elles obligent la base à exécuter des clauses UNION.





https://github.com/user-attachments/assets/55bc0aca-ecb9-45f2-b42a-ab9524d67553



