origin ## **Mémo Linux-docker**
Formattage : .md

---
### <Ins>**Linux**</Ins>
| Syntax | Description                                                                                     |
|----|-------------------------------------------------------------------------------------------------|
| ssh utilisateur@xxx.xx.xx.xx | se connecter à un serveur avec SSH                                                              |
| passwd | changement du password                                                                          |
| xxxx.xxxx$(date +%Y%m%d) | rajoute la date aaaammdd dans le nom du fichier                                                 |
| ls | afficher les fichers d’un dossier                                                               |
| ls -la | afficher les fichers d’un dossier verticalement                                                 |
| cd xxxx | changer de dossier                                                                              |
| cd ~ ou  cd			 | Revenir à la racine de l'utilisateur.                                                           |
| TAB				 | Complète le chemin par le début saisi                                                           |
| pwd 				 | affiche le chemin courant                                                                       |
| mkdir				 | créer un dossier                                                                                |
| rm 				 | supprimer un fichier                                                                            |
| rm -r				 | supprimer un dossier                                                                            |
| mv				 | deplace un fichier                                                                              |
| echo "texte"			 | affiche un texte                                                                                |
| touch 			 | créer un fichier                                                                                |
| echo "lulu" >> toto.txt 	 | Crée un fichier .txtnavec le texte lulu                                                         |
| cp 				 | copier                                                                                          |
| mv fichier repertoire		 | déplacer                                                                                        |
| mv fichier fichier2		 | renome le fichier en fichier2                                                                   |
| cat	xx.yy 			 | affiche le contenu du fichier xx.yy                                                             |
| cat *.* > toto.txt 		 | met le contenu de tous les fichiers dans le fichier toto.txt                                    |	
| find . -name '*hp.*' -print 	 | rechercher tous les fichiers dont le nom contient hp dans le répertoire courant et sous-dossier |
| sed -n 3p *.* 		 | affiche la 3ème ligne du contenu de tous les fichiers                                           |
| sed -i 's/REGEX_RECHERCHE/REMPLACEMENT/g' [Fichier] | pour rechercher et remplacer un contenu dans un fichier                                         |
| grep -rni 'dossier' -e 'expression' | liste les fichiers qui contiennent l'expression                                                 |
| clear				 | Efface la console                                                                               |
| Ports réservés 		 | 20-21:FTP 22:SSH/SCP 53:DNS 80:HTTP 443:HTTPS 3306:mysql                                        |
| sudo ufw status verbose 	 | Affiche l'état actuel des règles du firewall                                                    |
| sudo ufw enable ou disable 	 | active ou desactive le firewall                                                                 |
| sudo ufw allow 53 		 | ouvre le port 53                                                                                |
| sudo l 			 | Autoriser le trafic entrant suivant les règles par défaut                                       |
| env				 | liste les variables d'environnement                                                             |
| netstat -an 			 | liste les applications installées                                                               |
| utiliser apt dans la console, apt-get dans un script |
| apt update			 | Mets à jour la liste des paquets                                                                |
| apt list --installed        	 | Liste des paquets installés                                                                     |
| apt upgrade 			 | Mets à jour les paquets                                                                         |
| apt install xxxx		 | install le paquet xxxxxx                                                                        |
| apt autoremove xxxx --purge 	 | Désisntall le paquet (logiciel) xxxx ainsi que ses dépendances et ces fichiers de configuration |
| ps -u				 | Affiche les processus de l'utilisateur, -ef pour tous les processus                             |
| lsof -i tcp:22		 | Affiche les processus qui utilisent le port 22                                                  |
| pstree -p			 | Affiche l'intégralité des processus avec une représentation graphique                           |
| tail -f /var/log/syslog     	 | Affichage dynamique du fichier log du systeme                                                   |
| exit				 | quit la console                                                                                 |
| apt install figlet		 | figlet affiche un texte en tres gros caractères --> sympa !                                     |


