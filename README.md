## Prérequis

Avant de démarrer le déploiement, assurez-vous que votre environnement dispose des outils suivants installés :

- **Docker**
- **Docker Compose**

## Structure du Projet

Les services suivants sont définis dans `docker-compose.yml` :

- **PostgreSQL** : Base de données
- **Backend** : API applicative
- **Frontend** : Interface utilisateur

## Arborescence du projet

```
<dossier>/
├── docker-compose.yml
├── .env
```

## Installation et Configuration

### 1. Clone du code 

```
unzip EU-BACKUP.zip
cd EU-BACKUP
```

### 2. Configurer les variables d'environnement

Créez un fichier `.env` à la racine du projet et renseignez-y les variables nécessaires. Assurez-vous que ce fichier contient les informations suivantes :

```
# Exemple de contenu
PORT=8080
API_KEY="default_api_key"
API_KEY_NAME="X-API-Key"
SWAGGER_USERNAME="admin"
SWAGGER_PASSWORD="admin"
SECRET_KEY="@(;}R;VXD4^CuSDzKOe+rJ(Ru;sPeWG+N^u~7aKdGOe{NFq')6"
ALGORITHM="HS256"
ACCESS_TOKEN_EXPIRE_MINUTES=60
REFRESH_TOKEN_EXPIRE_DAYS=7
DATABASE_URL=postgresql+asyncpg://postgres:postgres@postgres:5432/EU_backup
DB_HOST=postgres
DB_USER=postgres
DB_PASSWORD=postgres
```

### 3. Vérifier les permissions d'accès aux ports sériels

Si vous utilisez les périphériques `/dev/ttyUSB*`, assurez-vous que votre utilisateur a les droits nécessaires :

```
sudo usermod -a -G dialout $(whoami)
```

Redémarrez votre session pour appliquer les modifications.

## Lancer les services

### 1. Démarrer les conteneurs

Exécutez la commande suivante :

```
docker-compose up -d
```

Cette commande va :

- Démarrer PostgreSQL
- Démarrer le backend et le connecter à la base de données
- Démarrer le frontend et le connecter au backend

### 2. Vérifier l'état des conteneurs

```
docker ps
```

Si un conteneur rencontre une erreur, consultez ses logs avec :

```
docker logs <container_name>
```

## Accès aux Services

- **Base de données PostgreSQL** : `localhost:5432`
- **Backend** : `http://localhost:8000`
- **Frontend** : `http://localhost`

## Arrêt et Nettoyag

- Arrêter les services :
    
    ```
    docker-compose down
    ```
    
- Supprimer les volumes (attention, ceci supprimera toutes les données de PostgreSQL) :
    
    ```
    docker-compose down -v
    ```
    

## Debugging

- Pour voir les logs de tous les services :
    
    ```
    docker-compose logs -f
    ```
    
- Pour redémarrer un service :
    
    ```
    docker-compose restart <service_name>
    ```
    

---