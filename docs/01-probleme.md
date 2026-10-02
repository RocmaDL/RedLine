# Fiche problème

*Qui a le problème, concurrents, différence, modèle économique*

> **Nom du projet**
>
> **RedLine** (disponibilité du nom, marque et domaine, à vérifier avant tout usage commercial)

> **Équipe**
>
> 1 personne : Rocma

> **Statut**
>
> Brouillon de recherche au 1<sup>er</sup> octobre 2026. Les faits sont sourcés, les hypothèses signalées.

## 1. Le problème en une phrase

> Les écoles privées post-bac doivent placer leurs étudiants en alternance ou en stage, mais elles suivent cette recherche avec un tableur et une boîte mail, sans vision en temps réel de qui a trouvé une entreprise, alors que le marché se contracte.

## 2. Qui a le problème

| Acteur | Problème vécu | Paie ? |
|---|---|---|
| **École privée post-bac** (bachelors, MBA, écoles du numérique) | Elle doit placer sa promo. Elle ne voit pas en temps réel qui est sans piste, et réagit tard. | Oui `Hypothèse` licence annuelle |
| **Étudiant en recherche d'alternance ou de stage** | Mal accompagné, peu d'offres près de chez lui, candidatures éparpillées. | Non (gratuit) |
| **Entreprise partenaire de l'école** | Reçoit des candidatures de mauvaise qualité, publier est lourd. | Non en V1 `Hypothèse` |

### Ordre de grandeur

> **846 700**
>
> contrats d'apprentissage débutés en 2025 (−5 % sur un an), dont **497 916 dans le supérieur** (58,8 %), en baisse de 7,8 % (Dares, estimation du 27 février 2026).

> **−16,4 %**
>
> d'entrées dans le supérieur entre janvier et mai 2026 (Dares, données au 31 juillet 2026). Cause avancée : le barème d'aides à l'embauche en vigueur depuis le 8 mars 2026 (pour un master en petite entreprise, l'aide passerait de 6 000 € à 2 000 €).

> **3 465**
>
> CFA en 2024, nombre multiplié par 3 entre 2017 et 2023 (DEPP, via Filiz).

> [!WARNING]
> **À compléter**
>
> Le **nombre d'écoles privées post-bac** (la cible précise) n'a pas été trouvé. À chiffrer avec une source officielle (SIES / MESR) avant de parler de taille de marché.

### Pourquoi maintenant

La baisse des contrats dans le supérieur en 2026 augmente le nombre d'étudiants sans entreprise en début d'année : le problème des écoles s'aggrave. En contrepartie, leurs budgets sont sous pression, donc l'outil doit se rentabiliser vite.

## 3. Comment ils font aujourd'hui

