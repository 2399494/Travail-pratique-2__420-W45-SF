# Utilisez l'image officielle PostgreSQL comme base
FROM postgres:latest

# Définissez les variables d'environnement pour la base de données
ENV POSTGRES_DB=drupal
ENV POSTGRES_USER=drupaluser
ENV POSTGRES_PASSWORD=drupalpassword

# Le volume pour stocker les données de la base PostgreSQL
VOLUME ["/var/lib/postgresql/data"]

