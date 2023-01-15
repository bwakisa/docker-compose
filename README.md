
## Run API service

- Up api service with docker-compose

```
    docker-compose up -d nginx_bwakisa

```
- Acceder au shell bash du conteneur de l'application

```
    docker-compose exec php_bwakisa /bin/bash

```

- Une fois acceder au shell, cloner le projet git

```
    git clone https://github.com/bwakisa/bwakisa.git .

```


- Une fois le projet cloné, quitter le shell du container api

```

    exit

```

- Donnez à tous le monde le droit de lire et ecrire sur le dossier `app_bwakisa`

```

    sudo chmod 777 -R ./app_bwakisa

```


- créer .env le fichier `./app_bwakisa/.env` puis inserer le contenu 

```
    Modifier le fichier d'environement

```
- Acceder au shell bash du conteneur de l'application

```
    docker-compose exec php_bwakisa /bin/bash

```

- Télécharger les dependances php du projet

```
    composer install

```


- Télécharger les dependances js du projet pour la documentation de l'application

```
    yarn install

```

- compiller les js du projet pour la documentation de l'application

```
    npm run build

```

- Créer la base des données

```
    php bin/console doctrine:database:create

```

- Créer les shema de la base des données

```

    php bin/console doctrine:schema:create    

```


- Remplir la base des données de fausse données

```

    php bin/console doctrine:fixtures:load   

```
- Tester l'api sur le navigateur

```
    http://localhost:8080

```

- Quitter le shell du container php

```

    exit

```
# docker-compose-bwakisa
