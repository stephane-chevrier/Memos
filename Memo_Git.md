mkdir del## **Mémo Git**
Formattage : .md

---
## <Ins>**Console Git Bash**</Ins>
| Syntax | Description |
| ------ | ----------- |
| ls 		| afficher les fichers d’un dossier |
| ls -la	| afficher les fichers d’un dossier verticalement |
| cd 		| changer de dossier |
| cd ~		| Revenir à la racine de l'utilisateur|
| TAB		| Complète le chemin par le début saisi|
| pwd 		| affiche le chemin courant |
| mkdir		| créer un dossier |
| rm 		| supprimer un fichier |
| rm -r		| supprimer un dossier |
| mv		| deplace un fichier |
| echo "texte"	| affiche un texte |
| touch 	| créer un fichier |
| echo "lulu" >> toto.txt 	| Crée un fichier .txtnavec le texte lulu |
| cp 		| copier |
| mv 		| déplacer |
| cat	xx.yy 	| affiche le contenu du fichier xx.yy|
| cat *.* > toto.txt | met le contenu de tous les fichiers dans le fichier toto.txt |	
| sed -n 3p *.* | affiche la 3ème ligne du contenu de tous les fichiers |
| sed -i 's/REGEX_RECHERCHE/REMPLACEMENT/g' [Fichier] | pour rechercher et remplacer un contenu dans un fichier |
| grep -rni 'dossier de recherche' -e 'expression à rechercher' | liste les fichiers qui contiennent l'expression |
| clear		| Efface la console|
| exit		| quit la console|


| Option 	| Description |
| ------ 	| ----------- |
|– help	| liste des options|


---
## <Ins>**Ressources**</Ins>
Git-it : Application qui permet d'apprendre à utiliser Git & GitHub
[petit guide](https://rogerdudler.github.io/git-guide/index.fr.html)
[jeu pour comprendre Git](https://ohmygit.org/)
[Git doc officielle](https://git-scm.com/)
[Git les commandes à connaitre absolument](https://www.hostinger.fr/tutoriels/commandes-git)

---
## <Ins>**Commandes Git**</Ins>
| Syntax 		| Description |
| ------ 		| ----------- |
| git config --global user.username <USerNamE>	| Ajoutez votre nom d'utilisateur GitHub à votre configuration Git |
| git config --global user.username		| Affiche le nom d'utilisateur |
| git config --global user.email "xxx@yyy"	| Ajoutez votre mail à votre configutation Git|
| git config color.ui true			| utiliser des couleurs dans la sortie de git|
| git init		| Activez Git pour un repertoire (dans ce cas le répertoire courant) |
| get init --bare	| Cette option permet de préciser que ce dossier ne contiendra pas de dossier de travail mais seulement l'historique de notre projet. Ces dossiers --bare peuvent être utilisés comme dépôt distant.|
| git status    	| Vérifiez l'état des modifications dans un dépôt |
| git log		| Afficher l'historique du projet |
| git diff 		| Afficher les modifications apportés aux fichiers |
| git add <FILENAME>	| Ajouter à l'index les modifications d'un fichier à soumettre. |
| git add .		| Pour ajouter toutes les modifications d'un seul coup. [A proscrire quand on travaille à plusieurs] |
| git commit -m "xxx"	| Pour soumettre les modifications que vous avez ajoutées avec un court message "xxx" |
| git remote add <alias> <chemin/url> | Ajoute un nouveau dépôt distant|
| git remote -v		| affiche toutes les listes de dépôts et leurs URL|
| git remote rm <alias> | supprime un depot distant|
| git clone /github...	| Pour créer une copie dans le repertoire courant de votre dépôt local; username@host:/chemin |
| git push		| Pour les envoyer à votre dépôt distant|
| git push <remote> <branche> |permet d'envoyer tous les commits d'une branche au dépôt distant.|
| git pull		| Récupère la version du dépo distant|
| git pull <remote> <branche>| récupère la branche du depot distant|
| git checkout <commit> | Pour voir le projet avant le précédent commit|
| git reset		| A voir, très nombreuses possibilités. ne jamais utiliser après avoir publié (push)|
| git branch -M main	| Pour/créer une branche, en l'occurence main|
| git remote add origin https://github.com/stephane-chevrier/memo-git.git|
| git rm 		| Supprime des fichiers de l'arborescence de travail et de l'index|


<Ins>**Pour ajouter un fichier au repository : add + commit**</Ins>
exemple : add a, commit --> demande de validation de a
exemple : add a, add b, commit, add c, commit --> demande de validation de a et b, demande de validation de c

## <Ins>**Comment créez un nouveau dépôt en ligne de commande**</Ins>
git init 	// dans le répertoire du projet
touch .gitignore // Créé le fichier .gitignore; Il a besoin d'un fichier .gitignore, même vide, pour fonctionner
echo ".idea" >> .gitignore // Retire le dossier .idea de la synchronisation
git add xx.yy	// mets à jour l'index avec le fichier xx.yy
git commit -m "first commit" // Créé une version avec un commentaire
git branch -M main  // créé la branche "Main"
Créer sous GitHub le repository toto.lulu
  // Créé le depot en git ligne sur github. origin=chemin d'origine
git remote add origin https://github.com/stephane-chevrier/toto.lulu
git push -u origin main  // pousse la branche main dans origin

## <Ins>**Comment créez un clone**</Ins>
Se place dans le répertoire où on veut mettre le clone
git clone https://github.com/stephane-chevrier/RepositorySouahité
cd NomProjet

## <Ins>**Mettre à jour le projet sur GitHub**</Ins>
faire ses modifications sur le clone
git add .	[A proscrire quand on travaille à plusieurs]
git commit -m "version modifiée"
git push
la version modifiée est déormais sur GitHub

## <Ins>**Mettre à jour le projet local avec la version GitHub**</Ins>
git pull

## <Ins>**Définir des fichiers à ignorer lors de la synchronisation**</Ins>
Créer un fichier texte .gitignore
Mettre dans chaque ligne le nom du fichier ignoré
par exemple *.txt ignorera touts les fichiers .txt
Git add .gitignore
git commit -m "xxxx"

## <Ins>**Pour recréer la branche origin**</Ins>
git remote remove origin
git remote add origin https://github.com/stephane-chevrier/toto.lulu
git push --set-upstream origin main     //Pour pousser la branche courante et définir la distante comme amont

## <Ins>**Pour enlever d'un commit un fichier qui génère un conflit au moment d'un push **</Ins>
git restore --staged src/Main.java  // dans ce cas on eneleve le fichier Main.java

## <Ins>**Pour afficher et changer le chemin de github **</Ins>
git remote get-url origin
git remote set-url origin https://github.com/stephane-chevrier/Repository


