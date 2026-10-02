# ADR-001 · Style d'architecture : monolithe modulaire, hexagonal dans chaque module

| | |
|---|---|
| **Statut** | Proposée (à valider au point de validation de la phase 2) |
| **Date** | 1<sup>er</sup> octobre 2026 |
| **Exigences liées** | ENF-02, ENF-05, ENF-08, ENF-14, ENF-15, ENF-16, contextes du [chapitre 02](../02-domaine.md) |

## Contexte

Un seul développeur, environ 8 heures par semaine (ENF-15), un plafond de 100 € par mois (ENF-14), une charge de pointe de 20 requêtes par seconde (ENF-02) et une exigence de disponibilité modeste (ENF-05). Le domaine se découpe en six contextes aux vocabulaires distincts ([chapitre 02](../02-domaine.md)). Deux dépendances externes volatiles : les API d'offres et le LLM. Les règles d'architecture doivent être **vérifiables par machine** (ENF-16), car l'auteur n'a pas de relecteur et une IA écrit une partie du code.

## Décision

**Un monolithe modulaire** : un seul déployable Java, divisé en **six modules**, un par bounded context. Chaque module est organisé en **architecture hexagonale** (`domain`, `application`, `infrastructure`). Les modules ne communiquent que par leur package `api` (requêtes synchrones) et par des **événements internes** publiés en mémoire après commit. Les règles sont contrôlées à chaque build par ArchUnit.

## Lien avec les exigences

| Exigence | Conséquence sur le style |
|---|---|
| ENF-15 : 1 développeur, 8 h/semaine | Un seul dépôt, un seul build, un seul déployable. Pas d'orchestrateur ni de réseau entre services à exploiter |
| ENF-02 : 20 requêtes/s en pointe | Une instance de 1 Go suffit largement. Aucun besoin de monter en charge module par module |
| ENF-14 : ≤ 100 €/mois | Trois conteneurs au total (API, web, base). Des microservices en multiplieraient le nombre |
| ENF-05 : 99,5 % | Pas de mode de panne réseau entre services, pas de transaction distribuée |
| ENF-08 : l'école ne voit que le statut global | Frontières nettes entre contextes : Suivi de promo ne peut pas lire les candidatures, il en reçoit des événements |
| ENF-16 : règles vérifiables | Packages et dépendances normalisés, donc testables avec ArchUnit |
| Dépendances volatiles (API d'offres, LLM, e-mail) | Ports et adaptateurs : remplacer un fournisseur ne touche ni le domaine ni les cas d'usage |

## Alternatives écartées

| Alternative | Pourquoi elle est écartée |
|---|---|
| **Microservices** (un service par contexte) | Un seul développeur ne peut pas exploiter six services, six pipelines et un réseau entre eux. Aucun besoin de mise à l'échelle indépendante à 20 requêtes/s. Coût d'hébergement multiplié par trois à six, ce qui dépasse le plafond. Cohérence des données (le statut global) rendue plus difficile |
| **Monolithe en couches classique** (controller, service, repository, un seul modèle) | Le plus rapide à démarrer, mais la logique glisse vers les services « fourre-tout » et les entités JPA fuient jusque dans l'API. Les frontières entre contextes ne sont pas vérifiables : l'école pourrait accidentellement lire des candidatures. Difficile à contraindre pour une IA |
| **BaaS ou serverless** (Supabase, Firebase, fonctions) | Règles métier dispersées entre fonctions et politiques de base ; dépendance forte à un fournisseur ; contradiction avec la stack choisie (Java) ; hébergement des données à vérifier au regard de la contrainte « européen » |
| **Architecture pilotée par événements avec broker** (Kafka, RabbitMQ, CQRS complet, event sourcing) | Complexité d'exploitation et de modélisation disproportionnée pour 60 000 candidatures par an. Un broker est un service de plus à héberger et à surveiller |
| **Next.js seul** (routes serveur et ORM TypeScript, sans backend Java) | Possible techniquement et moins cher, mais écarte la stack Java choisie par l'auteur pour ce projet et l'outillage ArchUnit ; les règles de dépendance y sont moins naturelles à imposer |

## Conséquences

- **Positives** : un déploiement simple, des tests rapides, un domaine isolé des frameworks, une trajectoire d'extraction possible (un module peut devenir un service si un ADR le justifie).
- **Négatives** : un seul processus (un module défaillant peut ralentir les autres), une seule base à dimensionner, et la discipline de frontières à tenir : elle ne se « sent » pas, elle se teste.
- **Réexamen** : une seconde équipe, ou un module qui demande une mise à l'échelle indépendante (l'import d'offres par exemple), ou un besoin de disponibilité supérieur à 99,9 %.
