# RedLine

> Le suivi d'alternance et de stage pour les écoles privées post-bac, sans exposer le détail de la recherche de chaque étudiant.

Projet fil rouge « Architecture logicielle », phase R&D. Auteur : Rocma (équipe d'une personne). Statut : **brouillon de recherche du 1er octobre 2026**, le code arrive en phase 4.

> [!NOTE]
> Le nom **RedLine** (choisi par l'auteur le 2 octobre 2026, à la place du nom de travail « Passerelle ») n'a pas fait l'objet d'une vérification de disponibilité (marque, domaine).

## Le produit

- **L'étudiant** (gratuit) suit ses candidatures d'alternance et de stage et génère ses lettres de motivation avec l'aide d'une IA.
- **L'école** (payeur) voit un **statut global** par étudiant, reçoit des alertes et une synthèse de promo, et invite des entreprises partenaires. Elle ne voit jamais le détail des candidatures.
- **Les offres** viennent d'API officielles (La Bonne Alternance, France Travail) et des entreprises invitées. **Jamais de scraping.**

## L'architecture en six lignes

1. **Monolithe modulaire** Java 21 / Spring Boot : un seul déployable, six modules, un par bounded context ([ADR-001](docs/adr/0001-style.md)).
2. **Hexagonal dans chaque module** : le domaine ne dépend d'aucun framework, les API externes et le LLM sont derrière des ports ([ADR-003](docs/adr/0003-patterns.md)).
3. **Un seul PostgreSQL, un schéma par contexte**, aucune jointure entre schémas ; événements internes en mémoire, après commit.
4. **Next.js** (TypeScript) pour l'interface, client d'API généré depuis l'OpenAPI du backend.
5. **PaaS européen** (Scalingo en premier choix), environ 72 €/mois prévus pour un plafond de 100 € ([ADR-002](docs/adr/0002-stack.md)).
6. **Garde-fou** : ArchUnit côté Java, dependency-cruiser côté front, en intégration continue. La charte est lue par l'IA via [`AGENTS.md`](AGENTS.md).

## Documentation

| Livrable | Fichier |
|---|---|
| Fiche problème | [docs/01-probleme.md](docs/01-probleme.md) |
| Analyse de marché (taille, concurrents, réglementation, risques) | [docs/analyse-marche.md](docs/analyse-marche.md) |
| Domaine : événements, bounded contexts, glossaire, context map | [docs/02-domaine.md](docs/02-domaine.md) |
| Exigences fonctionnelles et non fonctionnelles chiffrées | [docs/03-exigences.md](docs/03-exigences.md) |
| Décisions d'architecture (ADR-001 à 005) | [docs/adr/](docs/adr/README.md) |
| Diagrammes C4 (contexte, conteneurs, composants) | [docs/c4/](docs/c4/README.md) |
| Charte d'architecture (version complète) | [docs/06-charte.md](docs/06-charte.md) |
| Charte pour l'IA (version courte) | [AGENTS.md](AGENTS.md) |
| Journal d'usage de l'IA | [docs/journal-ia.md](docs/journal-ia.md) |

## Ce qui est un fait, ce qui est une hypothèse

Les chiffres de marché viennent de sources citées dans la [fiche problème](docs/01-probleme.md). Tout le reste est étiqueté `Hypothèse` : les chiffres de dimensionnement ([exigences](docs/03-exigences.md)), le choix de l'hébergeur ([ADR-002](docs/adr/0002-stack.md)) et le flux « l'étudiant déclare, le référent confirme » n'ont pas été validés avec une école ni un étudiant.

## Ce qui reste à faire

- **Phase 4** : arborescence `backend/` et `frontend/`, test d'architecture ArchUnit, intégration continue, squelette du module Offres.
- Validation de l'idée et de la taille de l'équipe par le formateur.
- Entretiens avec des écoles pour confirmer les hypothèses, et réponse écrite de la DGEFP sur les conditions de l'API La Bonne Alternance ([analyse de marché](docs/analyse-marche.md), §4 et §6).
- Relecture personnelle du [journal IA](docs/journal-ia.md), reconstitué à partir de la conversation de travail.

## Ce que nous ne ferons pas en V1

Conventions et contrats d'apprentissage, facturation, publication libre des offres par les entreprises (elles sont invitées par l'école), flux de job boards partenaires, recommandation d'étudiants aux entreprises, intégration aux ERP de CFA (Ypareo, Ymag, Digiforma), application mobile native, et le **scraping, jamais**.