---
### <Ins>**Preparation installation Docker**</Ins>
| Syntax                                                                                                          | Description                                      |
|-----------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done | désinstaller tous les packages docker en conflit |
| sudo apt update	                                                                                                | Mettre à jour les packages existant              |


### <Ins>**Installation Docker**</Ins>
| Syntax                                                                                                                                                                     | Description                                                                                                   |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| La Syntax correspond à Ubuntu                                                                                                                                              | Le mieux est d'aller sur le site docker pour prendre la commande qui correspond en fonction de son OS / linux |
| sudo apt install apt-transport-https ca-certificates curl software-properties-common                                                                                       | installe quelques packages prérequis qui permettent aptd'utiliser des packages via HTTPS                      |
| curl -fsSL https://download.docker.com/linux/ubuntu/gpg                                                                                                                    | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg                                          | Ajoute ensuite la clé GPG du référentiel Docker officiel à votre système |
| echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null                                                      | Ajoute le dépôt Docker aux sources APT |
| sudo apt update	                                                                                                                                                           |
| sudo apt install docker-ce 		                                                                                                                                              | Installe Docker                                                                                               |
| sudo systemctl status docker		                                                                                                                                             | Verifie que le Docker fonctionne;  q pour quiter                                                              |
| sudo usermod -aG docker username	                                                                                                                                          | Ajoute username au docker groupe; evite de taper sudo a chaque fois                                           |
| groups				                                                                                                                                                                 | Liste les utilisateurs du groupe Docker                                                                       |

### <Ins>Création Conteneur à partir d'une image </Ins>
| Syntax                   | Description                                                                         |
|--------------------------|-------------------------------------------------------------------------------------|
| docker run hello-world   | Télécharge l'image hello-world; permet de vérifier que le processus fonctionne bien |
| docker run toto lulu     | Télécharge l'image lulu et crée un container associé toto                           |
| docker run -d toto lulu  | Télécharge l'image lulu et crée un container associé toto en arrière plan           |


### <Ins>Gestion des images</Ins>
| Syntax           | Description                              |
|------------------|------------------------------------------|
| docker images    | Affiche la liste des images téléchargées |
| docker rmi toto  | Supprime l'image toto                    |

### <Ins>Arrêt conteneur</Ins>
| Syntax             | Description                                   |
|--------------------|-----------------------------------------------|
| docker stop toto   | Arrête le conteneur toto en-cours d'exécution |
| docker start toto  | Démarre le conteneur toto arrêté              |


### <Ins>Suppression</Ins>
| Syntax                 | Description                                     |
|------------------------|-------------------------------------------------|
| docker container prune | Supprime tous les conteneurs arrêtés            |
| docker rm -f toto      | Supprime le conteneur toto en-cours d'exécution |

** Affichage **
| docker ps				| Affiche les conteneurs en-cours d'exécution |
| docker ps -a				| Affiche tous les conteneurs |

** Commande dans le conteneur **
| docker exec -it toto bash		| Démarre une session bash du container toto en-cours d'exécution |

** Renommage **
| docker rename toto lulu		| renomme le conteneur toto en lulu |

** Serveur Apache **
| docker run -dit --name toto -p 8080:80 -v /home/user/website/:/usr/local/apache2/htdocs/ httpd:2.4 |
|	lance un container à partir de l'image Apache (httpd:2.4) |
|	redirige le port 80 vers le port 8080 |
|	transfert le dossier /home/user/website/ vers le dossier /usr/local/apache2/htdocs/ du conteneur |

** Construire une image à partir d'un Dockerfile **
| docker build -t nomImage .	

** Créé et lance un container à partir de l'image **			
| docker run -dit -p 9091:8080 nomImage			| redirige port 8080 sur 9091 |

** Docker File pour docker qui affiche un texte **
| Créer un dossier avec le fichier Dockerfile 				|
| FROM alpine								|
| LABEL maintainer="Stephane"						|
| CMD ["echo", "Conversation depuis l’intérieur de la baleine"]		|

