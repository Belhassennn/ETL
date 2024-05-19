# ETL
Ce projet implique le traitement d'un jeu de données de parties d'échecs de Lichess.org, la division de ces données en deux parties, l'importation d'une partie dans une base de données MySQL, puis la combinaison des deux parties pour une analyse ultérieure. Voici un guide détaillé et structuré du workflow complet, basé sur les étapes mentionnées :

##1. Compréhension du Projet
Objectif :

Utiliser les enregistrements de parties d'échecs de Lichess.org pour l'analyse.
Traiter les données, y compris la concaténation de différentes parties du jeu de données.
S'assurer que les données sont divisées, traitées et stockées correctement.
##2. Compréhension des Données
Aperçu du Jeu de Données :

Nombre de lignes : 20058
Nombre de colonnes : 16
Colonnes comprenant des identifiants, des détails de la partie, les classements des joueurs et des informations sur les ouvertures.
Détails des Colonnes :

Id : Identifiant de la partie
Rated : Si la partie est classée ou non
Created_at : Heure de début
Last_move_at : Heure de fin
Turns : Nombre de coups
Victory_status : Statut de la partie
Winner : Gagnant (noir ou blanc)
Increment_code : Mode d'incrément de temps
White_id : Identifiant du joueur blanc
White_rating : Classement du joueur blanc
Black_id : Identifiant du joueur noir
Black_rating : Classement du joueur noir
Moves : Tous les coups en notation standard des échecs
Opening_eco : Code standardisé pour les ouvertures
Opening_name : Nom de l'ouverture
Opening_ply : Nombre de coups dans la phase d'ouverture
#3. Préparation des Données
Division du Jeu de Données :

Diviser le jeu de données en deux parties :
Première partie : 19058 lignes enregistrées dans un fichier CSV.
Deuxième partie : 1000 lignes déplacées dans un nouveau fichier CSV pour importation dans MySQL.
Étapes :

Utilisation d'un éditeur de texte :

Ouvrez le fichier CSV original.
Déplacez les 1000 dernières lignes vers un nouveau fichier CSV (second_part.csv).
Enregistrez les 19058 premières lignes dans un autre fichier CSV (first_part.csv).
Lecture du CSV dans KNIME :

Utilisez le nœud CSV Reader pour lire first_part.csv.
Configuration du CSV Reader :

Emplacement du fichier : Chemin vers first_part.csv.
Supporter les lignes courtes : Coché.
En-tête de colonne : Coché.
En-tête de ligne : Décoché.
Configuration de MySQL :
Ajoutez le nœud MySQL Connector dans KNIME.
Configurez-le avec les informations nécessaires (nom d'utilisateur, mot de passe, nom d'hôte, nom de la base de données).
Configuration du MySQL Connector :

Configurez les détails de connexion pour votre base de données MySQL.
Nœud DB Writer :
Utilisez le nœud DB Writer pour écrire les données de second_part.csv dans la base de données MySQL.
##4. Modélisation
Extraction de Données de Différentes Sources :

Fichier CSV :
Ajoutez un autre nœud CSV Reader.
Configurez-le pour lire le fichier first_part.csv.
Configuration du CSV Reader :

Emplacement du fichier : Chemin vers first_part.csv.
Supporter les lignes courtes : Coché.
En-tête de colonne : Coché.
En-tête de ligne : Décoché.
DB Reader :
Ajoutez le nœud DB Reader dans KNIME.
Configurez-le pour lire les données de la table MySQL où second_part.csv a été importé.
Concaténation :

Utilisez le nœud Concatenate pour combiner les sorties des nœuds CSV Reader et DB Reader.
##5. Évaluation
Validation :

Assurez-vous que le nombre de lignes dans le jeu de données concaténé est égal au nombre de lignes dans le jeu de données original (20058 lignes).
##6. Déploiement
Excel Writer :

Ajoutez un nœud Excel Writer dans KNIME.
Configurez-le avec l'emplacement de sortie et les colonnes souhaitées pour le jeu de données final.
Configuration de l'Excel Writer :

Emplacement du fichier de sortie : Spécifiez où le fichier Excel final doit être enregistré.
Colonnes à inclure : Sélectionnez les colonnes nécessaires.
DB Writer :

Ajoutez un nœud DB Writer dans KNIME.
Configurez-le pour écrire le jeu de données concaténé dans la base de données MySQL.
Configuration du DB Writer :

Schéma et table de sortie : Spécifiez le schéma et le nom de la table dans la base de données MySQL.
Colonnes à inclure : Sélectionnez les colonnes nécessaires.
##orkflow Final
###Workflow KNIME :

Commencez avec le nœud CSV Reader pour first_part.csv.
Utilisez les nœuds MySQL Connector et DB Writer pour importer second_part.csv dans MySQL.
Extrayez les données des deux sources en utilisant les nœuds CSV Reader et DB Reader.
Concaténez les deux jeux de données avec le nœud Concatenate.
Déployez le jeu de données final en utilisant les nœuds Excel Writer et DB Writer.
Ce guide structuré garantit un traitement efficace et une intégration des données, les rendant prêtes pour une analyse et un rapport ultérieurs.








