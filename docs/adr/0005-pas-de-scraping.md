# ADR-005 · Offres issues de sources officielles uniquement, aucun scraping

| | |
|---|---|
| **Statut** | Proposée |
| **Date** | 1<sup>er</sup> octobre 2026 |
| **Exigences liées** | ENF-19, EF-08, EF-09 |

## Contexte

Le projet précédent de l'auteur (un prototype de moteur d'offres) reposait sur un module de scraping de plusieurs job boards. Il a été écarté pour ce produit : l'auteur ne veut plus de scraping.

## Décision

Les offres proviennent de **deux voies seulement** : les **API officielles** (La Bonne Alternance, France Travail) et les **entreprises partenaires invitées par l'école**. Les sources sont branchées derrière le port `OffreSource` et traduites par une couche anti-corruption. Les partenariats avec des job boards ou des flux d'agrégateurs seront ajoutés plus tard par de nouveaux adaptateurs du même port, après accord écrit.

## Alternatives écartées

| Alternative | Pourquoi elle est écartée |
|---|---|
| Scraping de job boards | Choix de l'auteur ; conditions d'utilisation des sites ; fragilité (le site change, le scraper casse) ; coût de maintenance incompatible avec un développeur à temps partiel |
| Achat d'un flux d'agrégateur | Coût non chiffré, hors budget de la V1 |
| Saisie manuelle uniquement | Trop pauvre pour l'étudiant ; reste possible pour une piste hors plateforme (EF-11) |

## Conséquences

Une couverture plus étroite (surtout des stages, dont la couverture par les API n'est pas confirmée), mais un risque juridique et de maintenance beaucoup plus faible. Il faudra **lire et respecter les conditions** d'attribution et d'affichage de chaque API ([chapitre 01](../01-probleme.md), §8) avant la mise en production.
