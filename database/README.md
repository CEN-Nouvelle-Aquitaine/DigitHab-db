# DigitHab_db

## Concepts clés de la base de données

La digitalisation des habitats (communément appelée cartographie des habitats) permet de connaître à un instant t sur un territoire bien défini les formations végétales présentes (_cf. p11 du standard pour les définitions d'habitat, de végétation et de typologie_).

Les typologies d'habitats et de végétation s'appuient sur le référentiel national **HabRef** publié par PatriNat (version 6.0) :

- **EUNIS** (CD_TYPO = 7) : classification des habitats EUNIS
- **HIC** (CD_TYPO = 8) : liste hiérarchisée et descriptifs des habitats d'intérêt communautaire de la directive "Habitats"
- **Cahiers d'habitat** (CD_TYPO = 4) : liste hiérarchisée et descriptifs des habitats des Cahiers d'habitats

Les habitats sont regroupés au sein d'une unité écologique qui représente sur le terrain un milieu homogène. Cette unité écologique peut être digitalisée sous forme de polygone, de ligne ou de point.

Une unité écologique peut contenir un ou plusiers habitats : on parle alors de mosaïque d'habitats au sein de l'unité écologique (_cf. p13 du standard pour les définitions de mosaïques, correspondances et superpositions_).

### Correspondances avec le modèle conceptuel de données du standard et tables centrales

- la table ***Evenement*** du standard contient les informations de l'objet géographique, l'observateur, la date d'observation et le type de mosaïque. Elle correspond à la table ***unite_ecologique*** de notre base de données.

- la table ***ObservationHabitat*** du standard contient les informations sur l'habitat (code, tyologie,recouvrement, determinateur, etc.). Elle corespond à la table ***habitat_unite_ecologique*** de notre base de données.

