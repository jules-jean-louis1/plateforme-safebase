<div align="center">
  <svg
    width="100"
    height="90"
    viewBox="0 0 40 36"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <g clip-path="url(#clip0_104_2)">
      <rect width="40" height="36" fill="none" />
      <path
        d="M0.096614 35.9905V27.0455H19.5688H20.031L18.9045 26.5083C18.9045 26.5083 6.84699 21.0481 0.820792 18.3639C0.2079 18.0902 -0.0146648 17.7748 0.000743114 17.0851C0.0486788 14.6591 0.0349829 12.2331 0.000743114 9.80715C0.000743114 9.24397 0.135992 8.94072 0.67698 8.69813C6.9634 5.89091 13.2361 3.0525 19.5191 0.234893C19.8275 0.0924184 20.1612 0.0146144 20.5001 0.00616124C26.8344 -0.00770154 39.5032 0.00616124 39.5032 0.00616124H39.9106V8.97711H20.5155H20.0995L21.0051 9.44498C21.0051 9.44498 33.1363 14.9277 39.2155 17.6396C39.801 17.9013 40.0099 18.2028 39.9996 18.8526C39.9586 21.3358 39.9688 23.8207 39.9996 26.3039C39.9996 26.8098 39.8473 27.0784 39.3919 27.2829C33.0575 30.1225 26.7232 32.9684 20.3888 35.8207C20.1285 35.9334 19.8485 35.9923 19.5653 35.9939C13.2036 36.002 6.84184 36.002 0.480098 35.9939L0.096614 35.9905ZM20.055 17.9082V26.9623L29.9674 22.4829C28.418 21.7898 27.0895 21.1989 25.7696 20.5907C23.8573 19.7104 21.9501 18.8162 20.0413 17.9273V8.97711L10.0193 13.4946C12.4863 14.6037 14.7375 15.626 17.0008 16.6276C18.0091 17.0764 19.0381 17.4802 20.055 17.9082Z"
        fill="#B19DF7"
      />
    </g>
    <defs>
      <clipPath id="clip0_104_2">
        <rect width="40" height="36" fill="none" />
      </clipPath>
    </defs>
  </svg>
  <h1 style="font-size: 3em; margin-bottom: 0;">SafeBase</h1>
</div>

## 📋 Description du projet

SafeBase est un projet réalisé en Go, conçu pour permettre la gestion des backups et restaurations de bases de données PostgreSQL et MySQL. Le projet fournit une API REST qui permet aux utilisateurs de sauvegarder (dump) et restaurer des bases de données, soit à partir d'un conteneur Docker contenant la base de données, soit en téléchargeant directement les fichiers de backup depuis le frontend.

### 🌟 Fonctionnalités clés

- **🔒 Sauvegarde des bases de données** : Crée des dumps complets des bases de données.
- **🔄 Restauration des bases de données** : Permet la restauration à partir de fichiers de sauvegarde existants.
- **📊 Suivi des opérations** : Garde un historique des backups et des restaurations effectués, avec des statuts de réussite ou d'échec.
- **⏰ Gestion des jobs planifiés (cron jobs)** : Automatisation des backups à intervalles réguliers.
- **🖥️ Interface utilisateur** : Permet de télécharger et restaurer les backups directement via le frontend.

L'application s'appuie sur les outils `pg_dump` pour PostgreSQL et `mysqldump` pour MySQL afin d'assurer la sécurité et l'intégrité des sauvegardes.

## 🚀 Initialisation du projet

1. Copier le `.env.example` dans des `.env`, le dossier `docker/` et remplacer les valeurs par défaut par celles de votre environnement local.

   ```bash
   cp docker/.env.example docker/.env

2. Pour initialiser le projet, utilisez la commande suivante à la racine du projet pour créer tous les conteneurs nécessaires :

   ```bash
   ./docker/docker.sh up -d
   ```

3. Démarrer les conteneurs :

   ```bash
   ./docker/docker.sh start
   ```

4. Arrêter les conteneurs :

   ```bash
   ./docker/docker.sh stop
   ```

5. (Re)build un seul conteneur :

   ```bash
   ./docker/docker.sh up -d <container_name>
   ```

6. Rentrer dans le container :

   ```bash
   docker exec -it <container_name> /bin/sh
   ```

🌐 Le frontend est accessible à l'adresse suivante : `http://localhost:4200/`
🚀 L'API REST est accessible à `http://localhost:8080/`

## 🗄️ Connexion aux différentes bases de données

### DBeaver

#### SafeBase

- Host: `localhost`
- Port: `5434`
- Username: `postgres`
- Password: `password`
- Database: `safebase`

#### Postgres_DB

- Host: `localhost`
- Port: `5433`
- Username: `postgres`
- Password: `password`
- Database: `postgresdb` || `dev` || `prod`

#### MySQL_DB

- Host: `localhost`
- Port: `3307`
- Username: `root`
- Password: `password`
- Database: `online_library` || `dev_db` || `prod_db`

### Sur l'application

#### Postgres_DB

- Host: `postgres_db`
- Port: `5432`
- Username: `postgres`
- Password: `password`
- Database: `postgresdb` || `dev` || `prod`

#### MySQL_DB

- Host: `mysql_db`
- Port: `3306`
- Username: `root`
- Password: `password`
- Database: `online_library` || `dev_db` || `prod_db`

## 🛠️ API REST

L'API REST fournit les endpoints suivants :

- **GET /databases** : Récupère la liste des bases de données disponibles.

  ```bash
  curl -X GET http://localhost:8080/databases
  ```

- **POST /database** : Ajouter un base de donnée.

  ```bash
  curl -X POST http://localhost:8080/database
  ```

## Lint

Pour linter le code, `golangci-lint` est utilisé pour le backend en Go. Exécutez cette commande dans le conteneur Docker, assurez-vous d'être dans le dossier `/app`:

```bash
golangci-lint ./ ...
```

En front Prettier est utiliser pour le front-end, se rendre dans le dossier `/frontend`:

```bash
npm run -save-dev prettier
npm run format.
```

Pour vérifier le formatage sans modifier les fichiers, exécutez:

```bash
npm run format:check
```


## Déploiement

### Pousser les images Docker

Les images Docker pour le backend et le frontend sont poussées sur GitHub Container Registry lors de chaque push ou pull request sur la branche `dev`.

Modifiez  le fichier `.env` dans le dossier `docker/` pour passer la variable NODE_ENV à `production` pour le déploiement en production.

```bash
   ./docker/docker.sh up -d
```


## 📄 License

[MIT](https://choosealicense.com/licenses/mit/)

## 👥 Contributeurs

- [Jean-Louis Jules](https://github.com/jules-jean-louis1)
