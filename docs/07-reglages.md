# Reglages du MCZ DOC Comfort Air — ancienne generation Maestro

[Accueil](../README.md) · [Appareil](00-appareil.md) · [Menus et codes](03-menus-et-codes.md) · [Guide nettoyage](01-nettoyage-courant.md)

**Etat : recherche documentaire du 21 novembre 2026 ; aucun reglage sur l'appareil n'a ete lu ou modifie par l'assistant.**

## Sources, generation et limites

- Appareil observe : MCZ DOC Comfort Air, code produit `7117008A`, etiquette `V: 00` (cette mention n'est pas une version firmware).
- **Source principale de cette fiche :** ancienne notice **DOC Comfort Air, Partie 2 — fonctionnement et entretien**, chapitres 18 a 30 [S44, S45]. Le document porte le nom « DOC Comfort Air » **sans suffixe M1**.
- Les documents **DOC Comfort Air 9 M1** datent d'une generation differente et ne valident pas les menus, codes ou valeurs de la revision `7117008A`. L'applicabilite exacte des fonctions et des recettes de la notice ancienne a cet exemplaire doit encore etre confirmee par la version firmware et une consultation sans modification des menus.
- Les applications iOS anciennes et Upgrade peuvent afficher des libelles et chemins differents ; les modes locaux et distants sont rapportes fonctionnels par le proprietaire.

## Reglages d'usage courant : notice DOC ancienne

| Fonction | Fonctionnement documente | Precaution ou limite |
| --- | --- | --- |
| **AUTO** | Reglage de la temperature ambiante souhaitee ; regulation de puissance du poele ; possibilite de la fonction ECO STOP. | La sonde ambiante effectivement selectionnee doit donner une temperature representative. |
| **MANUEL** | Reglage de la puissance de flamme, sans regulation automatique par la consigne ambiante. | ECO STOP n'est pas disponible en MANUEL. |
| **Ventilateurs Comfort Air** | Pour chaque ventilateur disponible : cinq niveaux, AUTO ou arret. | Le mode manuel de ventilation peut limiter la puissance maximale du poele ; ne pas en deduire le nombre exact de ventilateurs sur cet exemplaire. |
| **SILENT** | Puissance de flamme reduite a P1 ; ventilation ambiante arretee apres environ 10 min. Fonction des modes AUTO et MAN, non disponible en TIMER selon la notice. | Ce n'est pas une extinction du poele, ni une desactivation des protections ou de l'extraction de fumees. |
| **ECO STOP** | Si la consigne reste satisfaite pendant le delai choisi, le poele s'arrete, puis peut redemarrer a la baisse de temperature. Delai indique : 5 a 30 minutes. | MCZ le recommande surtout dans les locaux suffisamment isoles pour eviter des allumages/extinctions trop rapproches. L'hysteresis est presentee en °C mais la transcription lui attribue par erreur une plage « 2 a 5 minutes » : **unite incoherente, ne pas retenir ce chiffre comme consigne sans preuve supplementaire**. |
| **SLEEP** | Programmation ponctuelle d'une heure d'extinction, disponible en AUTO et MAN. | Ne correspond pas a un reglage de combustion. |
| **CHRONO** | Programmation hebdomadaire par demi-heures avec trois temperatures T1, T2 et T3. | Avant d'activer une plage d'allumage automatique, s'assurer que le poele est mécaniquement sain et correctement entretenu. |
| **Entree ambiance** | Choix de la sonde Wi-Fi, du thermostat ou de la sonde d'ambiance selon equipement. | Si la sonde Wi-Fi n'est pas presente ou est deconnectee, verifier la source de temperature selectionnee avant d'interpréter une anomalie. |
| **Autres bases** | Langue, date et heure, °C/°F, sons, liste des appareils, accessoires, configuration de sonde Wi-Fi. | Les ecrans « versions du logiciel » peuvent montrer des secrets d'appairage : pas de capture brute publique. |

References : ancienne notice, chapitres 18 a 24 et 29-30 [S44, S45].

## Recettes de combustion : valeurs expliquees dans l'ancienne notice

**Les valeurs ci-dessous sont des indications documentaires de la notice candidate, et ne sont PAS une prescription de correction.** Elles influencent la combustion, les emissions, la stabilite de flamme et potentiellement la securite de fonctionnement. Ne pas les modifier simplement sur la foi du machefer observe sur les photos.

| Recette PELLET | Effet annonce sur l'apport de granules, a toutes les puissances |
| ---: | --- |
| `-3` | -20 % |
| `-2` | -13 % |
| `-1` | -6 % |
| `0` | Aucune correction |
| `+1` | +3 % |
| `+2` | +6 % |
| `+3` | +10 % |

| Recette AIR | Effet annonce sur l'air de combustion |
| ---: | --- |
| `-2` | -10 % |
| `-1` | -5 % |
| `0` | Valeur par defaut dans la notice |
| `+1` | +5 % |
| `+2` | +10 % |

Ces tableaux correspondent au chapitre 26 « Recettes » de la notice ancienne [S44, S45]. Le code `1234` est **publie pour les recettes sur la notice M1**, mais n'est **pas confirme pour ce DOC**. Un code de menu n'equivaut pas a une autorisation de modifier les reglages.

### Machefer : diagnostic avant toute correction

L'ancien manuel envisage comme causes possibles d'une flamme faible, d'une accumulation de granules ou d'une vitre tres sale : **passages d'air du creuset bouches, arrivee d'air insuffisante, encrassement de la chambre ou des conduits, joints de porte, granules humides ou inadaptes** [S44, S45, section « Pannes/causes/solutions »].

Dans le cas suivi :
- Trois photos initiales montraient des depots importants ; les cinq photos suivantes montrent un nettoyage efficace, avec orifices majoritairement degages. Aucune rupture du metal n'est prouvee sur photos.
- L'appui correct du creuset, la piece tombee pres de l'arrivee des granules et l'etat reel du circuit de fumee restent a valider. Des alarmes A01/A02 avaient ete signalees : leur cause reste indeterminee.
- **Ordre a privilegier** : integrite et position des pieces, trous d'air propres, qualite et stockage des granules, prise d'air, joints/evacuation et entretien technique ; ensuite seulement, lecture des valeurs actuelles et diagnostic instrumente en cas de combustion anormale persistante.
- Le manuel recommande de ne pas neutraliser les securites. Pas de recette « anti-machefer » universelle et pas de modification du tirage, du capteur ACTIVE, du pressostat, des regimes de moteurs ou des parametres de base de donnees sans professionnel et mesures adequates.

## Configuration / menu technique

- **Activer vis sans fin** : remplissage du circuit d'alimentation uniquement apres vidange du reservoir, avec poele eteint, selon chapitre 25 ; ce n'est pas un reglage courant du debit de granules.
- **ETE/HIVER** : choix de saison ; fonction mentionnee mais effet exact sur cet exemplaire non qualifie.
- **Menu technique** (chapitre 28) : parametres, ACTIVE ON/OFF, diagnostics, banque de donnees, remise a zero usine/service, dernieres alarmes, heures de fonctionnement, SERIAL BAUD. **Reserve au technicien specialise MCZ dans la notice**.
- **Version logiciel** (chapitre 29) et **INFO** (chapitre 30) : rubriques pertinentes pour observer la version carte/Wi-Fi/base de donnees, les etats et les alarmes, sans enregistrer de changement.
- Le code `0434` est rapporte dans des forums pour d'autres poeles Maestro mais non valide sur ce `7117008A`. Ne pas l'utiliser pour rechercher des changements de securites.

## Releves utiles sur l'exemplaire (sans ecriture)

| Champ a relever hors secrets | Etat |
| --- | --- |
| Nom exact et version de chaque application iOS | Inconnu |
| FW carte, Wi-Fi HOME, Wi-Fi distant, banque de donnees | Inconnus |
| Mode AUTO ou MANUEL en cours | Inconnu |
| Consigne et source de temperature ambiante | Inconnues |
| Ventilation des zones Comfort Air | Inconnue |
| SILENT / ECO STOP / CHRONO actifs ou non | Inconnus |
| Recette PELLET et AIR actuellement enregistrees | Inconnues |
| Historique d'alarme et heures de fonctionnement | Non releves ici |

Les photos d'ecran doivent **masquer mot de passe Wi-Fi HOME, QR, numero de serie et MAC distante** avant publication. Aucun essai de modification ne fait partie de cette fiche.

[Sources generales](../SOURCES.md#reglages-de-lancienne-generation-doc-comfort-air).
