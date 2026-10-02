# Charte d'architecture

*Règles de dépendance, conventions, tests, erreurs, consignes à l'IA*

La charte est le contrat de l'équipe et de l'IA. Elle est **précise** (pas de « bonnes pratiques » vagues) et **vérifiable** (chaque règle porte un numéro et dit qui la contrôle). Sa version courte, lue par l'outil d'IA, est le fichier `AGENTS.md` à la racine ([AGENTS.md](../AGENTS.md)). Ce document est la version complète.

## 1. Principes

1. **Le domaine d'abord.** Le métier est écrit dans le langage du glossaire ([chapitre 02](02-domaine.md)) et ne dépend d'aucun framework.
2. **Les frontières se testent.** Une règle qu'aucun test ne contrôle n'est pas une règle.
3. **Le plus simple qui tienne les exigences.** Pas de technologie sans besoin mesuré (ADR-003).
4. **L'IA propose, l'auteur dispose.** Tout code généré est relu ; les demandes importantes sont consignées ([chapitre 08](journal-ia.md)).

## 2. Organisation des dossiers

```text
redline/
├── AGENTS.md                  # la charte, lue par l'IA et par l'équipe
├── CLAUDE.md                  # une ligne : @AGENTS.md
├── README.md                  # comment lancer le projet
├── docker-compose.yml         # PostgreSQL pour le développement local
├── .github/workflows/ci.yml   # analyse, tests, garde-fous
├── docs/
│   ├── 01-probleme.md  02-domaine.md  03-exigences.md
│   ├── adr/                   # 0001-style.md, 0002-stack.md, 0003-patterns.md …
│   ├── c4/                    # contexte, conteneurs, composants (SVG + sources)
│   └── journal-ia.md
├── backend/                   # Java 21, Spring Boot, Maven
│   ├── pom.xml
│   └── src/
│       ├── main/java/fr/redline/
│       │   ├── RedLineApplication.java
│       │   ├── partage/       # noyau technique minimal, sans logique métier
│       │   ├── organisations/ ┐
│       │   ├── profil/        │  un package racine par bounded context,
│       │   ├── offres/        │  chacun organisé ainsi :
│       │   ├── candidatures/  │    api/             événements et interfaces publics
│       │   ├── suivi/         │    domain/          agrégats, objets-valeurs, règles
│       │   └── notifications/ ┘    application/     cas d'usage + ports (interfaces)
│       │                           infrastructure/  adaptateurs : web, persistence,
│       │                                            source, llm, mail, scheduling
│       ├── main/resources/db/migration/   # V001__offres_creer_schema.sql …
│       └── test/java/fr/redline/       # ArchitectureTest + un dossier de tests par module
└── frontend/                  # Next.js, TypeScript
    ├── package.json  .dependency-cruiser.cjs
    └── src/
        ├── app/               # routes et mises en page uniquement
        ├── features/          # offres, candidatures, suivi, profil, organisations
        └── lib/               # api (client généré), ui, utilitaires
```

## 3. Règles de dépendance

Chaque règle a un numéro, repris dans les messages de test et dans `AGENTS.md`.

### Backend

| N° | Règle | Contrôlée par |
|---|---|---|
| **R-01** | `domain` ne dépend d'aucun framework : ni Spring, ni Jakarta (persistance, validation), ni Jackson, ni client HTTP | ArchUnit `ArchitectureTest` |
| **R-02** | `domain` et `application` ne dépendent jamais de `infrastructure` | ArchUnit |
| **R-03** | `domain` ne dépend pas de `application` | ArchUnit |
| **R-04** | `application` ne dépend que de `domain`, de `partage`, de l'`api` d'un autre module et d'un petit lot d'annotations Spring autorisées (`@Transactional`) | ArchUnit |
| **R-05** | Un module n'accède à un autre module que par son package `api` | ArchUnit, règle personnalisée |
| **R-06** | Aucun cycle entre modules | ArchUnit `slices()` |
| **R-07** | `partage` ne dépend d'aucun module | ArchUnit |
| **R-08** | Injection par constructeur uniquement ; `@Autowired` sur un attribut est interdit | ArchUnit |
| **R-09** | Les contrôleurs ne renvoient ni objet de domaine ni entité JPA, seulement des `*Response` | ArchUnit |
| **R-10** | `jakarta.persistence` n'apparaît que dans `infrastructure.persistence` | ArchUnit |
| **R-11** | Un script de migration ne référence que le schéma de son propre contexte | Test de migration (analyse des fichiers `.sql`) |
| **R-12** | Aucun appel HTTP sortant hors de `infrastructure` | ArchUnit |
| **R-13** | Aucune donnée d'identité dans un prompt ou un journal : le port `AssistantRedaction` n'accepte qu'un `ContexteLettre` sans nom, e-mail ni adresse | Typage du port + test du constructeur de prompt |

