origin ## **Mémo Linux-docker**
Formattage : .md

---
## <Ins>**Linux**</Ins>
| Syntax | Description |
| ------ | ----------- |
| ssh utilisateur@xxx.xx.xx.xx  | se connecter à un serveur avec SSH |
| passwd			| changement du password |
| xxxx.xxxx$(date +%Y%m%d) 	| rajoute la date aaaammdd dans le nom du fichier |
| ls 				| afficher les fichers d’un dossier |
| ls -la			| afficher les fichers d’un dossier verticalement |
| cd xxxx			| changer de dossier |
| cd ~ ou  cd			| Revenir à la racine de l'utilisateur.|
| TAB				| Complète le chemin par le début saisi|
| pwd 				| affiche le chemin courant |
| mkdir				| créer un dossier |
| rm 				| supprimer un fichier |
| rm -r				| supprimer un dossier |
| mv				| deplace un fichier |
| echo "texte"			| affiche un texte |
| touch 			| créer un fichier |
| echo "lulu" >> toto.txt 	| Crée un fichier .txtnavec le texte lulu |
| cp 				| copier |
| mv fichier repertoire		| déplacer |
| mv fichier fichier2		| renome le fichier en fichier2|
| cat	xx.yy 			| affiche le contenu du fichier xx.yy|
| cat *.* > toto.txt 		| met le contenu de tous les fichiers dans le fichier toto.txt |	
| find . -name '*hp.*' -print 	| rechercher tous les fichiers dont le nom contient hp dans le répertoire courant et sous-dossier|
| sed -n 3p *.* 		| affiche la 3ème ligne du contenu de tous les fichiers |
| sed -i 's/REGEX_RECHERCHE/REMPLACEMENT/g' [Fichier] | pour rechercher et remplacer un contenu dans un fichier |
| grep -rni 'dossier' -e 'expression' | liste les fichiers qui contiennent l'expression |
| clear				| Efface la console|
| Ports réservés 		| 20-21:FTP 22:SSH/SCP 53:DNS 80:HTTP 443:HTTPS 3306:mysql |
| sudo ufw status verbose 	| Affiche l'état actuel des règles du firewall|
| sudo ufw enable ou disable 	| active ou desactive le firewall |
| sudo ufw allow 53 		| ouvre le port 53 |
| sudo l 			| Autoriser le trafic entrant suivant les règles par défaut |
| env				| liste les variables d'environnement|
| netstat -an 			| liste les applications installées|
| utiliser apt dans la console, apt-get dans un script |
| apt update			| Mets à jour la liste des paquets|
| apt list --installed        	| Liste des paquets installés |
| apt upgrade 			| Mets à jour les paquets|
| apt install xxxx		| install le paquet xxxxxx|
| apt autoremove xxxx --purge 	| Désisntall le paquet (logiciel) xxxx ainsi que ses dépendances et ces fichiers de configuration|
| ps -u				| Affiche les processus de l'utilisateur, -ef pour tous les processus|
| lsof -i tcp:22		| Affiche les processus qui utilisent le port 22|
| pstree -p			| Affiche l'intégralité des processus avec une représentation graphique|
| tail -f /var/log/syslog     	| Affichage dynamique du fichier log du systeme|
| apt install
| exit				| quit la console|
| apt install figlet		| figlet affiche un texte en tres gros caractères --> sympa ! |


---
## <Ins>**Docker**</Ins>
| Syntax | Description |
| ------ | ----------- |

** Preparation installation Docker **
| for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done | désinstaller tous les packages docker en conflit |
| sudo apt update	| Mettre à jour les packages existant |
| sudo apt install apt-transport-https ca-certificates curl software-properties-common | installe quelques packages prérequis qui permettent aptd'utiliser des packages via HTTPS |
| curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg | Ajoute ensuite la clé GPG du référentiel Docker officiel à votre système |
| echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null | Ajoute le dépôt Docker aux sources APT |
| sudo apt update	|

** Installation Docker **
| sudo apt install docker-ce 		| Installe Docker |
| sudo systemctl status docker		| Verifie que le Docker fonctionne;  q pour quiter|
| sudo usermod -aG docker username	| Ajoute username au docker groupe; evite de taper sudo a chaque fois |
| groups				| Liste les utilisateurs du groupe Docker |

** Création Conteneur à partir d'une image **
| docker run hello-world		| Télécharge l'image hello-world; permet de vérifier que le processus fonctionne bien |
| docker run toto lulu			| Télécharge l'image lulu et crée un container associé toto |
| docker run -d toto lulu		| Télécharge l'image lulu et crée un container associé toto en arrière plan |

** Gestion des images **
| docker images 			| Affiche la liste des images téléchargées |
| docker rmi toto			| Supprime l'image toto |

** Arrêt conteneur **
| docker stop toto			| Arrête le conteneur toto en-cours d'exécution |
| docker start toto			| Démarre le conteneur toto arrêté |

** Suppression **
| docker container prune		| Supprime tous les conteneurs arrêtés |
| docker rm -f toto			| Supprime le conteneur toto en-cours d'exécution |

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

** Docker File pour serveur apache avec page index personnalisée. index.html dans le même dossier que Dockerfile **
| FROM httpd:2.4							|
| LABEL maintener = "Stephane"						|
| RUN apt update && apt upgrade						|
| COPY index.html /usr/local/apache2/htdocs/				|

** Docker file de l'exercice quarkus-api **
| FROM alpine
| LABEL maintainer="Stephane"
| RUN apk update
| RUN apk upgrade
| RUN apk add maven
| RUN apk add openjdk11
| RUN mkdir /realworld-api-quarkus_3
| COPY /realworld-api-quarkus/*.* /realworld-api-quarkus_3
| WORKDIR /realworld-api-quarkus_3
| RUN mvn install
| RUN mvn package
| WORKDIR /target/quarkus-app
| CMD ["java","-jar","/target/....]




















