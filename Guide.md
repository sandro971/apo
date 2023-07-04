<h1> Guide de survie à l'apo<s>calipse</s> théose 🐰</h1>


![Alt text](image.png)



<h2>Avant propos</h2>

<h4>Les <s>10</s> 9 commandements de l'apothéose </h4>

- <b>Les rôles des membres, vous définirez</b> :haltérophile_femme:
Avant de commencer, il est crucial de définir les rôles de chaque membre pour exploiter leurs forces, éviter la confusion lors de la répartition des tâches et disposer de référents pour chaque aspect technique du projet (par exemple, "Monsieur React", "Monsieur SQL", "Monsieur Scrum Master" etc.).
- <b>La progression, vous évaluerez</b> :fléchette:
Pour s'assurer de l'avancement du projet, il est judicieux d'organiser des réunions quotidiennes au début de chaque jour. Vous pourrez ainsi identifier rapidement les problèmes, éviter l'accumulation de dettes techniques, renforcer la cohésion de l'équipe, et avoir une vue d'ensemble sur l'avancement du projet. Parfois, des membres de l'équipe peuvent même proposer leur aide pour rattraper les tâches en retard.
- <b>Vous rendre utile et encourager les autres, vous chercherez</b> :mains_cœur:
Il est important de se rappeler que ce travail est avant tout un travail d'équipe, et que votre réussite dépend de celle de vos collègues. Soyez polis et courtois lors de vos interactions avec eux. Ce qui vous dérange peut également déranger votre interlocuteur, même s'il ne le montre pas, donc il est inutile de lui mettre le nez dans le cambouis. Proposez votre aide ou échangez les tâches pour mieux correspondre à vos capacités distincts. Personne ne peut devenir expert en quatre semaines.
- <b>Faire des pauses, vous devrez</b> :pause:
Il est également important de prendre des pauses pour prendre soin de vous. Cela n'est pas une course, mais un marathon, donc il est impératif de ne pas passer votre vie penché sur votre écran. Les pauses permettent également de prendre du recul sur votre propre travail et d'obtenir de nouvelles idées. L'accumulation de stress peut également nuire à votre travail en équipe et favoriser les conflits. N'oubliez pas de prendre des pauses carottes de temps en temps.
- <b>Poser des questions, vous n'hésiterez</b> :point_d'interrogation_rouge:
Sans omettre la règle du "Google est ton ami" ( ou même chatGPT & stackoverflow est ton ami ), pensez à échanger sur vos problèmes aussi auprès de vos collaborateurs.
Dans l'ordre, vous consulterez :
  - Les solutions numériques tels que google, stackoverflow, chatGPT
  - Vos camarades (dans votre groupe, ou d'un autre groupe d'Apo s'ils ne sont pas en mode "concentration maximale", et comme toujours le canal #entraide du Slack)
issues (propre, bien formulé et explicite, avec l'erreur, des bouts de code bien choisis, screen si besoin)
  - En dernier recours, un MP à l'équipe péda
- <b>Du code propre, vous écrirez</b> ( dette technique ) :bouton_de_commande:
Coder c'est bien mais coder lisiblement, c'est mieux ! N'oubliez pas que vous n'êtes pas seul dans votre chambre à code le prochain facebook. Il est donc de bon ton de respecter quelques règles :
  - Ajouter des commentaires clairs et concis pour comprendre les portions ciblées de votre code.
  - Utiliser une indentation cohérente et facile à lire peut améliorer la lisibilité.
  - Utiliser des noms de variables et de fonctions claires et descriptives pour améliorer la compréhension de votre code.
- <b>Utiliser des outils connues et reconnues, vous devrez</b> :construction_bâtiment:
Cela vous apportera l'assurance de trouver facilement des ressources pour vous débloquer en cas de bug 

- <b>Votre journal d'équipe / individuel, vous maintiendrez</b>
- <b>Des commits régulièrement, vous enverrez</b>

<h2 style="color: red;"> -- Sprint 0 - Entamer la conception de votre application </h2>

![Alt text](image-1.png)


<h3>1. Dans quel ordre produire les documents ?</h3>

1 - Arboressence du site
2 - Wireframe <i>( nécessite l'arboressence du site * )</i>
3 - Users Stories <i>( nécessite l'arboressence du site * )</i>
4 - MCD -> MLD -> MPD -> Dictionnaire de donnée <i>( nécessite les users stories * )</i>
5 - Route front <i>( nécessite l'arboressence * )</i>
6 - Route back <i>( nécessite le dictionnaire de donnée / MPD * )</i>




<h3>2. Les erreurs à éviter sur son MCD</h3>

- la surenchère de tables
- créer des tables pour stocker uniquement des données numériques ( dates, heures etc.. )
- utiliser des outils graphiques non prévus pour faire des MCD


<h3>3. Comment bien faire ses routes côté back ?</h3>

<h5>Listez les ressources de votre app</h5>
Prenez toutes vos tables et considérez les comme les racines de vos chemins.
Exemple :

- /user
- /article
- /commentaire

<h5>Appliquez les méthodes du CRUD à vos routes :</h5>

- GET /user
- POST /user
- DELETE /user
- PATCH /user

<h5> Pour cibler une ressource en particulier, il suffit de passer l'ID dans le chemin</h5>

GET `/article/:articleid`

<h5>Récupérer la ** liste ** d'une ressource</h5>

Exemple 1:
Pour récupérer une simple liste d'articles, pas besoin de spécifier quoi que ce soit
GET `/article` ( Vous pourrez passer une query afin de récupérer la pagination : `/article?page=25`)
* Récupérer un groupe de données d'une ressource ( Array ) qui est elle-même dépendante d'une autre ressource ( article -> commentaire )
Pour récupérer un groupe de commentaires ( Array ), il est nécessaire d'avoir l'ID de l'article en question ( 1,1 <--> 1,n )
GET `/article/:articleid/comment` ( j'accepte un `s` à `comment` )
* Pour accéder à une ressource en particulier, on a besoin que de son ID.. c'est coté back qu'on vérifiera les relations.. il n'est donc pas nécessaire de passer l'id de l'article pour supprimer un commentaire
GET `/comment/:commentid`
PATCH `/comment/:commentid`
DELETE `/comment/:commentid`
* Pour créer une nouvelle ressource, on cherche :
- À savoir si une information est prérequis mais, en règle générale, on passe toutes les données dans le body..
Exemple : Pour créer un commentaire, il faut l'ID de l'article
POST `/comment`
```JSON
body
{
    "articleid": 28,
    "message": "C'est cool !"
}
```

<h5>(Astuce) Faire ses routes au format YAML</h5>

```YML
/article (prefix)
  - / : GET
  - / : POST
  - /:id : DELETE
  - /:id : PUT
​
/comment (prefix)
  - /:articleId?page : GET (récupère une liste de commentaire)
  - /:articleId : POST ( envoie un nouveau commentaire )
  - /:id : DELETE ( supprime un commentaire en particulier )
  - /:id : PUT ( met à jour un commentaire )
​
/user (prefix)
  - / : GET
  - / : DELETE (supprime le compte)
  - / : PUT (modifie le compte)
  - /logout : DELETE (ban le token de session)
  
  - /avatar (prefix)
    - / : PUT
    - / : DELETE
```

<h3>4. Comment faire les routes côté front ?</h3>

<h3>5. Comment faire les users stories ?</h3>

<h3>6. Bien penser l'arborescence de votre site</h3>

<h2 style="color: red;"> -- Sprint 1 - On code ! </h2>

![Alt text](image-2.png)


<h3>ROADMAP côté front</h3>

Voici une roadmap pour bien débuter votre développement côté front :
- Reproduire la maquette en HTML avant de le porter sous React ( faire tourner le tout avec le plugin live server ) * facultatif mais recommandé !
(Astuce) N'hésitez pas à utiliser Sass pour plus de lisibilité
déclarer les routes ( React Router est votre ami )
- Créer les fichiers du dossier pages ( La nomenclature suit celle des routes )
- Créer les fichiers du dossier components
(Astuce) Un composant se reconnaît à plusieurs choses : Il est répété plusieurs fois dans le code, il a sa propre logique algorithmique, il n'englobe pas tout une page..
- Tester avec des fake data ( des fichiers ou json-server )
- Implémenter la vraie API



<h3>ROADMAP côté back</h3>


- <b>Les routes</b>

- <b>Les datamappers</b>

- <b>Les middlewares</b>

- <b>JWT</b>

- <b>REST et la validation des données</b>

<h2 style="color: red;"> -- Sprint 2 - On code.. encore ! </h2>

![Alt text](image-3.png)

<h2 style="color: red;"> -- Sprint 3 - On peaufine, on déploie, on flex</h2>

![Alt text](image-4.png)

<h4>1. Debugage et autres joyeusetés</h4>

<h4>2. Les plateformes de déploiement</h4>

<h4>3. On flex</h4>