### Frontend

| N° | Règle | Contrôlée par |
|---|---|---|
| **R-14** | `app` → `features` → `lib` : jamais en sens inverse ; une feature n'importe pas une autre feature | dependency-cruiser |
| **R-15** | Les appels réseau passent uniquement par `lib/api` (client généré, jamais édité à la main) | dependency-cruiser, génération en CI |
| **R-16** | Aucun secret ni adresse de service externe dans le code front ; seules les variables `NEXT_PUBLIC_*` publiques sont lisibles | ESLint, revue |

### Processus

| N° | Règle | Contrôlée par |
|---|---|---|
| **R-17** | Toute nouvelle dépendance (`pom.xml`, `package.json`) est justifiée en une phrase dans la demande de fusion ; si elle est structurante, un ADR la précède | Revue, modèle de PR |
| **R-18** | Un ADR n'est jamais modifié : on le remplace par un nouvel ADR (« Remplace ADR-00x ») | Revue |
| **R-19** | `mvn verify` et `npm run check` sont verts avant de proposer un commit | CI |

## 4. Patterns imposés : où et pourquoi

| Pattern | Où | Pourquoi (ADR-003) |
|---|---|---|
| Ports et adaptateurs | Chaque module | Isoler le domaine des API externes, du LLM et de l'e-mail |
| Cas d'usage (une classe, une action) | `application.usecase` | Une action métier lisible et testable |
| Repository | Port dans `application.port`, adaptateurs dans `infrastructure.persistence` | Le domaine ignore la base |
| Couche anti-corruption | `offres.infrastructure.source` | Les DTO externes restent dans l'adaptateur |
| Événements en mémoire, après commit | Entre modules | Découpler sans broker |
| Modèle de lecture | `suivi` | Tableaux de bord sans accès aux candidatures |
| Erreurs RFC 9457 | `infrastructure.web` | Format d'erreur unique |

Les patterns interdits sont listés dans l'ADR-003 ; ils sont repris dans la section « Interdits » de `AGENTS.md`.

## 5. Conventions de nommage

| Élément | Convention | Exemple |
|---|---|---|
| Termes du métier | Français, sans accents, **exactement ceux du glossaire** | `Candidature`, `StatutGlobal`, `Promotion` |
| Termes techniques | Anglais | `Repository`, `Controller`, `Adapter` |
| Cas d'usage | Verbe à l'infinitif + objet | `ImporterOffres`, `DeclarerPlacement` |
| Port sortant | Nom du besoin métier, sans technologie | `OffreSource`, `OffreRepository`, `AssistantRedaction`, `Courrier`, `Horloge` |
| Adaptateur | Technologie + port | `PostgresOffreRepository`, `InMemoryOffreRepository`, `LaBonneAlternanceOffreSource` |
| Événement | Participe passé, un `record` dans `api` | `CandidatureEnvoyee`, `PlacementDeclare` |
| Contrôleur et DTO | `<Ressource>Controller`, `<Action>Request`, `<Ressource>Response` | `SuiviPromoController`, `SuiviEtudiantResponse` |
| Tests | `<Classe>Test` (sans infrastructure), `<Classe>IT` (avec infrastructure) | `CandidatureTest`, `PostgresOffreRepositoryIT` |
| Méthodes de test | Phrase métier en `snake_case` français | `refuse_une_transition_depuis_un_etat_final` |
| Tables et colonnes | `snake_case`, une table par agrégat, dans le schéma du contexte | `candidatures.candidature`, `etudiant_id` |
| Migrations | `V<numéro à 3 chiffres>__<contexte>_<action>.sql` | `V003__candidatures_creer_index_acceptee.sql` |
| Fichiers front | `kebab-case` ; composants en `PascalCase` | `suivi-promo-table.tsx`, `SuiviPromoTable` |
| Commits et branches | Conventional Commits ; `feat/…`, `fix/…`, `docs/…` | `feat(offres): importer les offres de La Bonne Alternance` |

