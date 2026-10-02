# RedLine : charte d'architecture (v0.1)

Monolithe modulaire Java 21 / Spring Boot + Next.js + PostgreSQL. Lis `docs/` avant de coder.

> État : le dépôt ne contient pour l'instant que `docs/` (phase R&D). Les règles de code s'appliquent dès l'arrivée de `backend/` et `frontend/` (phase 4).

## Langage
- Termes métier : ceux de `docs/02-domaine.md`, en français sans accents (`Candidature`, `Offre`, `Etudiant`).
- Interdits : `User`, `Job`, `Application`, `Student`, `Company`, `BaseService`, `BaseRepository`.

## Structure (un package par contexte : organisations, profil, offres, candidatures, suivi, notifications)
`api/` événements et interfaces publics · `domain/` métier pur · `application/` cas d'usage + ports ·
`infrastructure/` adaptateurs (web, persistence, source, llm, mail, scheduling).

## Règles de dépendance (contrôlées par ArchitectureTest, ne les contourne pas)
R-01 `domain` : aucun framework (ni Spring, ni Jakarta, ni Jackson, ni client HTTP).
R-02/03 `domain` et `application` ne dépendent jamais de `infrastructure`.
R-05 un module n'accède à un autre que par son package `api`. R-06 aucun cycle.
R-09 un contrôleur ne renvoie que des `*Response`. R-10 JPA seulement dans `infrastructure.persistence`.
R-12 aucun appel HTTP hors `infrastructure`. R-13 aucune donnée d'identité dans un prompt ou un log.
Front : `app` → `features` → `lib`, pas de feature vers feature, appels réseau via `lib/api` (généré).

## Ce que tu dois faire
1. Écris d'abord le test du domaine, sans infrastructure. Teste avec des adaptateurs en mémoire, pas des mocks de ports.
2. Tout appel externe (HTTP, LLM, e-mail) passe par un port. Jamais de scraping.
3. Lance `./mvnw verify` et `npm run check` et rapporte le résultat réel. Dis « non exécuté » si tu ne peux pas.
4. Pour Next.js, lis la documentation de la version installée avant d'écrire du code.
5. N'invente aucun champ d'API externe : lis la documentation officielle, sinon laisse un `TODO` avec la question.

## Ce que tu ne dois jamais faire
- Modifier `ArchitectureTest`, `ci.yml`, un seuil de couverture ou un test pour faire passer le build.
- Ajouter une dépendance sans justification (R-17) : pas de Lombok dans `domain`, pas de Redis, broker, GraphQL.
- Mettre de la logique métier dans un contrôleur, un mappeur ou du SQL.
- Coder ce qui est hors V1 (conventions, facturation, SSO, publication libre, flux de partenaires).
- Écrire des données personnelles dans un prompt, un journal ou un message d'erreur.

## Erreurs
Exceptions métier typées → `ProblemDetail` RFC 9457 dans la couche web. Jamais de trace de pile dans une réponse.

## Journal
Consigne les demandes importantes et ce qui est accepté ou refusé dans `docs/journal-ia.md`.
