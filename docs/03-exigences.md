# Exigences

*Fonctionnelles et non fonctionnelles chiffrées*

Ce chapitre fixe les exigences qui commandent l'architecture. Les exigences non fonctionnelles sont **chiffrées**, même quand le chiffre est une hypothèse : un chiffre faux mais écrit se corrige, une exigence floue ne se discute pas. Chaque ligne indique si le chiffre est un fait ou une hypothèse.

## 1. Hypothèses de dimensionnement à douze mois `Hypothèse`

> **5**
>
> écoles clientes (1 pilote puis 4)

> **1 500**
>
> étudiants inscrits, soit 300 par école en moyenne

> **150**
>
> entreprises partenaires actives, soit 30 par école

> **20**
>
> personnes côté écoles (référents, administrateurs)

**Contrôles de cohérence** (les calculs sont refaits, pas estimés à l'œil) :

| Grandeur | Calcul | Résultat |
|---|---|---|
| Pic d'utilisateurs simultanés | 1 500 étudiants × 7 % connectés en même temps pendant la rentrée | ≈ 100 |
| Pic de requêtes | 100 utilisateurs × 1 requête toutes les 5 s | ≈ 20 requêtes/s |
| Indisponibilité tolérée | (1 − 0,995) × 30 jours × 24 h | 3,6 h = **3 h 36** par mois |
| Volume de candidatures | 1 500 étudiants × 40 candidatures par an | ≈ 60 000 lignes par an |
| Volume d'offres | ≤ 50 000 offres actives, expirées conservées 90 jours | ≤ 150 000 lignes |
| Taille de la base | environ 150 000 offres × 3 Ko + 60 000 candidatures × 1 Ko, marge ×3 | < 2 Go |
| Coût LLM plafond | 15 € ÷ (1 500 étudiants × 3 lettres par mois) | ≈ 0,003 € par lettre à ne pas dépasser |

Les pics sont **saisonniers** : septembre à octobre (rentrée, recherche d'entreprise) et la fin de chaque semestre. Le reste de l'année la charge est faible. C'est un argument pour une instance unique et petite.

## 2. Exigences fonctionnelles principales

Vingt exigences, regroupées par contexte. Toutes sont dans la V1 `V1`.

| N° | Contexte | Exigence |
|---|---|---|
| EF-01 | OA | L'équipe crée une école ; l'administrateur de l'école crée des promotions (nom, rentrée, parcours alternance ou stage). |
| EF-02 | OA | L'administrateur invite des étudiants (import CSV ou e-mail) ; l'étudiant crée son compte par le lien d'invitation et est rattaché à sa promo. |
| EF-03 | OA | L'administrateur invite des référents et des entreprises partenaires. |
| EF-04 | OA | Connexion par e-mail et mot de passe, réinitialisation, trois rôles (étudiant, référent/administrateur, entreprise). Un utilisateur ne voit jamais les données d'une autre école. |
| EF-05 | OA | L'étudiant supprime son compte (droit à l'effacement) et exporte ses données. |
| EF-06 | PA | L'étudiant renseigne ses critères de recherche : domaine, commune, rayon, rythme d'alternance, rentrée visée. |
| EF-07 | PA | L'étudiant génère une lettre de motivation à partir de son profil et d'une offre, la modifie, l'enregistre. Quota de lettres par mois. |
| EF-08 | OF | Le système importe chaque nuit les offres de La Bonne Alternance et de France Travail, les géolocalise, supprime les doublons et marque les offres expirées. |
| EF-09 | OF | Une entreprise partenaire publie une offre (alternance ou stage) et la réserve à une ou plusieurs promos. |
| EF-10 | OF | L'étudiant recherche et filtre les offres (mots-clés, distance, type de contrat, source). Les offres réservées à sa promo passent en premier. |
| EF-11 | CA | L'étudiant enregistre une offre dans son pipeline, ou ajoute une piste manuelle (offre hors plateforme). |
| EF-12 | CA | L'étudiant fait avancer sa candidature dans les états du pipeline, avec notes et prochaine étape datée. |
| EF-13 | CA | L'étudiant reçoit un rappel par e-mail quand une relance prévue est dépassée. |
| EF-14 | CA | L'étudiant déclare un placement (entreprise, type de contrat, date de début) et peut déclarer une rupture. |
| EF-15 | SP | Le référent consulte la liste de sa promo avec **le statut global seulement**, la filtre et l'exporte en CSV. |
| EF-16 | SP | Le référent confirme ou conteste un placement déclaré. |
| EF-17 | SP | Le système lève des alertes à partir de règles : étudiant sans piste depuis N jours, échéance de 3 ou 6 mois approchant. |
| EF-18 | SP | Le système produit chaque semaine une synthèse de promo : chiffres agrégés et résumé rédigé par l'assistant IA, **sans donnée nominative envoyée au LLM**. |
| EF-19 | NO | Le système envoie les e-mails transactionnels (invitation, rappel, alerte, confirmation, synthèse). |
| EF-20 | OA/SP | Le journal d'audit enregistre qui a confirmé ou contesté un placement et quand. |

> [!IMPORTANT]
> **Précision honnête sur « l'IA »**
>
> Dans cette liste, l'IA ne sert qu'à **deux choses** : rédiger un brouillon de lettre (EF-07) et rédiger le résumé en langage naturel d'une synthèse (EF-18). Les **alertes (EF-17) sont des règles déterministes**, pas de l'IA. Annoncer « alertes par IA » serait faux et ne résisterait pas à la question d'un responsable sécurité.

## 3. Exigences non fonctionnelles chiffrées

| N° | Catégorie | Exigence | Vérification | Nature |
|---|---|---|---|---|
| ENF-01 | Capacité | 5 écoles, 1 500 étudiants, 150 entreprises, 20 personnels d'école à 12 mois | revue trimestrielle | `Hypothèse` |
| ENF-02 | Charge | Pic de **100 utilisateurs simultanés, 20 requêtes/s** pendant la rentrée | test de charge (module 3) | `Hypothèse` |
| ENF-03 | Performance | p95 des lectures < **500 ms**, p95 des écritures < 800 ms ; affichage d'une page < 2,5 s sur 4G | test de charge, Lighthouse | `Hypothèse` |
| ENF-04 | Traitements différés | Génération d'une lettre en asynchrone, p95 < 30 s ; import nocturne des offres < 15 min | métriques de durée | `Hypothèse` |
| ENF-05 | Disponibilité | **99,5 % par mois** (3 h 36 d'arrêt), hors maintenance annoncée | sonde d'uptime | `Hypothèse` |
| ENF-06 | Reprise | **RPO 24 h** (sauvegarde quotidienne), **RTO 4 h** | exercice de restauration trimestriel | `Hypothèse` |
| ENF-07 | Données sensibles | Données personnelles d'étudiants : identité, e-mail, commune, parcours, historique de candidatures. Pas de donnée de catégorie particulière (RGPD art. 9). Possibles mineurs (17 ans) : information adaptée. **Aucun CV ni pièce jointe stockés en V1.** | registre des traitements | `Hypothèse` |
| ENF-08 | Confidentialité | L'école ne reçoit **que** le statut global : aucune route ne renvoie une candidature à un rôle école. | test d'autorisation automatisé par rôle | `Décision` ADR-004 |
| ENF-09 | Hébergement | Données hébergées dans l'Union européenne ; contrat de sous-traitance (DPA) avec l'hébergeur, le service d'e-mail et le fournisseur LLM | checklist avant signature | `À confirmer` |
| ENF-10 | LLM | **Aucune donnée d'identité** (nom, e-mail, adresse, école) dans les requêtes au LLM ; quota **10 lettres par étudiant et par mois** ; coût plafonné à 15 €/mois, alerte à 80 % | test sur le type du port, métrique de coût | `Décision` |
| ENF-11 | Sécurité | Mots de passe hachés, session par cookie `HttpOnly` et `SameSite`, protection CSRF, isolation par école, référentiel OWASP ASVS niveau 1, dépendances surveillées | tests de sécurité, Dependabot | `Décision` |
| ENF-12 | Rétention | Suppression de compte : effacement sous 30 jours. Comptes inactifs : anonymisation après 24 mois. Journaux sans donnée personnelle, conservés 30 jours | job d'effacement, revue | `Hypothèse` |
| ENF-13 | Accessibilité | WCAG 2.1 niveau AA visé sur les parcours étudiant et référent | audit axe, revue manuelle | `Hypothèse` |
| ENF-14 | Budget | **≤ 100 € par mois HT**, tout compris (hébergement, e-mail, LLM, domaine) ; prévision 72 € | facture mensuelle | `Plafond` voir §4 |
| ENF-15 | Équipe | **1 développeur, environ 8 h par semaine** → un seul déployable, aucun orchestrateur, déploiement automatique depuis `main`, aucune astreinte | — | `Hypothèse` |
| ENF-16 | Maintenabilité | Règles de dépendance vérifiées à chaque build ; couverture des lignes du domaine et de l'application ≥ **80 %** ; pipeline complet < 10 min | ArchUnit, JaCoCo, CI | `Décision` |
| ENF-17 | Observabilité | Journaux JSON avec identifiant de requête ; sonde de santé ; alerte par e-mail si plus de 5 % d'erreurs 5xx sur 5 min | PaaS, sonde externe | `Hypothèse` |
| ENF-18 | Compatibilité | Deux dernières versions de Chrome, Firefox, Safari et Edge ; interface adaptée au mobile, pas d'application native | tests Playwright | `Hypothèse` |
| ENF-19 | API externes | Import limité à 2 requêtes/s, sous les limites relevées (La Bonne Alternance 5 à 20/s, France Travail 10/s), avec reprise exponentielle | test d'adaptateur | `Fait` limites relevées |

## 4. Budget mensuel `Hypothèse`

Les trois premières lignes sont les **prix relevés le 1<sup>er</sup> octobre 2026** sur la page tarifaire de Scalingo (HT, région standard). Les autres sont des estimations à confirmer.

| Poste | Choix | € HT par mois | Source |
|---|---|---|---|
| API backend | conteneur L, 1 Go de mémoire | 28,80 | page tarifs Scalingo |
| Application web | conteneur M, 512 Mo | 14,40 | page tarifs Scalingo |
| Base de données | PostgreSQL Starter, 512 Mo, 10 Go | 7,20 | page tarifs Scalingo, palier supérieur à confirmer |
| **Sous-total relevé** | | **50,40** | |
| Fournisseur LLM | lettres et synthèses, plafond | 15,00 | estimation, voir §1 |
| E-mail transactionnel | palier gratuit ou entrée de gamme | 5,00 | estimation |
| Nom de domaine et DNS | | 2,00 | estimation |
| **Prévision** | | **72,40** | |
| Marge sous le plafond | | 27,60 | |
| **Plafond** | | **100,00** | exigence ENF-14 |

> [!NOTE]
> **Ce que ce budget n'inclut pas**
>
> Pas d'environnement de préproduction payant (développement local avec Docker, tests avec Testcontainers, déploiement direct depuis `main` après CI verte). Pas d'outil d'observabilité payant. Pas de TVA ni de temps de travail. Le palier de base de données au-dessus de « Starter » n'a pas été relevé : si la base dépasse 10 Go ou 512 Mo de mémoire, le budget est à recalculer.

## 5. Ce que nous ne ferons pas dans la première version

| Hors V1 | Raison |
|---|---|
| Conventions et contrats d'apprentissage | L'école garde son process ; périmètre juridique lourd |
| Facturation et paiement en ligne | La licence se facture hors plateforme au démarrage |
| Publication libre des offres par les entreprises | Les entreprises sont invitées : la qualité reste maîtrisée |
| Flux de job boards partenaires | Le port `OffreSource` les accueillera plus tard |
| Recommandation d'étudiants aux entreprises | Demande un consentement par étudiant, à concevoir |
| Intégration aux ERP de CFA | Risque commercial n°1 ; à traiter après les entretiens |
| Application mobile native | Interface web adaptée au mobile suffit |
| **Scraping** | Jamais : voir ADR-005 |
| Stockage de CV et de pièces jointes | Réduit la surface RGPD (ENF-07) |
| Authentification unique (SSO) d'école | À étudier avec un ADR si un client l'exige |
