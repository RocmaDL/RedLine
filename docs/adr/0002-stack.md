# ADR-002 · Stack : Java 21 / Spring Boot, Next.js, PostgreSQL, PaaS européen

| | |
|---|---|
| **Statut** | Proposée |
| **Date** | 1<sup>er</sup> octobre 2026 |
| **Exigences liées** | ENF-09, ENF-14, ENF-15, ENF-16, ENF-18 |

## Contexte

La stack est libre mais doit se justifier. Contraintes posées par l'auteur : **équipe de un**, **Java Spring Boot + Next.js + PostgreSQL**, **PaaS européen**, **moins de 100 € par mois**. Une IA participe à l'écriture : les technologies choisies doivent être très documentées et testables sans infrastructure.

## Décision

| Couche | Choix | Justification |
|---|---|---|
| **Langage backend** | Java 21 (LTS) | Typage fort adapté au domaine ; écosystème de tests et d'ArchUnit ; choix de l'auteur |
| **Framework backend** | Spring Boot : Web, Security, Validation, Data JPA, Actuator, Session JDBC | Standard, très documenté ; les modules s'y branchent sans que le domaine le sache |
| **Build** | Maven | Conventions stables ; un seul module Maven et six packages racines, pas de multi-modules Maven |
| **Persistance** | PostgreSQL ; Flyway (migrations) ; Spring Data JPA **uniquement dans les adaptateurs** | Base relationnelle fiable, schémas par contexte, migrations versionnées |
| **Appels sortants** | Spring `RestClient` + Resilience4j (délai d'attente, reprise, disjoncteur) | Les API externes tombent ; l'import doit survivre |
| **Contrat d'API** | OpenAPI généré par springdoc → client TypeScript généré | Un seul contrat, pas de types recopiés à la main |
| **Frontend** | Next.js (App Router), TypeScript strict, Tailwind CSS | Choix de l'auteur ; rendu serveur pour les pages publiques ; version à figer au démarrage |
| **Tests backend** | JUnit 5, AssertJ, Testcontainers (PostgreSQL), WireMock, ArchUnit, JaCoCo | Tests sans infrastructure pour le domaine ; vraie base pour les adaptateurs |
| **Tests frontend** | Vitest, Playwright (3 à 5 parcours critiques), dependency-cruiser | Règles de dépendance côté front vérifiables |
| **Authentification** | Comptes locaux, Spring Security, sessions en base (Spring Session JDBC), cookie `HttpOnly` | Pas de service tiers ; tout reste en Europe ; SSO d'école reportable |
| **Hébergement** | **Scalingo** (PaaS français) en premier choix | Voir ci-dessous |
| **E-mail transactionnel** | Fournisseur européen à choisir, derrière un port `Courrier` | Interchangeable ; pas de prix affirmé ici |
| **Fournisseur LLM** | À choisir parmi les fournisseurs traitant les données dans l'UE (Mistral AI est un candidat), derrière le port `AssistantRedaction` | Interchangeable ; DPA obligatoire (ENF-09) |
| **Intégration continue** | GitHub Actions ; déploiement depuis `main` | Gratuit pour un dépôt de cette taille `À confirmer` |

## Hébergement : pourquoi Scalingo en premier choix

Prix relevés sur la page tarifaire de Scalingo le 1<sup>er</sup> octobre 2026, HT, région standard : conteneur M (512 Mo) 14,40 €, conteneur L (1 Go) 28,80 €, PostgreSQL Starter (512 Mo, 10 Go) 7,20 €, sauvegardes quotidiennes comprises. Soit **50,40 € par mois** pour la plateforme, dans le plafond ([chapitre 03](../03-exigences.md), §4).

| Option | Avantages | Raison de ne pas la retenir en premier |
|---|---|---|
| **Scalingo** (France) | PaaS : déploiement par `git push`, base gérée avec sauvegardes quotidiennes, société française, prix affichés | **Retenu en premier choix.** Le lieu exact du centre de données n'est pas précisé sur la page de tarifs : à confirmer avant de signer |
| **Clever Cloud** (France) | PaaS français comparable, facturation à la seconde | Prix non lisibles dans la page consultée (estimateur interactif) : comparaison à faire avant la décision finale |
| **VPS Hetzner ou serveur OVHcloud** | Le moins cher | Ce n'est pas un PaaS : mises à jour, sauvegardes, certificats et supervision reposent sur un seul développeur à 8 h par semaine |
| **OVHcloud ou Scaleway, conteneurs managés** | Hébergeurs européens, plus de contrôle | Plus d'assemblage à faire (registre, réseau, base séparée) que sur un PaaS |
| **Vercel, Render, Fly.io** | Très simples | Écartés par la contrainte « PaaS européen » |

**Réversibilité.** Le backend et le front sont des applications standard (variables d'environnement, base PostgreSQL standard, aucune API propriétaire du PaaS). Changer d'hébergeur coûte quelques jours, pas une réécriture.

## Alternatives écartées sur la persistance

| Alternative | Pourquoi pas |
|---|---|
| jOOQ | Très bon outil SQL, mais courbe d'apprentissage supplémentaire pour un projet à une personne ; à reconsidérer pour les requêtes de synthèse |
| Spring Data JDBC | Proche des agrégats DDD, mais les annotations de mapping se placeraient sur le domaine ou obligeraient à dupliquer : même coût que JPA, écosystème plus petit |
| Base documentaire | Les relations (promo, étudiant, candidature) et les contraintes (index unique partiel) sont naturellement relationnelles |

## Conséquences

- **Positives** : stack très documentée (utile à l'IA), coût de plateforme maîtrisé, aucune dépendance propriétaire.
- **Négatives** : deux écosystèmes à maintenir (Java et TypeScript) pour un seul développeur ; Java demande plus de mémoire que Node (d'où le conteneur de 1 Go pour l'API).
- **Réexamen** : si la base dépasse le palier Starter, si un client exige un hébergement certifié (HDS, SecNumCloud : Scalingo en propose avec un surcoût d'environ 20 % relevé sur sa page), ou si les prix changent.