# Docker File pour serveur apache avec page index personnalisée. index.html dans le même dossier que Dockerfile **
| FROM httpd:2.4							|
| LABEL maintener = "Stephane"						|
| RUN apt update && apt upgrade						|
| COPY index.html /usr/local/apache2/htdocs/				|

** Docker Compose **
| apt install docker-compose                        | installe docker-compose  |
| docker-compose up                                 | monte docker-compose, lance le fichier docker-compose.yml |
| docker compose down                               | arrête proprement tous les containers montés avec up |
voir docker-compose.yml fait en formation sept 2023

** Reverse proxy NGINX **
nécessite :
- un pavé dans le docker-compose.yml pour créer un container qui va contenir les autres container
- un fichier nginx.conf (voir plus bas)

** Docker file de l'exercice quarkus-api **
# A partir de l'image alpine  
FROM alpine  
LABEL maintainer="Stephane"
# Maj systeme. Dans alpine apt est remplacé par apk
RUN apk update
RUN apk upgrade
# Ajoute Maven, necessaire pour apirealworld sous quarkus
RUN apk add maven
# Ajoute console bash
RUN apk add bash
# apirealworld a besoin de openjdk11
RUN apk add openjdk11
# creation dossier dans container
# RUN mkdir /realworld-api-quarkus_1
# copie du projet realworld dans le container
COPY realworld-api-quarkus/ /realworld-api-quarkus_1/
# On se place dans le dossier créé
WORKDIR /realworld-api-quarkus_1
# install et compile le projet apirealworld
# RUN mvn install
# RUN mvn package
RUN cd /realworld-api-quarkus_1 && chmod u+x ./mvnw && ./mvnw package
# On se place dans le dossier ou se situe le .jar du projet apirealworld
WORKDIR /realworld-api-quarkus_1/target/quarkus-app

ENV POSTGRES_USERNAME=postgres
ENV POSTGRES_PASSWORD=123456
ENV POSTGRES_HOST=localhost
ENV POSTGRES_DB=postgres
ENV POSTGRES_PORT=5432

# Lance le .jar
CMD ["java","-jar","quarkus-run.jar"]


** Docker-compose.yml de l'exercice realworld **
version: '3'
services:

# Container DB Postgres
  realworld-postgres:
    image: "postgres:15.4-alpine"
    container_name: realworld-postgres
# Sauvegarde ce chemin du container dans l'environnement (persistence)
#    volumes:
#      - realworld-data:/var/lib/postgresql/data
    ports:
      - 5432:5432
# Valeurs par defaut qui seront redéfinis par l'image realworld-api
    environment:
      POSTGRES_DB: "postgres"
      POSTGRES_USER: "postgres"
      POSTGRES_PASSWORD: "123456"
      #POSTGRES_HOST: "localhost"
      #POSTGRES_PORT: 5432
      #POSTGRES_HOST_AUTH_METHOD: "trust"

# Container API
  realworld-api:
    image: "api"
    container_name: realworld-api
    environment:
      POSTGRES_HOST: "realworld-postgres"
    ports:
      - 8080:8080
    links:
      - realworld-postgres


# Container front
  realworld-front:
    image: "ember"
    container_name: realworld-front
    ports:
      - 4200:4200
    environment:
      HOSTNAME: "localhost"

# ReverseProxy : voir nginx.conf
  nginx:
    image: "nginx:latest"
    ports: 
      - 80:80
    depends_on: 
      - realworld-api
      - realworld-front
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
            
#volumes:
#  realworld-data:

** nginx.conf de realworld **
worker_processes 1;

events {
    worker_connections 1024;
}

http {
    server {
        listen 80;
        server_name your-domain.com;  

        location / {
            proxy_pass http://realworld-front:4200;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }

        location /api {
            proxy_pass http://realworld-api/8080;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
















