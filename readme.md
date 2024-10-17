# Projet Docker TP - Étapes Complètes

Ce projet Docker couvre la mise en place d'une infrastructure complète comprenant NGINX, PHP-FPM et MySQL pour héberger un site WordPress. Chaque étape montre comment configurer et lancer les conteneurs à l'aide de Docker ou Docker Compose.

## Pré-requis

- Docker et Docker Compose installés sur votre machine.
- Connexion internet pour télécharger les images nécessaires et WordPress.
- Créer un Réseau Docker Personnalisé

## Structure du Projet

docker-tp2/
├── etape1/
│   ├── http/
│   │   ├── Dockerfile        # Fichier Docker pour configurer NGINX
│   │   └── default.conf      # Configuration de NGINX
│   ├── script/
│   │   └── Dockerfile        # Fichier Docker pour configurer PHP-FPM
├── etape2/
│   ├── http/
│   │   ├── Dockerfile        # Fichier Docker pour configurer NGINX
│   │   └── default.conf      # Configuration de NGINX
│   ├── script/
│   │   └── Dockerfile        # Fichier Docker pour configurer PHP-FPM
│   ├── data/
│   │   ├── Dockerfile        # Fichier Docker pour configurer MySQL
│   │   └── init.sql          # Script SQL d'initialisation de la base de données
│   ├── app/
│   │   └── test_bdd.php      # Fichier PHP pour tester la connexion à MySQL
├── etape3/
│   ├── http/
│   │   ├── Dockerfile        # Fichier Docker pour configurer NGINX pour WordPress
│   │   └── default.conf      # Configuration de NGINX pour WordPress
│   ├── script/
│   │   └── Dockerfile        # Fichier Docker pour configurer PHP-FPM
│   ├── data/
│   │   ├── Dockerfile        # Fichier Docker pour configurer MySQL
│   │   └── init.sql          # Script SQL d'initialisation de la base de données
│   ├── app/
│   │   └── wordpress/        # Dossier contenant tous les fichiers WordPress
└── etape4/
│   ├── http/
│   │   ├── Dockerfile        # Fichier Docker pour configurer NGINX
│   │   └── default.conf      # Configuration de NGINX
│   ├── script/
│   │   └── Dockerfile        # Fichier Docker pour configurer PHP-FPM
│   ├── data/
│   │   ├── Dockerfile        # Fichier Docker pour configurer MySQL
│   │   └── init.sql          # Script SQL d'initialisation de la base de données
│   ├── app/
│   │   └── wordpress/        # Dossier contenant tous les fichiers WordPress
│   ├── docker-compose.yml    # Fichier Docker Compose pour orchestrer tous les services
│
└──  README.md      # Instructions du projet



## Étape 1 : Mise en Place de NGINX et PHP-FPM

### Commandes à Exécuter :

1. **Configurer et Construire les Conteneurs :**
   ```bash
    docker build -t my-php ./etape1/script
    docker run --name script --network my-network -v $(pwd)/etape1/app:/app -d my-php
    docker build -t my-nginx ./etape1/http
    docker run --name http --network my-network -p 8080:8080 -v $(pwd)/etape1/app:/app -d my-nginx

    Accéder à la Page dAccueil : Visitez http://localhost:8080

## Étape 2 : Ajout de MySQL et Connexion avec PHP

### Commandes à Exécuter :

1. **Configurer et Construire les Conteneurs :**
   ```bash
    ddocker build -t my-mysql ./etape2/data
    docker run --name data --network my-network -p 3306:3306 -d my-mysql

    docker build -t my-php ./etape2/script
    docker run --name script --network my-network -v $(pwd)/etape2/app:/app -d my-php

    docker build -t my-nginx ./etape2/http
    docker run --name http --network my-network -p 8080:8080 -v $(pwd)/etape2/app:/app -d my-nginx

    Accéder à la Page de Test : Visitez http://localhost:8080/test_bdd.php

## Étape 3 : Mise en Place de WordPress

### Commandes à Exécuter :

1. **Configurer et Construire les Conteneurs :**
   ```bash
    curl -o wordpress.tar.gz https://wordpress.org/latest.tar.gz
    dans létape 3 mkdir -p /app/wordpress
    tar -xzvf wordpress.tar.gz -C /app/wordpress --strip-components=1

    docker build -t my-mysql ./etape3/data
    docker run --name data --network my-network -p 3306:3306 -d my-mysql

    docker build -t my-php ./etape3/script
    docker run --name script --network my-network -v $(pwd)/etape3/app/wordpress:/app -d my-php

    docker build -t my-nginx ./etape3/http
    docker run --name http --network my-network -p 8080:8080 -v $(pwd)/etape3/app/wordpress:/app -d my-nginx

    Accéder à lInterface de WordPress : Visitez http://localhost:8080

## Étape 4 : Utilisation de Docker Compose pour Lancer Tous les Services

### Commandes à Exécuter :

1. **Construire et Lancer Tous les Services avec Docker Compose : :**
   ```bash
    curl -o wordpress.tar.gz https://wordpress.org/latest.tar.gz
    dans létape 3 mkdir -p /app/wordpress
    tar -xzvf wordpress.tar.gz -C /app/wordpress --strip-components=1
    (si jamais vous n avez plus le dossier wordpress precedent)

    Dans l etape 4 => docker-compose up --build -d ou docker compose up --build -d
    Dans l etape 4 => docker-compose down

    Accéder à l Interface de WordPress : Visitez http://localhost:8080