# Utiliser l'image de base officielle de Drupal
FROM drupal:latest

# Mettre à jour les dépôts, installer Git, puis nettoyer les fichiers inutiles
RUN apt-get update && \
    apt-get install -y git && \
    rm -rf /var/lib/apt/lists/*

# Changer de répertoire pour /var/www/html/themes
WORKDIR /var/www/html/themes

# Cloner le thème Bootstrap à la branche 5.0.x
RUN git clone --branch 5.0.x --single-branch --depth 1 https://git.drupalcode.org/project/bootstrap.git && \
    chown -R www-data:www-data bootstrap

# Revenir au répertoire principal de Drupal
WORKDIR /var/www/html

# Définir les volumes nécessaires pour Drupal
VOLUME ["/var/www/html/sites", "/var/www/html/files"]

# Exposer le port 8080 pour Drupal
EXPOSE 8080

