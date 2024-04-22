## Compte rendu théorique

### Etat des lieux
1. Il n'y a pas de CI/CD
2. Il n'y a pas de tests automatisés
3. Il n'y a pas de commande de build ou autres commandes stockés dans un fichier
4. Il y a un seul support qui sert à installer et lancer l'application qui est le fichier README.md qui contient les commandes suivantes
<br>Installation -> `mvn clean package`
<br>Démarrage de l'application -> `java -jar brick-game-0.3.0-SNAPSHOT.jar`
<br>
La commande de démarrage nous a indiqué le nom de l'image jar qui contient l'application

### Problèmes rencontrés
1. Lorsqu'on a cloné le projet, nous avions des erreurs concernant la dépendance Lombok
qui bloquait la compilation et le build du projet.<br>
_Correctif_ : Nous avons mis à niveau les versions de _lombok_ et _lombok-maven-plugin_
2. Il y avait des problèmes au niveau des tests qui étaient mal configurés (Mockito ne peut pas mocker des classes finales).
_Correctif_ : Pour pouvoir compiler et packager, nous avons décidé d'ignorer les tests pour le moment `mvn compile package -DskipTests`


### Ce que nous comptons faire
1. Corriger les tests
2. Créer une pipeline Jenkins qui permet de a) tester b) builder et c) enregistrer l'image créée
3. Tester chaque étape du pipeline
4. Si nous avons du temps nous pourrons rajouter une étape de publication de l'image sur un registry mais aussi un versionnage automatique qui upgrade la version du jar selon les tags des releases
<br>Release majeur -> de 1.0.0 à 2.0.0
<br>Release mineure -> de 1.0.0 à 1.1.0
<br>release hotfix -> de 1.0.0 à 1.0.1
5. Si nous avons du temps nous pourrons également rajouter des Github Actions pour valider les PR (SonarQube -> code coverage, Checkmarx -> SAST & DAST..)


### Jenkins
1. Nous allons créer un projet Pipeline que nous allons configurer
2. Nous prenons le pipeline d'exemple Github + Maven que l'on configure avec lien vers notre repo
3. Nous rajoutons maven (Configuration tools -> Install Maven)
4. Nous créons un fichier Jenkinsfile que nous rajoutons dans notre projet
5. Nous effectuons un push sur le remote repository et lorsqu'on vérifie le résultat du pipeline nous remarquons l'évolution des tests
