### Système d’information :
L'ensemble des formations proposées par la plateforme est libre d’accès, de sorte que le contenu pédagogique mis à disposition par ladite formation soit un copié-collé en français des différentes formations proposées par les entreprises et/ou écoles internationales telles que Google, Harvard, le MIT, et autres. Les formations sont divisées en modules qui sont eux-mêmes divisés en chapitres. À la fin de chaque module, un QCM à résoudre se génère automatiquement en piochant aléatoirement 15 questions dans une liste de questions précédemment définie dans le but de réduire la probabilité que deux étudiants puissent être confrontés au même QCM en même temps. Seuls les utilisateurs ayant validé le QCM du module i peuvent passer au module i+1. Un module peut être payant ou non et seuls les utilisateurs inscrits, authentifiés et ayant payé leur abonnement auront accès aux modules payants. Toutes les formations proposées par la plateforme ont un module payant libellé "Pratique" qui présente les solutions expliquées de l'ensemble des examens proposés par la formation sur le site d'origine.

### Les fonctionnalités :
1.	Inscription : L'utilisateur devra fournir une adresse e-mail qui lui servira d'identifiant unique, un numéro de téléphone, son nom et son prénom. Après s'être inscrit, un e-mail de confirmation est envoyé à l'adresse renseignée.
2.	Authentification : L'application doit être disponible à la fois via un navigateur web et via une application pour smartphone (Android et iPhone). Le backend sera donc une API et l'authentification se fera via le token JWT.
3.	CRUD des formations : L'interface d'administration doit permettre aux responsables de la plateforme d'ajouter, éditer et supprimer une formation tout en gardant à l'esprit que toute formation est divisée en modules qui sont divisés en chapitres, et chaque module est lié à un questionnaire. Enfin, une question est liée à un ensemble de réponses dont une seule est vraie. Dans la base de données, les cours seront enregistrés en MARKDOWN.
4.	Suivi des cours : Ils se présenteront sous forme de texte explicatif détaillé, copié-collé du cours original, et de vidéos courtes qui se limiteront à la démonstration. Les vidéos seront hébergées sur une chaîne YouTube monétisable dédiée au projet ou aux activités du groupe. Il suffira que la plateforme émette une requête AJAX vers l’API YouTube pour les afficher.
5.	Validation du module : Un module n'est validé que si le client répond correctement à 85% du QCM lié audit module. Si l'utilisateur obtient moins de 85%, le QCM se régénère.
6.	Le paiement : Pour s'abonner, l'utilisateur doit payer les frais d'abonnement qui lui donnent accès à toutes les formations et à tous les modules gratuits ou non pendant 1 mois. L’abonnement se fait à l'inscription et les paiements se font via mobile money. Actuellement, je dispose des autorisations pour utiliser les API de MTN et d'AIRTEL. Nous verrons ensemble dans quelle mesure nous pourrons avoir un système plus global.
7.	Le Backend : Il s'agit globalement d'une API Rest pour permettre que le système soit accessible sur n'importe quel support numérique. Les réponses émises par l’API seront au format JSON.

### Modèle conceptuel des données

1. Dictionaire des données élémentaires

| Name         | Type   | Constraint | NULL     | Default | Description                         |
|--------------|--------|------------|----------|---------|-------------------------------------|
| lastname     | string |            | NOT NULL |         |                                     |
| firstname    | string |            |          |         |                                     |
| email        | string | UNIQUE     | NOT NULL |         | email user                          |
| password     | string |            | NOT NULL |         |                                     |
| label        | string | UNIQUE     | NOT NULL |         | label formation                     |
| description  | text   |            |          |         | description formation               |
| title        | string | UNIQUE     | NOT NULL |         | title module                        |
| price        | float  |            |          | 0.      | price module                        |
| formation_id | int    | FK         | NOT NULL |         | module FK reference to formation id |
| title        | string | UNIQUE     | NOT NULL |         | title chapter                       |
| content      | text   |            | NOT NULL |         | content chapter                     |
| module_id    | int    | FK         | NOT NULL |         | chapter FK reference to module id   |
| content      | text   |            | NOT NULL |         | content QCM                         |
| value        | int    |            | NOT NULL | false   | Answer value 1 or 0                 |
| qcm_id       | int    | FK         | NOT NULL |         | answer FK reference to QCM id       |

2. Diagramme
[![](https://mermaid.ink/img/pako:eNqdU11PwjAU_StNn5kRxhjujQBGIx8KGhOzxNTtok26dnadX9v-u91aIwM1xD6155x7bnt7b4EjEQMOsOM4IVdUMQjQWPAIUpUThmKiCEq0hIW8kYQc5ISSR0mSkCO9btbTFSpLxxEFmi5Wy9kMBUgyZViLVJovS3S6XM1H1-fLhZF0jeYbrW3KAs2Xk5vZ1Gh6RmMh6zM-G11e67SNwm0phLG4Gs8N2zdsfbbuo8X69ivW23pDYfb1olwhGqPLi28oU5LyR8RIpjhJYI_YUPkLAwmhbA9NSZa9ChkbotqtxIGXeYB95xiySNJUUcFb5vYr9pzb5zwDea_TnV608Y2QCak9t8mqVfqD7ty0WFuYShrB4dns5_8nm0UjwRVw1TbQTZ4z-CFf3ToHJWvZ2mDbbH_H19ALYflOEZ6jZOc6uIMT0JWhsZ7YxjPE6gl00-FAb2PYkFxPHg55paUkV2L9ziMcKJlDB-epnmaww_sFpoTjoMBvOHAH3lHX7Xc9r-e7fdf3Ovhdo8dH_snQ9Xu9wXDgD3xvWHXwhxDaoNtE3zX7DWEZVJ-jmj-g?type=png)](https://mermaid.live/edit#pako:eNqdU11PwjAU_StNn5kRxhjujQBGIx8KGhOzxNTtok26dnadX9v-u91aIwM1xD6155x7bnt7b4EjEQMOsOM4IVdUMQjQWPAIUpUThmKiCEq0hIW8kYQc5ISSR0mSkCO9btbTFSpLxxEFmi5Wy9kMBUgyZViLVJovS3S6XM1H1-fLhZF0jeYbrW3KAs2Xk5vZ1Gh6RmMh6zM-G11e67SNwm0phLG4Gs8N2zdsfbbuo8X69ivW23pDYfb1olwhGqPLi28oU5LyR8RIpjhJYI_YUPkLAwmhbA9NSZa9ChkbotqtxIGXeYB95xiySNJUUcFb5vYr9pzb5zwDea_TnV608Y2QCak9t8mqVfqD7ty0WFuYShrB4dns5_8nm0UjwRVw1TbQTZ4z-CFf3ToHJWvZ2mDbbH_H19ALYflOEZ6jZOc6uIMT0JWhsZ7YxjPE6gl00-FAb2PYkFxPHg55paUkV2L9ziMcKJlDB-epnmaww_sFpoTjoMBvOHAH3lHX7Xc9r-e7fdf3Ovhdo8dH_snQ9Xu9wXDgD3xvWHXwhxDaoNtE3zX7DWEZVJ-jmj-g)
