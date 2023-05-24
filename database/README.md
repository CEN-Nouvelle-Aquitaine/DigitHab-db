# DigitHab-db

## Concepts clés de la base de données

La digitalisation des habitats (communément appelée cartographie des habitats) permet de connaître à un instant t sur un territoire bien défini les formations végétales présentes (_cf. p11 du standard pour les définitions d'habitat, de végétation et de typologie_).

Les typologies d'habitats et de végétation s'appuient sur le référentiel national **HabRef** publié par PatriNat (version 6.0) :

- **EUNIS** (CD_TYPO = 7) : classification des habitats EUNIS
- **HIC** (CD_TYPO = 8) : liste hiérarchisée et descriptifs des habitats d'intérêt communautaire de la directive "Habitats"
- **Cahiers d'habitat** (CD_TYPO = 4) : liste hiérarchisée et descriptifs des habitats des Cahiers d'habitats

Les habitats sont regroupés au sein d'une unité écologique qui représente sur le terrain un milieu homogène. Cette unité écologique peut être digitalisée sous forme de polygone, de ligne ou de point.

Une unité écologique peut contenir un ou plusiers habitats : on parle alors de mosaïque d'habitats au sein de l'unité écologique (_cf. p13 du standard pour les définitions de mosaïques, correspondances et superpositions_).

 <br>

### Correspondances avec le modèle conceptuel de données du standard et les tables centrales

 <br>

- la table ***Evenement*** du standard contient les informations de l'objet géographique, l'observateur, la date d'observation et le type de mosaïque. Elle correspond à la table ***unite_ecologique*** de notre base de données.


 <br>




| Champ table Evenement | Champ table unite_ecologique  | Remarque correspondance | Description |
|:---------|:---------------|:---------------| :---------------|
|  | idue | | ***PKEY*** Identifiant unique technique de la ligne|
| idSinpJdd | idjdd | | Lien vers l'identifiant unique technique du jeu de données associé |
| idSinpEvenement | uuid_ue | identifiant unique SINP (UUID) généré automatiquement |
| ObjetGeographiqueType | | Généré automatiquement selon la géométrie de la table | |
| dateExacte | | Par simplification, la date exacte correspond au champ date1 si date2 non renseigné|
| dateDebut | date_debut | | Date de la description de l'unité écologique
| dateFin | date_fin | | Date de fin de description de l'unité écologique si la date est imprécise
| dateImprecise | | Sera à *vrai* si date_debut et date_fin sont renseignés |
| idOrigineEvenement |  | Généré automatiquement à partir du champ *idue*| Concatenation du champ *idue* avec une chaine de caractère de type "CENNA_ue_125"|
| observateur* | idcontrib |  | Lien vers l'identifiant unique du contributeur principal|
| organismeObs* | idorg |  | Lien vers l'identifiant unique de l'organisme lié au contributeur principal|
|  | idetude |  | Lien vers l'identifiant de l'étude liée à l'organisme du contributeur principal |
|  | lib_ue |  | Libellé de l'unité éclogique |
|estMosaique  | id_type_ue | Sera à vrai si une mosaique est renseignée dans les types d'unité écologique | Lien vers l'identifiant du type d'unité écologique |
|  | id_interet_ue |  | Lien vers l'identifiant unique de l'intérêt de l'unité écologique|
|  | rq_interet |  | Remarques sur l'intérêt de l'unité écologique|
| exposition | id_expostition |  | Lien vers l'identifiant unique de l'exposition |
| typeSol | id_type_sol |  | lien vers l'identifiant unique du type de sol |
| commentaire | rq_ue |  | Remarques générales sur l'unité écologique|

 <br>

- la table ***ObservationHabitat*** du standard contient les informations sur l'habitat (code, typologie, recouvrement, determinateur, etc.). Elle corespond à la table ***habitat_unite_ecologique*** de notre base de données.

 <br>
 
| Champ table ObservationHabitat | Champ table habitat_unite_ecologique  | Remarque correspondance | Description |
|:---------|:---------------|:---------------| :---------------|

 <br>

### Organisation de la saisie des informations

<br>

La cartographie des habitats doit permettre de comparer les effets de la gestion réalisée sur un site tous les 5 ans.

Il faut donc prévoir une gestion de millésime et un système de mise à jour. A contratrio de la gestion des données naturaliste d'occurence de taxon, une intervention géomatique est nécessaire afin de préparer en amont chaque projet de cartographie des habitats.

Fonctionnement prévu quand un chargé de mission prévoit de réaliser une cartographie d'habitat sur un territoire donné:

1. Il sélectionne l'ensemble du parcellaire à cartographier via le plugin QGIS Digit-Hab en précisant l'étude et l'année associée (ce couple etude/année devient l'identifiant de la cartographie)

2. Cette action à pour effet de créer en base de donnée un schéma et les tables (temporaires) nécessaires à cette digitalisation. L'utilisateur "base de données" est identifié grâce au compte CEN NA et l'extension LDAP2PG (pas besoin de gérer les utilisateurs en base). L'utilisateur a maintenant les droits INSERT, UPDATE, DELETE sur ces tables. Les administrateurs de données reçoivent une notification de création d'environnement de saisies avec toutes les infos et peuvent valider la demandr

3. Via le plugin QGIS Digit-Hab et une fois la demande validée, l'utilisateur a désormais accès aux tables PostGIS en édition et peut ainsi charger son environnement de saisie dans QGIS.

4. Une fois sa saisie terminée, il en informe les administrateurs qui peuvent alors procéder aux vérifications.

5. Une fois les vérifications terminées et les éventuelles erreurs corrigées, l'utilisateur a accès au module cartographique dans le plugin QGIS Digit-Hab lui permettant de créer les différentes cartes. Le modèle de carte spécifique à cette carto est réalisée par un géomaticien.

6. Une fois la carto terminée, les informations saisies sont injectées dans les tables générales afin d'alimenter la couche régionale.
Un tableau de bord avec un certain nombre de statistiques est mis en place pour cette cartographie. 
