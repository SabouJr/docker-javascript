# Node App with MongoDB in Docker Containers

## Dockerfile

---

```Docker
FROM node:12.18.1
```

> Prend l'image de node version 12.18.1 en tant que base

```Docker
WORKDIR /app
```

> On se place dans le répertoire /app

```Docker
COPY ["package.json", "package-lock.json*", "./"]
```

> On copie les fichiers "package.json", "package-lock.json", "./" dans le répertoire courant

```Docker
RUN npm install
```

> Installe les dépendances nécessaires pour l'application nodeJS

```Docker
COPY . .
```

> On copie tous les fichiers du répertoire courant de la machine sur le répertoire courant de l'image

```Docker
CMD ["npm", "start"]
```

> Lance le script de démarrage de l'application nodeJS

---

## Docker compose

### Service Node

---

```Docker
restart: always
```

> Relance le script de démarrage de nodeJS à chaque rechargement de page

```Docker
build .
```

> Lance le build du Dockerfile situé dans le répertoire courant

```Docker
ports:
    - 8443:3000
```

> Relie le port 8443 de la machine avec le port 3000 du container

```Docker
volumes:
    - ./:/code
```

> Créer un volume entre le répertoire courant de la machine et le répertoire /code du container

---

### Service mongo

---

```Docker
image: mongo
```

> Prend l'image mongo comme base du container

```Docker
ports:
    - 27017:27017
```

> Relie le port 27017 de la machine au port 27017 du container

```Docker
volumes:
    - mongodb:/data/db
```

> Créer un volume entre le répertoire mongodb de la machine et le répertoire /data/db du container