**Synonymes interdits** : on n'écrit jamais `User`, `Job`, `Application`, `Student` ou `Company` dans le code. On écrit `Etudiant`, `Offre`, `Candidature`, `EntreprisePartenaire`. Un nouveau terme métier entre d'abord dans le glossaire.

## 6. Stratégie de tests

| Niveau | Ce qu'il teste | Outils | Infrastructure | Cible |
|---|---|---|---|---|
| **Domaine** | Agrégats, objets-valeurs, règles (transitions, échéances) | JUnit 5, AssertJ | **Aucune**, millisecondes | La majorité des tests |
| **Application** | Cas d'usage avec des **adaptateurs en mémoire** (fausses implémentations, pas de mocks de ports) | JUnit 5, AssertJ | **Aucune** | Chaque cas d'usage, cas nominal et chaque erreur |
| **Contrat de port** | Un même jeu de tests exécuté sur **tous** les adaptateurs d'un port (en mémoire et réel) | JUnit 5, classe abstraite | Base pour l'adaptateur réel | Chaque port `Repository` |
| **Adaptateurs** | Persistance contre un vrai PostgreSQL ; clients HTTP contre un faux serveur | Testcontainers, WireMock | Docker | Chaque adaptateur réel |
| **Architecture** | Règles R-01 à R-13 | ArchUnit | **Aucune** | À chaque build |
| **Autorisation** | Un test par route et par rôle : qui lit quoi (ADR-004) | Spring MockMvc | Base de test | Toutes les routes |
| **Interface** | 3 à 5 parcours critiques de bout en bout | Playwright | Pile complète en local | Connexion, enregistrer une candidature, vue du référent |
| **Front** | Composants et fonctions pures | Vitest | Aucune | Logique non triviale |

Seuil : **80 % de couverture de lignes** sur `domain` et `application` (JaCoCo, le build échoue en dessous). Pas de seuil sur `infrastructure` : on teste ce qui se casse, pas pour atteindre un chiffre. Un bogue corrigé reçoit d'abord un test qui l'exprime.

## 7. Gestion des erreurs

**Principe.** Le domaine lève des exceptions **métier typées** ; la couche web les traduit en réponses **RFC 9457** (`ProblemDetail`). Jamais de trace de pile dans une réponse. Jamais d'exception avalée en silence.

