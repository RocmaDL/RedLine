# Journal d'usage de l'IA

*Demandes importantes, décisions acceptées, modifiées ou refusées*

Ce journal applique la règle 5 de l'énoncé : « l'IA est une collègue, pas un auteur ». Le journal garde les demandes **importantes**, ce qui a été **accepté**, **modifié** ou **refusé**, et **pourquoi**.

> [!WARNING]
> **À relire avant dépôt**
>
> Ce journal a été **reconstitué par l'IA à partir de la conversation de travail** du 1<sup>er</sup> octobre 2026. Il est exact sur ce qui a été demandé et proposé. Les colonnes « Décision » et « Pourquoi » reprennent ce que vous avez dit pendant la conversation ; **corrigez-les si elles ne reflètent pas votre raisonnement**. C'est aussi la preuve de « l'esprit critique face aux propositions de l'IA » de la grille : un journal où tout est « accepté » ne la démontre pas.

## Journal des demandes importantes

| N° | Date | Demande | Ce que l'IA a produit | Décision | Pourquoi |
|---|---|---|---|---|---|
| 1 | 1<sup>er</sup> oct. | Résumer le cours et la consigne (deux PDF joints) | Récapitulatif du cours et de ce qu'il fallait rendre | `Accepté` | Sert de base ; **l'énoncé original reste la référence** (la grille a été relue dans le PDF d'origine pour ce dossier) |
| 2 | 1<sup>er</sup> oct. | Différence entre SaaS et application mobile | Explication | Information | Pas de décision |
| 3 | 1<sup>er</sup> oct. | Chercher dans mes dépôts un projet qui pourrait devenir un SaaS | Analyse de 12 dépôts ; classement avec **StageFlow en premier choix** | `Refusé` | J'ai jugé **jobscraper** plus prometteur |
| 4 | 1<sup>er</sup> oct. | Analyser jobscraper ; clients = étudiants et écoles ; plus de scraping ; entreprises qui postent ; partenariats job boards plus tard | Constats sur le dépôt (API FastAPI, modules de scraping d'environ 2 370 lignes, schéma de données dupliqué entre back et front, un seul test, fichier `.env` suivi par Git) ; proposition de pivot vers un produit centré sur l'école | `Accepté` | Le pivot correspond à mon besoin. **Constat de sécurité à traiter** dans l'ancien dépôt : `.env` suivi par Git, à purger de l'historique s'il contient des secrets |
| 5 | 1<sup>er</sup> oct. | Poser des questions pour affiner le produit | Questions à choix : payeur, cible, source des offres, périmètre, vue de l'école, conventions, IA. L'IA a **recommandé de limiter à l'alternance** | `Refusé` sur le périmètre | J'ai choisi **alternance et stages**. Conséquence assumée : les stages dépendront des entreprises invitées (couverture des API non confirmée) |
| 6 | 1<sup>er</sup> oct. | Comparer ma solution à Grimp, JobTeaser, HubSpot, Salesforce, Hub3E | Tableau comparatif. **Grimp est apparu très proche de mon idée** | `Accepté` avec réserves | Une page de l'App Store nommée « Grimp » était une application d'escalade : **écartée**. Les pages Trustpilot de JobTeaser et goalternance.fr étaient inaccessibles : **non devinées**. Prix côté école de Grimp et Hub3E : introuvables |
| 7 | 1<sup>er</sup> oct. | Chercher des avis d'utilisateurs pour repérer des frustrations | Peu d'avis directs ; frustrations déduites de baromètres et de retours éditeurs | `Accepté` | La limite est écrite dans la fiche : **les entretiens d'école restent la vraie source** |
| 8 | 1<sup>er</sup> oct. | Recherche de marché et de R&D | Fiche problème ([chapitre 01](01-probleme.md)), environ 21 sources | `Modifié` à faire | Les chiffres Dares viennent de **presse spécialisée**, pas du document primaire : à rouvrir avant de les citer à l'oral. Le nombre d'écoles privées post-bac **n'a pas été trouvé** |
| 9 | 1<sup>er</sup> oct. | Un PDF unique avec tous les livrables, design moderne ; équipe de 1, Java Spring Boot + Next.js + PostgreSQL, PaaS européen < 100 €/mois | Ce dossier. **Décisions prises par l'IA, à valider** : voir ci-dessous | `À relire` | Je dois relire chaque décision avant de la défendre |
| 10 | 1<sup>er</sup> oct. | (Dans le cadre du n° 9) Vérifier le code du squelette | Squelette compilé avec `javac`, dix tests exécutés avec des substituts de JUnit et d'AssertJ ; ArchUnit **non exécuté** (dépôt Maven inaccessible) | `Accepté` partiellement | À refaire avec les vraies bibliothèques en phase 4 |

### Décisions prises par l'IA dans le dossier, à valider par l'auteur

Ces points n'ont pas été demandés explicitement. L'IA les a tranchés pour avancer et les a marqués comme hypothèses ou décisions proposées.

| Décision | Où | Statut |
|---|---|---|
| Nom de travail « Passerelle » | Couverture, tout le dossier | À changer librement ; disponibilité non vérifiée |
| L'étudiant **déclare** un placement, le référent le **confirme** | [Chapitre 02](02-domaine.md) §4, EF-16 | Hypothèse jamais testée avec une école ou un étudiant |
| Six bounded contexts et leur classement (cœur, support, générique) | [Chapitre 02](02-domaine.md) | Proposition ; défendable à la revue |
| Scalingo en premier choix, Clever Cloud non comparé faute de prix lisibles | ADR-002 | Prix Scalingo relevés sur sa page ; lieu du centre de données à confirmer |
| Fournisseur LLM non choisi (Mistral cité comme candidat) | ADR-002 | À choisir ; DPA obligatoire |
| Seuils chiffrés (5 écoles, 100 simultanés, 99,5 %, 80 % de couverture) | [Chapitre 03](03-exigences.md) | Hypothèses de dimensionnement |
| ADR-004 (confidentialité) et ADR-005 (aucun scraping) ajoutés | [Chapitre 04](adr/README.md) | Ajouts ; la décision d'ADR-005 est la vôtre |
| Alertes par règles déterministes, pas par IA | EF-17 | Précision de l'IA, plus honnête que « alertes par IA » |

## Bilan provisoire

- **Accepté** : 1, 4, 6 (avec réserves), 7, 10 (en partie). **Refusé** : 3 et 5 (sur le périmètre). **À relire** : 8 et 9.
- **Ce que l'IA a mal fait ou risque de mal faire** : confondre des homonymes (la page App Store « Grimp »), citer des sources secondaires comme primaires, annoncer comme acquis ce qu'elle n'a pas pu exécuter. Les garde-fous correspondants sont dans la charte ([chapitre 06](06-charte.md) §8).
- **Ce que je retiens de l'usage de l'IA** : *à compléter par l'auteur, en une ou deux phrases personnelles.*

## Règles de tenue du journal

1. Ajouter une ligne pour toute demande qui change une décision, un document ou du code.
2. Dire si c'est accepté, modifié ou refusé, et pourquoi, en une phrase.
3. Ne jamais effacer une ligne : si un avis change, ajouter une ligne qui le dit.
4. Ne pas y coller de donnée personnelle ni de secret.
