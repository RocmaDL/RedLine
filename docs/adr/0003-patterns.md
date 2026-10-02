# ADR-003 · Patterns retenus et patterns interdits

| | |
|---|---|
| **Statut** | Proposée |
| **Date** | 1<sup>er</sup> octobre 2026 |
| **Exigences liées** | ENF-08, ENF-10, ENF-16, ENF-19 |

## Patterns retenus : où et pourquoi

| Pattern | Où | Pourquoi | Comment on le vérifie |
|---|---|---|---|
| **Ports et adaptateurs** (hexagonal) | Chaque module | Les API externes, le LLM et l'e-mail changent ; le domaine ne doit pas le savoir | ArchUnit : le domaine ne dépend d'aucun framework (R-01 à R-04) |
| **Agrégat et objets-valeurs** | `Candidature`, `Offre`, `SuiviEtudiant` | Les invariants (une seule candidature par offre, transitions autorisées) vivent dans le domaine | Tests unitaires sans infrastructure |
| **Cas d'usage** (une classe, une action) | `application` : `ImporterOffres`, `DeclarerPlacement`… | Une action métier = un fichier lisible et testable | Revue ; nom en verbe à l'infinitif |
| **Repository** (port) | `OffreRepository`, `CandidatureRepository`… | Le domaine demande un agrégat, il ignore la base | Test de contrat commun à tous les adaptateurs |
| **Couche anti-corruption** | `offres.infrastructure.source` | Les DTO de La Bonne Alternance et de France Travail ne doivent pas contaminer le modèle | Les DTO externes sont `package-private` dans l'adaptateur |
| **Événements de domaine en mémoire**, après commit | Entre modules | Découple les contextes sans broker ; Suivi de promo n'accède jamais aux candidatures | ArchUnit : aucun accès direct entre modules (R-05) |
| **Modèle de lecture** (CQRS léger) | `suivi.statut_global` | Les tableaux de bord lisent une table dédiée, reconstructible à partir des événements | Test de reconstruction |
| **Idempotence** | Import d'offres | Relancer un import ne crée pas de doublon : clé `(source, identifiant_externe)` | Test d'application avec adaptateurs en mémoire |
| **Résilience** (délai, reprise, disjoncteur) | Tous les adaptateurs sortants | Une API tierce lente ne doit pas bloquer l'application | Tests avec WireMock |
| **Erreurs normalisées** (RFC 9457) | Couche web | Un format d'erreur unique, stable et sans fuite d'information | Test sur chaque code de problème |

## Patterns interdits

| Interdit | Pourquoi | Garde-fou |
|---|---|---|
| Microservices, broker de messages, event sourcing | Disproportionnés (ADR-001) | Revue ; tout ajout de dépendance justifié (R-17) |
| Entité JPA ou objet de domaine renvoyé par l'API REST | Fuite de modèle ; risque de montrer à l'école ce qu'elle ne doit pas voir | ArchUnit R-09 : les contrôleurs ne renvoient que des `*Response` |
| Relation JPA ou jointure SQL entre deux schémas | Casse l'isolement des contextes | Test des migrations (R-11) |
| Logique métier dans un contrôleur, un trigger ou une procédure stockée | Intestable sans infrastructure | Revue ; tests de domaine |
| Classes « Base » génériques (`BaseService`, `BaseRepository<T>`) | Abstraction prématurée qui masque le langage du métier | Revue ; consigne à l'IA |
| Injection par champ (`@Autowired` sur un attribut), singletons statiques | Dépendances cachées, tests fragiles | ArchUnit R-08 |
| Appel HTTP ou appel LLM hors d'un adaptateur | Impossible à tester sans réseau, et risque de fuite de données | ArchUnit R-12 |
| Donnée personnelle dans un prompt ou dans les logs | RGPD (ENF-10) | Le type du port `AssistantRedaction` ne permet pas de la passer (R-13) |
| Cache distribué (Redis), GraphQL, file de messages dès la V1 | Ajout d'un service ou d'une complexité sans besoin mesuré | Revue ; réexamen si une mesure l'exige |

## Conséquences

Un peu plus de classes qu'un CRUD classique (objets de domaine distincts des entités JPA, mappeurs). C'est le prix de la testabilité et des frontières. Il est assumé, et borné par l'interdit des abstractions génériques.