- **Écoles** : un fichier Excel et une boîte mail, parfois Drive ou Notion (constat d'un éditeur concurrent, donc à vérifier en entretien). Pas de rappels automatiques, risque d'erreurs sur les documents, pas de vue globale, RGPD fragile.
- **ERP et CRM de CFA** : Ypareo (module de placement), Ymag, Digiforma, Gestibase/iCFA, MyScol. Ils couvrent la gestion, moins la recherche d'entreprise côté étudiant.
- **Étudiants** : Indeed, LinkedIn, JobTeaser, La Bonne Alternance, réseau personnel.
- **Difficulté ressentie** : les alternants notent la difficulté à trouver une entreprise à **6,8/10**. Causes citées : entreprises qui ne recrutent pas (32 %), offres insuffisantes (30 %), distance (26 %) (baromètre Igensia).
- **Côté entreprises** : candidats peu motivés (33 %), dossiers de mauvaise qualité (29 %), conflits de rythme (26 %) (même baromètre).
- **Côté étudiants** : un candidat sur deux n'est pas accompagné, 27 % trouvent compliqué de contacter les employeurs (AlternJob, cité par Welcome to the Jungle).

### Règles de l'apprenti sans entreprise (utile pour le domaine)

Un apprenti peut suivre sa formation sans employeur pendant **3 mois** (entrée en CFA sans entreprise) ou **6 mois** (après une rupture), avec le statut de stagiaire de la formation professionnelle et un CERFA P2S. Au-delà, le financement OPCO dépend d'un contrat signé dans le délai (Filiz). Ces délais fondent l'alerte d'échéance du [chapitre 02](02-domaine.md).

## 4. Concurrents (trois principaux)

| | Offre | Prix affiché | Point faible |
|---|---|---|---|
| **Grimp** | « CRM + job board » : suivi des candidatures, offres, CVthèque, correction de CV par IA, documents administratifs. 250+ établissements, 150 000+ candidats (selon l'éditeur). | Entreprises : gratuit, Basic, Pro. **Prix côté école non affiché.** | Avis Trustpilot (11 avis, 3,5/5) : offres concentrées à Paris, pièces jointes limitées au CV. Confidentialité côté école non vérifiée. |
| **Hub3E** | CRM/ATS pour CFA : candidats, matching IA, prospection d'entreprises, intégrations Yparéo, Charlemagne, Brevo, Galia. 200+ centres. | Non affiché | Mise en place « en quelques semaines » (selon l'éditeur). Prospection au niveau de l'entreprise, pas de l'offre ouverte (critique d'un concurrent). |
| **JobTeaser** | Job board et career centers, 800+ écoles et 2M+ étudiants (selon l'éditeur). | Recruteurs : packs dès 390 €, puis annuel sur devis. | Recruteurs : republication manuelle, tarifs élevés, peu de BTS/Licence, pas de multi-diffusion automatique (Capterra). |

**Autres acteurs repérés** : Go-Alternance (suivi des placements pour écoles), Bloom (suivi de l'intégration des apprentis), Pyramide (CRM/ATS pour CFA), Alternel (prospection d'entreprises).
**Alternatives génériques** : HubSpot (0 / 15 / 90 / 150 € par utilisateur et par mois), Salesforce Education Cloud (87 à 363 $ par utilisateur et par mois, tarif affiché pour le non-lucratif).

> [!TIP]
> **Limite de l'analyse**
>
> Le segment est occupé. Les avis directs sont rares (peu d'avis sur ces outils, Hub3E sans avis indépendant), et les pages Trustpilot de JobTeaser et goalternance.fr étaient inaccessibles : elles n'ont pas été devinées. **Les entretiens sont la vraie source.**

## 5. Notre différence `Hypothèse à valider`

> Pour les écoles privées post-bac : un suivi de promo en temps réel **qui respecte la vie privée des étudiants** (l'école voit un statut global, pas le détail), où l'école **recommande ses candidats à ses entreprises partenaires**, et qui s'installe sans projet d'intégration lourd.

Points d'appui, chacun à tester :

1. **Confidentialité par conception** (statut global côté école). C'est le point porté par l'architecture ([ADR-004](adr/0004-confidentialite.md)).
2. **Candidatures recommandées par l'école**, pour répondre au grief des entreprises sur la qualité des dossiers. *Hors V1 : voir périmètre.*
3. **Offres officielles géolocalisées** (La Bonne Alternance, France Travail), face au reproche de concentration parisienne.
4. **Mise en route rapide**, licence simple par promo.

> [!WARNING]
> **Risque principal**
>
> Aucune de ces différences n'est un fossé par elle-même. Les ERP de CFA ont déjà un module de placement, et Hub3E s'intègre à Ypareo : sans intégration aux ERP, l'adoption sera difficile. L'intégration est hors V1 et reste le risque commercial numéro un.

## 6. Modèle économique envisagé `Hypothèse`

- **Écoles** : licence annuelle, par promo ou par apprenant actif. Montant à fixer après entretiens.
- **Étudiants** : gratuit (ils apportent l'usage).
- **Entreprises** : gratuit en V1 (invitées par l'école). Option payante à étudier plus tard : multi-diffusion et mise en avant.

Repère de viabilité : le budget d'exploitation est plafonné à 100 € par mois ([chapitre 03](03-exigences.md)). Une seule licence d'école couvrant ce coût suffirait à être à l'équilibre sur l'hébergement. Ce n'est pas un modèle économique, seulement une borne basse qu'un entretien devra confirmer.

## 7. Périmètre de la première version

| Dans la V1 `V1` | Hors V1 `Plus tard` |
|---|---|
| Alternance **et** stages | Conventions et contrats (l'école garde son process) |
| Comptes étudiant, référent d'école, entreprise invitée | Facturation |
| Rattachement à une promo | Publication libre des offres par les entreprises |
| Offres via API officielles et entreprises invitées par l'école | Flux de job boards partenaires |
| Pipeline de candidatures, lettre de motivation par IA | Recommandation d'étudiants aux entreprises |
| Statut global, alertes et synthèse pour l'école | Intégration aux ERP de CFA |

**Piste ultérieure** : l'API La Bonne Alternance permet aux employeurs de déposer des offres rattachées à leur SIRET. On pourrait y diffuser les offres déposées sur la plateforme.

## 8. API officielles `Conditions à confirmer`

| API | Accès | Limites relevées | À vérifier |
|---|---|---|---|
| La Bonne Alternance | Gratuit, accès sur demande | 5 à 20 appels/s selon la route | Obligations d'attribution et d'affichage dans les CGU |
| France Travail, Offres d'emploi | Gratuit, inscription | 10 appels/s | Conditions d'affichage ; **couverture des stages non confirmée** |

Conséquence de périmètre : si les API ne couvrent pas les stages, les offres de stage viendront surtout des **entreprises invitées par l'école**. L'architecture s'en accommode (deux sources derrière un même port), mais le produit sera plus pauvre côté stages.

## 9. Hypothèse à vérifier d'ici la fin du trimestre

> Une école privée post-bac accepte de piloter une promo sur l'outil et décrit, sans qu'on le suggère, le suivi du placement comme un problème de visibilité.

**Critère de réussite (proposition)** : sur 5 écoles interrogées, au moins 3 décrivent le problème spontanément et 2 acceptent un pilote.

**Questions d'entretien (école)**

1. Comment suivez-vous aujourd'hui qui a trouvé une entreprise ?
2. Combien d'étudiants n'ont pas d'entreprise à date, et qu'est-ce que ça vous coûte ?
3. Quels outils utilisez-vous (ERP, offres, carrières) et qu'est-ce qui ne va pas ?
4. Qu'est-ce qui vous ferait payer un outil ? Quel budget, qui décide ?
5. Qu'accepteriez-vous (ou pas) que l'école voie de la recherche d'un étudiant ?

## 10. Sources

- [Dares, 846 700 contrats débutés en 2025 (News Tank)](https://education.newstank.fr/article/view/432982/apprentissage-846700-contrats-debutes-2025-5-an-7-8-superieur-dares.html)
- [Chute des contrats dans le supérieur, rentrée 2026 (Formation Professionnelle Mag)](https://formation-professionnelle-mag.fr/alternance-rentree-2026-chute-contrats-superieur/)
- [Rentrée 2026, la chasse au contrat (L'Apprenti)](https://www.lapprenti.com/articles/infos_apprentissage/3460)
- [France Compétences, apprentissage 2025](https://www.francecompetences.fr/app/uploads/2026/02/RUF25_Apprentissage.pdf)
- [Nombre de CFA et missions (Filiz)](https://www.filiz.io/blog/role-cfa-formation-alternance)
- [Apprenti sans contrat, CERFA P2S (Filiz)](https://www.filiz.io/blog/cerfa-p2s-apprenti-sans-contrat)
- [Baromètre Igensia, difficultés de placement (Cap Métiers)](https://pro.cap-metiers.fr/organismes-de-formation/pour-les-alternants-il-est-difficile-de-trouver-une-entreprise/)
- [Difficultés à trouver une alternance (Welcome to the Jungle)](https://www.welcometothejungle.com/fr/articles/apprentissage-contrat-difficile)
- [Gestion de l'alternance dans les écoles (Grimp, vendeur)](https://www.grimp.io/en/blog/plateforme-gestion-de-lalternance-le-guide-pour-les-etablissements-de-formation)
- [Placement en alternance (Ypareo)](https://www.ypareo.com/lexique/placement-alternance)
- [Grimp (EdtechActu)](https://edtechactu.com/plate-formes-lms/grimp-a-la-croisee-dun-crm-et-dun-jobboard/)
- [Grimp, abonnements recruteurs](https://www.grimp.io/en/recruteurs/abonnements)
- [Grimp sur Trustpilot](https://fr.trustpilot.com/review/grimp.io)
- [Hub3E](https://www.hub3e.com/)
- [Hub3E vs Alternel](https://alternel.com/alternel-vs-hub3e)
- [JobTeaser, packs recruteurs](https://www.jobteaser.com/en/corporate/our-packs)
- [JobTeaser, avis Capterra](https://www.capterra.com/p/246003/JobTeaser/reviews/)
- [Bloom, suivi d'intégration](https://bloom-alternance.fr/fonctionnalite/outil-de-suivi-dintegration-etudiant)
- [API La Bonne Alternance (data.gouv.fr)](https://www.data.gouv.fr/dataservices/api-la-bonne-alternance)
- [API Offres d'emploi France Travail (data.gouv.fr)](https://www.data.gouv.fr/dataservices/api-offres-demploi)
- [Salesforce Education, tarifs](https://www.salesforce.com/education/pricing/)
- [HubSpot, prix 2026 (StackIndep)](https://stackindep.fr/crm/hubspot-prix)
