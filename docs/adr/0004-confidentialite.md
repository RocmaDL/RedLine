# ADR-004 · Confidentialité par conception : l'école ne voit que le statut global

| | |
|---|---|
| **Statut** | Proposée |
| **Date** | 1<sup>er</sup> octobre 2026 |
| **Exigences liées** | ENF-07, ENF-08, ENF-11, EF-15, EF-16, EF-20 |

## Contexte

La différence du produit ([chapitre 01](../01-probleme.md), §5) est que l'école suit sa promo sans accéder au détail de la recherche de chaque étudiant. C'est la **décision la plus coûteuse à changer** : elle traverse chaque table, chaque requête et chaque test, et elle engage une promesse faite aux étudiants.

## Décision

1. **Tenant = école.** Chaque donnée rattachée à une école porte un `ecole_id`. Les ports de repository exigent un `EcoleId` : une requête sans école ne compile pas.
2. **Le suivi est un modèle de lecture séparé** (`suivi.statut_global`), alimenté uniquement par des événements. **Aucune route ne renvoie une candidature, une offre enregistrée ou une lettre à un rôle école.**
3. **Le statut global est calculé**, jamais saisi par l'école ([chapitre 02](../02-domaine.md), §4). Le placement est **déclaré** par l'étudiant et **confirmé** par le référent ; chaque confirmation est journalisée (EF-20).
4. **Test d'autorisation par rôle** : pour chaque route, un test vérifie qu'un étudiant ne lit que ses données, qu'un référent ne lit que le suivi de sa propre école, et qu'une école n'accède jamais à une autre.

## Alternatives écartées

| Alternative | Pourquoi elle est écartée |
|---|---|
| L'école voit tout le pipeline (c'est ce que font les concurrents) | Détruit la différence du produit et la confiance des étudiants ; surface RGPD plus large |
| Consentement fin par étudiant (il choisit ce qu'il partage) | Pertinent, mais complexe pour la V1 ; reportable sans casser le modèle |
| L'école ne voit que des chiffres agrégés | Elle ne pourrait pas agir sur un étudiant précis : le produit perd sa valeur d'alerte |
| Isolation par ligne dans PostgreSQL (Row Level Security) comme seule protection | Utile en seconde défense mais lourde avec JPA et le pool de connexions ; à évaluer plus tard |

## Conséquences

Chaque nouvelle fonction du suivi passe par un événement, ce qui ralentit un peu le développement. En échange, une fuite de données vers l'école devient structurellement difficile. Réexamen : un entretien d'école qui exigerait le détail, ou une obligation légale.
