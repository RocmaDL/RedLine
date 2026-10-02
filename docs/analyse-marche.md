# Analyse de marché

> **RedLine attaque un marché étroit et concentré**
>
> Notes de recherche arrêtées au 2 octobre 2026. Complète la [fiche problème](01-probleme.md). Rapport produit avec l'aide de l'IA à partir de sources web : plusieurs sont des pages d'éditeurs ou de la presse secondaire, et aucune hypothèse n'a été testée auprès d'une école (voir le [journal IA](journal-ia.md), n° 11).

**Réponse courte : le marché existe, il est solvable sur le papier, mais il est petit.** Le calcul bottom-up donne un TAM central d'environ **6,3 M€ par an**, un SAM central de **3,2 M€** et un SOM à trois ans de **181 k€** (fourchette 23 k€ à 486 k€ selon les scénarios). Ces chiffres reposent sur des effectifs officiels solides mais sur des hypothèses de prix, de conversion et de poids des groupes qui n'ont jamais été testées auprès d'une école. La demande est réelle : 67 % des étudiants du supérieur jugent difficile de trouver une entreprise d'accueil ([L'Étudiant, enquête Apec](https://www.letudiant.fr/etudes/alternance/alternance-deux-etudiants-sur-trois-ont-des-difficultes-a-trouver-un-contrat-dapprentissage.html)), et les entrées en apprentissage dans le supérieur reculent de 14,1 % de janvier à juillet 2026 ([Dares POEM](https://poem.travail-emploi.gouv.fr/donnee/contrat-dapprentissage-enseignement-superieur-entrees)). Le positionnement « l'école ne voit qu'un statut global » n'apparaît chez aucun concurrent dans les sources publiques. Mais personne n'a prouvé que l'acheteur le veut : l'école doit justifier son accompagnement (Qualiopi) et les concurrents vont plutôt vers plus de visibilité individuelle. Le risque juridique le plus dur est contractuel : les CGU de l'API La Bonne Alternance interdisent de « commercialiser les données reçues » ([CGU API](https://api.apprentissage.beta.gouv.fr/fr/cgu)). La confidentialité par étudiant est donc un pari de différenciation, à valider par cinq entretiens avant d'investir (section 6).

*Lecture des étiquettes. « Fait sourcé » : chiffre lu dans la source citée. « Hypothèse » : choix ou calcul à moi, sans source directe. Les sources secondaires (presse, éditeurs) sont signalées. Notes de recherche arrêtées au 2 octobre 2026 ; les chiffres de la rentrée 2026 ne sont pas publiés.*

## 1. Le TAM central vaut 6,3 M€, mais le SOM plafonne sous 0,5 M€

### Les volumes sont solides, les prix ne le sont pas

Le privé scolarise **786 900 étudiants en 2025-2026** (25,8 % du total), en baisse de 1,7 % : première baisse depuis 2014 ([SIES, juillet 2026](https://www.enseignementsup-recherche.gouv.fr/sites/default/files/2026-07/NF_synth%C3%A8se_effectifs_etudiants_2025-26.pdf)). Fin 2024, **505 000 apprentis** étaient dans le privé ([SIES NF n°21](https://www.enseignementsup-recherche.gouv.fr/sites/default/files/2025-09/nf-sies-2025-21-37938.pdf)). Le privé lucratif pèse au moins 226 000 étudiants selon le SIES, chiffre jugé « largement sous-estimé » par les rapporteures ; les estimations montent à 400 000 - 450 000 ([Rapport AN n°2458](https://www.assemblee-nationale.fr/dyn/16/rapports/cion-cedu/l16b2458_rapport-information.pdf)). La mission IGAS/IGESR de juillet 2026 reprend environ 400 000 ([IGAS/IGESR](https://igas.gouv.fr/sites/igas/files/2026-07/Rapport%20IGAS-IGESR_Contr%C3%B4le%20Enseignement%20priv%C3%A9%20lucratif.pdf)).

Le nombre d'acheteurs est le point faible. Les groupes centralisent : chez Galileo, les contrats d'apprentissage, le recrutement des étudiants et les programmes sont centralisés, et les écoles ont « un degré limité d'autonomie » (même rapport IGAS, §37). Un seul CFA du groupe accueille 80 % de ses apprentis. Les huit plus gros groupes déclarent ensemble environ 240 000 étudiants (calcul à moi, fragile : France et international, dates 2022-2025 mélangées).

### Hypothèses du modèle

| # | Paramètre | Prudent / Central / Optimiste | Statut | Base |
|---|---|---|---|---|
| A1 | Étudiants du privé | 786 900 (fixe) | **Fait sourcé** | SIES 2026, lien ci-dessus |
| A2 | Étudiants du privé lucratif (le noyau visé) | 226 000 / 400 000 / 450 000 | **Fait sourcé** pour les trois valeurs (SIES plancher, IGAS, haute estimation) ; le choix du scénario est une **Hypothèse** | Rapport AN, IGAS |
| A3 | Part de ce noyau détenue par des groupes qui achètent au niveau du groupe | 60 % (fixe) | **Hypothèse** | 240 000 déclarés / 400 000 ; calcul fragile |
| A4 | Nombre de groupes acheteurs | 8 / 9 / 10 | **Hypothèse** | 6 à 8 grands groupes cités en 2024 (Rapport AN) ; aucun décompte officiel |
| A5 | Taille moyenne d'une école indépendante | 400 étudiants (fixe) | **Hypothèse** | Écoles contrôlées de 352 à 2 307 étudiants (IGAS, annexe 1) ; moyenne de groupe de 400 à 800 = inférence |
| A6 | Prix par étudiant et par an, HT | 5 € / 8 € / 12 € | **Hypothèse** | Repères en section 2 ; aucun prix public de concurrent « placement » |
| A7 | Écoles indépendantes gagnées à 3 ans (part des acheteurs de A5) | 5 % / 10 % / 15 % | **Hypothèse** | Grimp : 65 écoles en octobre 2023, deux ans après son lancement ([Pôle Sociétés](https://polesocietes.com/actualites/levee-de-fonds/edtech-grimp-leve-1-million-d-euros-pour-faciliter-l-acces-a-l-emploi-en-france)) |
| A8 | Groupes gagnés à 3 ans | 0 / 1 / 2 | **Hypothèse** | Cycles longs, outils internes probables |
| A9 | Part des étudiants d'un groupe gagné déployée à 3 ans | 25 % (fixe) | **Hypothèse** | Pilote puis extension |

### Calculs, à refaire ligne par ligne

| Étape | Formule | Prudent | Central | Optimiste |
|---|---|---|---|---|
| **TAM** (€/an) | A1 × A6 | 786 900 × 5 = **3 934 500** | 786 900 × 8 = **6 295 200** | 786 900 × 12 = **9 442 800** |
| **SAM** (€/an) | A2 × A6 | 226 000 × 5 = **1 130 000** | 400 000 × 8 = **3 200 000** | 450 000 × 12 = **5 400 000** |
| Étudiants dans les écoles indépendantes | A2 × (1 − A3) | 90 400 | 160 000 | 180 000 |
| Acheteurs indépendants réels | ÷ A5 | 226 | 400 | 450 |
| Écoles indépendantes gagnées | × A7 | 11,3 | 40 | 67,5 |
| Étudiants correspondants | × A5 | 4 520 | 16 000 | 27 000 |
| Étudiants moyens par groupe | A2 × A3 ÷ A4 | 135 600 / 8 = 16 950 | 240 000 / 9 = 26 667 | 270 000 / 10 = 27 000 |
| Étudiants via groupes gagnés | A8 × ligne précédente × A9 | 0 | 1 × 26 667 × 0,25 = 6 667 | 2 × 27 000 × 0,25 = 13 500 |
| Étudiants servis (total) | somme | 4 520 | 22 667 | 40 500 |
| **SOM** (€/an, an 3) | étudiants × A6 | 4 520 × 5 = **22 600** | 22 667 × 8 = **181 333** | 40 500 × 12 = **486 000** |
| SOM / SAM | | 2,0 % | 5,7 % | 9,0 % |
| SOM / TAM | | 0,6 % | 2,9 % | 5,1 % |

Trois lectures. D'abord, le SAM central compte **400 acheteurs indépendants** contre 2 278 établissements privés hors lycées recensés en 2022 ([Rapport AN](https://www.assemblee-nationale.fr/dyn/16/rapports/cion-cedu/l16b2458_rapport-information.pdf)) : le modèle cible le noyau lucratif structuré, pas tout le privé. Ensuite, le revenu annuel par école (A5 × A6 : 2 000 / 3 200 / 4 800 €) tombe dans la zone de la grille Filiz, qui va de 2 340 € à 22 800 € par an ([Filiz](https://www.filiz.io/tarifs-filiz)). Enfin, le scénario optimiste (68 écoles) suit la trajectoire de Grimp, qui a levé 1 M€ et employait 10 personnes ; il suppose donc un financement comparable. **Le SOM central ne finance pas une équipe**. Il finance un projet en bootstrap ou un produit d'appoint.

Deux sensibilités. Si seuls les apprentis comptaient, le TAM central tomberait à 505 000 × 8 = **4 040 000 €** ; je n'ai trouvé aucun chiffre national de stagiaires, donc l'extension aux stages repose sur l'Hypothèse que les écoles paient aussi pour eux. Si le prix central passait à 5 € ou 12 €, le SOM central serait de 113 k€ ou 272 k€.

## 2. Aucun concurrent ne vend la confidentialité par étudiant, mais la preuve est mince

### Carte des concurrents directs

Les offres se vendent d'abord aux écoles ; les étudiants sont utilisateurs gratuits. Les pages marketing ne décrivent pas les réglages de visibilité : une fonction peut exister sans être documentée. CGU, aides en ligne et démos n'ont pas été lues.

| Acteur | Offre côté école | Prix public | Traction déclarée (éditeur) | Visibilité école sur l'étudiant |
|---|---|---|---|---|
| **Go-Alternance** | Suivi des placements : kanban de candidatures, relances automatiques après 7 jours, un référent par étudiant ([goalternance.fr](https://goalternance.fr/)) | Non trouvé | Non trouvée ; éditeur non confirmé | Activité et engagement **par étudiant** |
| **Grimp** (Vannes) | CRM + job board ; repère les étudiants en difficulté ; IA de correction de CV ; roadmap « détection d'étudiants en difficulté » ([EdtechActu](https://edtechactu.com/plate-formes-lms/grimp-a-la-croisee-dun-crm-et-dun-jobboard/)) | Aucun tarif ; licences illimitées ([grimp.io](https://www.grimp.io/carriere/abonnement)) | 65+ écoles en 2023 ; 150+, 200+, 250+ ou 500+ selon la page | Activité **par étudiant**, accès des entreprises aux CV sous contrôle de l'école |
| **Hub3E** (Link Part, Lyon) | ATS pour CFA : candidatures, matching, relance groupée ([hub3e.com](https://www.hub3e.com/)) ; cédé en sept. 2025 | Aucun | 200+ puis 250+ centres ([C Birds](https://www.cbirds.fr/blog/c-birds-2/c-birds-accompagne-la-cession-de-linkpart-editeur-du-logiciel-hub-3e-4)) | RGPD et sécurité seulement ; pas de suivi post-placement vu |
| **Bloom** (Paris) | Admission, placement, **suivi d'intégration** (onboarding, période d'essai, off-boarding) ([Bloom](https://bloom-alternance.fr/fonctionnalite/outil-de-suivi-dintegration-etudiant)) | Sur devis | 75 000+ candidats ; levée de 400 k€ en 2022 | Satisfaction partagée et alertes vers l'école ; niveaux de confidentialité non précisés |
| **Filiz** | ERP de CFA : contrats, CERFA, OPCO, conventions de stage (+15 €/dossier) | **195 à 1 900 €/mois** selon 50 à 1 000 dossiers ([grille](https://www.filiz.io/tarifs-filiz)) | 700+ centres | Non décrit |
| **Linkpick** | Contrats, sourcing, suivi pédagogique, OPCO ([linkpick.fr](https://linkpick.fr/ecole)) | « Gratuit et premium », montants non trouvés | 250 écoles/CFA | Non décrit |
| **Pyramide** | « CRM ATS du candidat au contrat » | Non trouvé | Non trouvée | Site inaccessible (robots.txt) : **non lu** |

### Substituts

| Substitut | Ce qu'il couvre | Prix public | Limite pour le placement |
|---|---|---|---|
| ERP de CFA (Ypareo, Ymag) | Contrats, OPCO, émargement | Ypareo Neo dès 6 € HT/mois par apprenti + 1 404 € de mise en place ([Ypareo](https://www.ypareo.com/tarifs-ypareo-suite)) | Aucune fonction de recherche d'entreprise ni de placement vue |
| Digiforma, Edusign, Hyperplanning | Gestion, émargement, planning | 49-839 €/mois ([Digiforma](https://www.digiforma.com/prix/)) ; 29-99 €/mois ([Edusign](https://edusign.com/fr/tarifs)) ; 1 677-5 017 €/an de licence ([Index Education](https://www.index-education.com/contenu/telechargement/hp/v2024.0/pdf/Tarifs-HYPERPLANNING-FR-2024.pdf)) | Compléments plutôt que substituts |
| Job boards | Diffusion d'offres | La Bonne Alternance et France Travail gratuits ; HelloWork 99-299 €/mois ([HelloWork](https://recruteur.hellowork.com/tarifs)) | Diffusion non monétisable ; pas de tableau de bord de placement |
| JobTeaser, Handshake | Career center | JobTeaser sur devis ; Handshake ≈ 8 000 $/école/an (agrégateur, estimation : [Sacra](https://sacra.com/c/handshake/)) | Pas de suivi d'intégration spécifique à l'alternance |
| Tableurs, e-mail, Notion | « Système » par défaut | Gratuit | Seule source : un blog de Grimp (concurrent, 9 mars 2026) ; aucune étude indépendante d'usage |
| Trackers étudiants (Huntr, Simplify) | Suivi de candidatures | Gratuit jusqu'à 100 offres chez Huntr ; Simplify illimité gratuit ([TrackJobs](https://trackjobs.co/blog/huntr-vs-simplify)) | Anglophones, sans lien avec l'école |

### Déclarations d'éditeurs contre avis indépendants

Presque tout ce qui précède est déclaratif. Les avis indépendants sont rares. Grimp : **3,5/5 sur 11 avis Trustpilot**, certains passés par l'école, plainte récurrente sur le manque d'offres dans certaines zones ([Trustpilot](https://fr.trustpilot.com/review/grimp.io)). JobTeaser : 3,7/5 sur 908 avis, plaintes sur la qualité des offres ([Trustpilot](https://www.trustpilot.com/review/www.jobteaser.com)) ; 4,5/5 sur 18 avis côté entreprises ([Capterra](https://www.capterra.com/p/246003/JobTeaser/)). Bloom : 4/5 sur 4 avis évalués sur une page non officielle ([GoWork](https://gowork.fr/bloom-alternance-paris)). **Aucun avis de CFA ou d'école** n'a été trouvé pour Hub3E, Filiz, Linkpick, Go-Alternance ou Pyramide. Les critiques entre concurrents (Alternel contre Hub3E) sont à lire comme du marketing.

### La place laissée à la confidentialité

Dans les sources lues, l'école voit l'activité par étudiant chez Go-Alternance et Grimp, et des alertes partagées chez Bloom. Aucun acteur ne revendique un « statut global seulement ». C'est un espace libre. C'est aussi un signal ambigu : soit personne n'a vu l'opportunité, soit les acheteurs ne la demandent pas. Deux faits penchent vers la seconde lecture. Grimp annonce vouloir détecter les étudiants en difficulté, soit l'inverse de la confidentialité. Et l'école doit prouver son accompagnement à la recherche d'employeur et le traitement des ruptures (section 4). **L'offre doit donc donner à l'école une preuve d'accompagnement sans lui donner le contenu de la recherche.** Aucune source ne dit si cela suffit.

## 3. La demande est forte, les payeurs sont fragilisés

### Le besoin se durcit

Les signaux convergent. Les offres d'alternance baissent de 9,5 % à 12 % en 2025 selon deux lectures du baromètre Hellowork ([Diplomeo](https://diplomeo.com/actualite-alternance_declin_2025), [Campus Matin](https://www.campusmatin.com/vie-campus/strategies/recul-des-offres-en-alternance-quelles-consequences-pour-les-etablissements.html)). Au premier semestre 2026, JobTeaser mesure **15 % de candidatures en plus pour 2 % d'offres en moins**, et 19 % d'offres en moins en TPE-PME ([JobTeaser Press](https://press.jobteaser.com/alternance-15-de-candidatures-en-plus-pour-2-doffres-en-moins-la-tension-monte-encore-dun-cran-4ru8x7)). Dans le supérieur, les entrées passent de 541 344 en 2024 à 501 091 en 2025 (-7,4 %), puis 54 478 de janvier à juillet 2026 contre 63 434 un an plus tôt (-14,1 %) ; le stock recule de 4,6 % en juillet 2026 ([Dares POEM](https://poem.travail-emploi.gouv.fr/donnee/contrat-dapprentissage-enseignement-superieur-entrees)). Le SIES relie la chute de 8,2 % des STS en apprentissage à la réduction des aides aux employeurs. Septembre pèse environ 57 % des entrées annuelles : l'effet de la rentrée 2026 ne sera visible qu'à partir de fin novembre.

Les aides ont changé le 8 mars 2026. Pour un employeur de moins de 250 salariés : 4 500 € au niveau 5 et 2 000 € aux niveaux 6-7 ; au-dessus de 250 salariés : 750 € aux niveaux 6-7 ([Service-public](https://entreprendre.service-public.gouv.fr/vosdroits/F23556)). L'embauche d'un bac+3 à bac+5 coûte donc plus cher à l'entreprise qu'avant ; c'est un moteur de difficulté de placement, **à ne pas coder en dur dans le produit** : aucun barème 2027 n'est connu.

### Un apprenti non placé coûte cher, mais pas tout de suite

Le CFA touche le niveau de prise en charge (NPEC) tant qu'un contrat est signé. La réforme 2026 fixe un plancher de 4 000 € et un plafond annoncé de 11 000 € pour les niveaux 5 à 7, dans une enveloppe France Compétences de 7,3 Md€, soit environ 1,1 Md€ de moins qu'en 2025 ([Ypareo](https://www.ypareo.com/blog-formation/reforme-npec-2026-cfa), [AlumnForce](https://www.alumnforce.com/reforme-npec-apprentissage-2026-ecoles-cfa/), sources d'éditeurs). **Hypothèse** : un apprenti non placé représente 4 000 à 11 000 € de recette annuelle perdue. Exemple illustratif : 500 apprentis, 5 % de contrats manquants, NPEC moyen de 8 000 € = 200 000 € par an. Avec le prix central du modèle (3 200 € par école de 400 étudiants), **un seul contrat sauvé par an dépasserait le prix annuel**. C'est l'argument de vente le plus fort, et il n'a pas été vérifié sur des NPEC réels.

Nuance honnête : pendant 3 mois, le candidat sans employeur a le statut de stagiaire de la formation professionnelle et les coûts de formation peuvent être pris en charge par l'OPCO (art. L6222-12-1, [Code du travail numérique](https://code.travail.gouv.fr/code-du-travail/l6222-12-1)). La perte n'est donc pas immédiate.

### Les payeurs dépendent du public

Pour les groupes contrôlés, le financement public lié à l'apprentissage représente « de 40 % à près de 70 % » du chiffre d'affaires ; 67 % au Collège de Paris ([IGAS/IGESR](https://igas.gouv.fr/sites/igas/files/2026-07/Rapport%20IGAS-IGESR_Contr%C3%B4le%20Enseignement%20priv%C3%A9%20lucratif.pdf), via [Headway Advisory](https://blog.headway-advisory.com/un-enseignement-superieur-prive-lucratif-a-reguler-demandent-ligas-et-ligesr/)). La même mission prévoit une consolidation du privé lucratif. Cela joue dans les deux sens : des acheteurs plus gros aux cycles plus longs, et des petites écoles moins solvables. **Le risque pour RedLine est budgétaire, pas un manque de besoin.** Le comparable américain pèse peu pour la France : Handshake reçoit environ 8 000 $ par université, mais monétise surtout les employeurs ([Sacra](https://sacra.com/c/handshake/), estimations).

## 4. Qualiopi crée un besoin de preuve, les CGU de l'API créent un risque de blocage

### Obligations de l'école : deux compteurs, pas un

Le Code du travail ne contient pas de « 6 mois sans contrat ». Il fixe **3 mois** pour le candidat sans employeur (L6222-12-1) et **6 mois** de poursuite de formation après une rupture (L6231-2) ; le CFA doit aider à trouver un employeur et prévenir les ruptures ([L6231-2](https://code.travail.gouv.fr/code-du-travail/l6231-2)). Le produit gère deux compteurs. Le référentiel Qualiopi passerait à 33 indicateurs au 1er novembre 2026, avec le traitement des ruptures (indicateur 14) et le suivi des sortants (29) ([Filiz, guide Qualiopi](https://www.filiz.io/blog/guide-qualiopi-cfa)). Le numéro du décret (2026-728) n'est confirmé par aucune source officielle lue. Le produit doit aussi savoir qui est le CFA et qui est l'école : le débiteur de L6231-2 est le CFA.

### La Bonne Alternance : la clause qui peut tout bloquer

Les CGU de l'API (version 1.0, 31 mars 2025, DGEFP) disent que l'utilisateur « s'engage à ne pas commercialiser les données reçues et à ne pas les communiquer à des tiers en dehors des cas prévus par la loi » ; l'éditeur peut modifier, suspendre ou bloquer un compte sans préavis ([CGU](https://api.apprentissage.beta.gouv.fr/fr/cgu)). Le site publie pourtant ses contenus sous licence etalab-2.0, qui autorise la réutilisation commerciale. **Les deux textes se contredisent et rien ne les départage.** Afficher des offres dans un produit facturé aux écoles peut être lu comme une commercialisation. Un argument défend RedLine (l'école paie le suivi, pas les offres), mais il n'a pas de base juridique lue. Action : demander à l'équipe une réponse écrite avant la production. Pour France Travail, l'API Offres d'emploi est sous Open Licence 2.0 à 10 appels par seconde ([data.gouv.fr](https://www.data.gouv.fr/dataservices/api-offres-demploi)), mais les CGU d'application sur francetravail.io n'ont pas pu être lues ; les CGU du site interdisent de constituer des fichiers de candidats hors recrutement ([France Travail](https://www.francetravail.fr/informations/informations-legales-et-conditio/conditions-generales-dutilisatio.html)).

### RGPD, AI Act, scraping

| Sujet | Ce que disent les sources | Conséquence |
|---|---|---|
| Rôles RGPD | L'école est vraisemblablement responsable de traitement, l'éditeur sous-traitant (**inférence**, non tranchée) | Si l'espace étudiant est privé, l'éditeur peut devenir responsable pour cette partie : à faire valider par un juriste ou un DPO |
| Mineurs | Consentement conjoint sous 15 ans pour les traitements fondés sur le consentement ([CNIL](https://www.cnil.fr/fr/recommandation-4-rechercher-le-consentement-dun-parent-pour-les-mineurs-de-moins-de-15-ans)) ; des étudiants de 17 ans existent | Fonctions optionnelles (IA) sur consentement adapté |
| AIPD | La liste CNIL n'a pas pu être lue (404) | À vérifier |
| AI Act | Un assistant de lettres pour l'étudiant n'est pas en annexe III ; haut risque reporté au **2 décembre 2027** par l'omnibus ; transparence (art. 50) applicable depuis le 2 août 2026 ([Quantic Avocats](https://www.quantic-avocats.com/2026/07/22/ai-act-digital-omnibus-report-obligations-haut-risque/), source secondaire) | **Aucun scoring ni classement d'étudiants par IA visible de l'école** : ce serait du haut risque |
| Scraping | La CNIL exige de respecter robots.txt et CAPTCHA ([CNIL](https://www.cnil.fr/fr/focus-interet-legitime-collecte-par-moissonnage)) ; les CGU peuvent interdire l'extraction contractuellement ([Ryanair C-30/14](https://www.pinsentmasons.com/out-law/news/website-operators-can-prohibit-screen-scraping-of-unprotected-data-via-terms-and-conditions-says-eu-court-in-ryanair-case)) | L'interdit de scraping est défendable ; formule : « uniquement des sources avec API ou licence ouverte » |

Les stages restent hors V1 : la convention engage la responsabilité de l'éditeur, et PStage occupe déjà le public ([Amue](https://www.amue.fr/publications/actualites/details/stages-etudiants-la-convention-nationale-de-stage-disponible-pour-les-etablissements)). Le produit peut suivre un statut (trouvé, en cours, convention signée) sans stocker la convention.

## 5. Sept risques majeurs et ce qu'ils imposent au produit

Les niveaux de gravité sont mon jugement, pas une mesure.

| Risque | Gravité | Ce que cela change |
|---|---|---|
| **Marché étroit** : SOM central de 181 k€ | Haute | Coût d'exploitation minimal, vente sans équipe commerciale lourde ; prévoir un second marché (CFA, établissements publics) avant de lever |
| **Centralisation par les groupes** : peu d'acheteurs, outils internes probables | Haute | Modèle de données hiérarchique groupe > école > promo ; SSO, export, API ; commencer par une école pilote d'un groupe |
| **CGU de La Bonne Alternance** : clause « ne pas commercialiser » | Haute | Chaque source d'offres derrière un adaptateur avec interrupteur ; liens sortants plutôt que copie ; durée de cache courte ; mode dégradé ; les **entreprises invitées** deviennent la source de base, pas un complément |
| **L'acheteur ne paie pas la confidentialité** : preuve Qualiopi, pression de transparence de l'IGAS | Haute | L'école reçoit des indicateurs et une preuve d'accompagnement (relances envoyées, statut), jamais le contenu ; le partage du détail est un choix de l'étudiant ; deux jeux de tables séparés (privé étudiant, agrégé école) |
| **Concurrents plus avancés ou mieux financés** (Bloom sur l'intégration, Grimp sur la détection) | Moyenne | La diffusion d'offres est gratuite ou presque : la valeur est le suivi ; intégration Ypareo, seul pont ERP nommé publiquement |
| **Baisse des entrées et solvabilité des écoles** | Moyenne | Contrat annuel, prix par étudiant suivi, pas de montants d'aides codés en dur |
| **Qualification RGPD et IA** | Moyenne | Hébergement UE, DPA, conservation courte, IA côté étudiant uniquement, étiquetée |

## 6. Ce qu'on ne sait pas, et cinq entretiens pour le savoir

### Contradictions entre sources, non résolues

| Sujet | Les versions | Traitement dans ce rapport |
|---|---|---|
| Entrées 2025 dans le supérieur | 497 900 (News Tank, estimation de février) contre 501 091 (Dares POEM, septembre 2026) | Dares retenue ; écart de 0,6 % |
| Apprentis du supérieur fin 2024 | 662 497 (Dares) contre 657 930 (DEPP) | Sources distinctes, non réconciliées |
| Privé lucratif | 226 000 (SIES) contre 400 000 à 450 000 | Les trois valeurs servent de scénarios |
| Offres d'alternance 2025 | -9,5 % contre -12 % (Hellowork) | Probablement des périodes différentes |
| Traction Grimp | 65, 150, 200, 250 ou 500+ écoles selon la page | Trajectoire 2023 seule retenue |
| Décret aides 2026 | Date limite 1er janvier 2027 ou 31 décembre 2026 ; une source dit que les grandes entreprises perdent l'aide aux niveaux 6-7, le Service-public leur accorde 750 € | Service-public retenu |
| Réforme NPEC | Modulation ±20 % ou jusqu'à 30 % ; application en mai ou au 1er septembre 2026 | Non tranché, aucun texte officiel lu |
| Handshake | Valorisation 1,5 Md$ (titre Forbes) contre 3,5 Md$ (Sacra) ; 1,10 Md$ de revenu annualisé contre 190 M$ en 2024 | Seul le prix par université est repris, avec réserve |
| Clause API La Bonne Alternance | Interdiction de commercialiser (CGU) contre licence etalab-2.0 | Non résolu, demande écrite nécessaire |

Deux erreurs de source corrigées. Une page de blog affirme « plus de 950 000 contrats signés en 2025 » : la Dares donne 846 700, la page est écartée. Les notes de recherche indiquaient environ 39 € par dossier au plus bas palier Filiz ; le calcul exact est 2 340 / 50 = 46,8 €, et 39 € correspond au palier Start (3 900 / 100). Le coût par dossier descend ensuite à 22,8 € au palier Premium.

### Chiffres non trouvés

Aucun taux national d'étudiants sans contrat à la rentrée, ni leur part dans le privé. Aucun effectif national de stagiaires. Aucun prix public de Hub3E, Bloom, Grimp, Go-Alternance, Pyramide. Pas de part des CFA privés. Pas d'effectifs 2025-2026 des groupes. Pas de NPEC moyen par école privée. Pas d'étude indépendante sur l'usage des tableurs. Pas de CGU francetravail.io. Pas d'entrées de septembre 2026. Le rapport IGAS n'a été lu que par extraits, les délibérations France Compétences et le décret du 6 mars 2026 pas du tout.

### Cinq entretiens d'école

Chaque entretien tranche une ou plusieurs hypothèses. Seuils de décision proposés par moi.

| # | Profil | Hypothèses | Questions précises | Seuil proposé |
|---|---|---|---|---|
| 1 | Directeur de l'alternance d'un **grand groupe** (siège) | A3, A4, A8, A9 | Qui signe un outil de suivi : le groupe ou l'école ? Existe-t-il un outil interne ? Combien de temps dure un appel d'offres ? Un pilote sur une école est-il possible sans le siège ? | Si le siège achète et construit en interne : A8 = 0 en central |
| 2 | Responsable relations entreprises d'une **école indépendante** (300-800 étudiants) | A5, A6, A7 | Quel outil utilisez-vous aujourd'hui et que coûte-t-il par an ? Combien de personnes suivent le placement, pour combien d'étudiants ? Quel prix par étudiant ou par an vous semble « évident » ? Qui décide ? | Prix évident hors de 5-12 € : revoir A6 |
| 3 | Responsable qualité d'un **CFA ou d'une école associative** | Valeur de la confidentialité, Qualiopi | Que montrez-vous à l'auditeur pour les indicateurs 14 et 29 ? Que perdez-vous si vous ne voyez qu'un statut global ? Qu'est-ce qui vous suffirait comme preuve ? | Si 3 entretiens sur 5 exigent le détail individuel : repenser l'offre |
| 4 | Responsable d'une école où le **stage domine** (commerce, ingénieur) | Part de stagiaires, périmètre stage | Quelle part de vos étudiants cherche un stage et non une alternance ? Qui gère les conventions (PStage, outil privé) ? Paieriez-vous pour le suivi de recherche de stage seul ? | Refus de payer pour le stage : TAM sur apprentis seuls (4,04 M€) |
| 5 | Directeur d'une école **cliente d'un concurrent** (Grimp, Bloom, Hub3E, Filiz) | A6, A7, coûts de changement | Combien payez-vous réellement ? Qu'est-ce qui vous manque ? Accepteriez-vous un outil qui ne montre pas le détail individuel ? Quel contrat vous lie, pour combien de temps ? | Prix réels hors de la zone Filiz : revoir A6 |

Deux questions transversales pour les cinq : combien d'apprentis non placés à la rentrée 2025 et quel NPEC moyen par apprenti (pour tester l'argument « un contrat sauvé paie l'outil »), et que feriez-vous si l'école ne pouvait plus afficher les offres de La Bonne Alternance.

## Conclusion

Le travail change la question. Il ne s'agit pas de savoir si le suivi d'alternance a un marché, mais si la confidentialité par étudiant se vend à ceux qui paient. Les chiffres disent que le volume est limité (SOM central de 181 k€), que la demande se durcit, et que l'argument économique est simple : un contrat sauvé couvre le prix annuel. Ils ne disent rien sur la disposition de l'école à renoncer au détail individuel, alors que Qualiopi et le contrôle de l'IGAS poussent vers plus de traçabilité.

Deux points peuvent se résoudre vite et à faible coût : la réponse écrite de la DGEFP sur la clause de commercialisation, et les entretiens 3 et 5, qui testent directement le pari. Si la clause se confirme ou si les écoles exigent le détail, l'architecture déjà décrite (adaptateurs de sources, entreprises invitées, séparation des données) limite le dégât. Dans le cas contraire, le produit a une place, mais pas encore une entreprise : il faudra élargir la cible avant de dimensionner une équipe.