| Situation | Exception | Levée dans | Statut HTTP | `code` |
|---|---|---|---|---|
| Entrée mal formée | validation Spring | web | 400 | `validation` + liste des violations |
| Non authentifié | — | Spring Security | 401 | `non-authentifie` |
| Mauvais rôle ou autre école | `AccesInterdit` | application | 403 | `acces-interdit` |
| Ressource absente (ou d'une autre école : on ne révèle pas son existence) | `RessourceIntrouvable` | application | 404 | `introuvable` |
| Doublon ou conflit | `ConflitMetier` | domain | 409 | `conflit` |
| Règle métier violée (transition interdite) | `TransitionInterdite` (hérite de `RegleMetierViolee`) | domain | 422 | `transition-interdite` |
| Quota de lettres atteint | `QuotaAtteint` | application | 429 | `quota-atteint` |
| Service externe indisponible, appel synchrone | `SourceIndisponible` | adaptateur | 503 | `service-indisponible` |
| Erreur imprévue | — | — | 500 | `erreur-interne` |

- Chaque réponse d'erreur porte `type`, `title`, `status`, `detail`, un `code` stable et un `correlationId` repris dans les journaux. Le `type` est une URI de documentation `domaine à définir`.
- **Appel sortant** : l'adaptateur applique délai d'attente, reprise exponentielle et disjoncteur (Resilience4j), puis lève `SourceIndisponible`. C'est le **cas d'usage** qui décide quoi faire : l'import nocturne journalise et émet `ImportDOffresEchoue` ; la génération d'une lettre répond 503 et propose de réessayer.
- **Journaux** : JSON, avec identifiant de requête ; **aucune donnée personnelle** (identifiants techniques seulement) ; niveau `ERROR` réservé à ce qui exige une action.
- **Front** : un composant d'erreur affiche `title` et `detail` ; un identifiant de corrélation est montré pour le support.

## 8. Règles données à l'IA

Ces règles sont copiées dans `AGENTS.md`. Elles sont écrites à l'impératif, une par ligne, pour être appliquées sans interprétation.

1. **Lire `AGENTS.md` et `docs/` avant de coder.** Utiliser les mots du glossaire, aucun synonyme (§5).
2. **Ne jamais modifier** `ArchitectureTest`, `ci.yml`, un seuil de couverture ou un test existant **pour faire passer le build**. Si une règle gêne, le dire et proposer un ADR.
3. **Ne pas ajouter de dépendance** sans la justifier (R-17). Pas de Lombok dans `domain`, pas de bibliothèque de mapping automatique, pas de cache distribué, pas de GraphQL.
4. **Le domaine est pur** : aucune annotation Spring, JPA ou Jackson dans `domain` (R-01).
5. **Aucune logique métier dans un contrôleur, un mappeur, un trigger ou une requête SQL.**
6. **Tout appel externe (HTTP, LLM, e-mail) passe par un port** dont l'adaptateur vit dans `infrastructure` (R-12). **Jamais de scraping.**
7. **Aucune donnée personnelle** dans un prompt, un journal ou un message d'erreur (R-13).
8. **Écrire le test du domaine d'abord**, puis le code. Tester avec des adaptateurs en mémoire, pas avec des mocks de ports.
9. **N'inventer aucune API externe** : pour La Bonne Alternance et France Travail, lire la documentation officielle ; si un champ est incertain, laisser un `TODO` avec la question, ne pas le deviner.
10. **Avant Next.js** : la bibliothèque évolue vite ; lire la documentation de **la version installée** et ses avis de dépréciation plutôt que se fier à la mémoire du modèle.
11. **Ne pas élargir le périmètre** : ce qui est hors V1 ([chapitre 03](03-exigences.md), §5) ne se code pas.
12. **Exécuter `mvn verify` et `npm run check`** et rapporter le résultat réel. Dire « je n'ai pas pu exécuter » plutôt que supposer que ça passe.
13. **Consigner** dans `docs/journal-ia.md` les demandes importantes et ce qui a été accepté ou refusé.

### Ce que l'IA ferait mal si on ne le lui interdisait pas

Réponse à l'une des quatre questions de la revue. Chaque dérive prévisible a son garde-fou.

| Dérive prévisible | Pourquoi l'IA le fait | Garde-fou |
|---|---|---|
| Mettre des annotations JPA ou Jackson dans le domaine « pour aller plus vite » | Le chemin le plus court vers du code qui compile | R-01 et R-10, ArchUnit fait échouer le build |
| Appeler l'API ou le LLM directement depuis un service | Un appel direct est plus court qu'un port | R-12 ; port avec type restreint (R-13) |
| Renvoyer l'entité telle quelle dans l'API | Évite d'écrire un DTO | R-09 ; et ADR-004 : l'école ne doit rien voir de plus |
| Créer un `User`, un `Job` ou un `BaseService<T>` générique | Vocabulaire et abstractions de ses données d'entraînement | Glossaire imposé, interdits de l'ADR-003, revue |
| Modifier un test ou la CI pour faire passer le build | Cherche à « réussir » | Règle 2 ; changement de `ArchitectureTest` ou `ci.yml` relu à la main |
| Ajouter Lombok, MapStruct, Redis, un broker | Habitudes de projets standards | R-17 : justification obligatoire |
| Inventer des champs ou des routes d'API externes | Complète ce qu'il ne connaît pas | Règle 9 ; test d'adaptateur contre une réponse réelle enregistrée |
| Envoyer nom ou e-mail dans un prompt | Contexte plus riche = lettre plus personnelle | Le type `ContexteLettre` ne contient pas ces champs |
| Écrire du code Next.js d'une ancienne version | Connaissance figée à une date | Règle 10 |
| Sur-développer (conventions, facturation, SSO) | Ne connaît pas le périmètre | Règle 11 ; liste « hors V1 » |
| Affirmer que les tests passent sans les lancer | Optimisme | Règle 12 ; CI comme arbitre |

## 9. Faire évoluer la charte

La charte se modifie par demande de fusion, avec la référence de l'ADR qui l'impose (R-18). Un changement de règle de dépendance modifie **dans le même commit** le test ArchUnit et ce chapitre. Version courante : **0.1**, 1<sup>er</sup> octobre 2026.
