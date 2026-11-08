# Sources et périmètre

[Retour à l'accueil](README.md)

Sources consultées les 7 et 8 novembre 2026. Les liens ci-dessous renvoient aux documents de référence ; la correspondance de la notice M1 avec l'appareil suivi reste à confirmer.

## Notice MCZ DOC M1

Notice du fabricant, DOC Comfort Air 9 M1 / DOC Comfort Air 9 UP! M1, partie 2, fonctionnement et entretien, hébergée par ManualsLib.

| Repère | Page et lien | Sujet utilisé dans la trame |
| --- | --- | --- |
| S1 | [Page 52](https://www.manualslib.fr/manual/282569/Mcz-Doc-Comfort-Air-9-M1.html?page=52) | Travail à froid et hors tension, nettoyage du brasier, aspiration des cendres |
| S2 | [Page 53](https://www.manualslib.fr/manual/282569/Mcz-Doc-Comfort-Air-9-M1.html?page=53) | Brasier, tiroir à cendres et remontage |
| S3 | [Page 54](https://www.manualslib.fr/manual/282569/Mcz-Doc-Comfort-Air-9-M1.html?page=54) | Vitre et filtre d'air selon équipement |
| S4 | [Page 55](https://www.manualslib.fr/manual/282569/Mcz-Doc-Comfort-Air-9-M1.html?page=55) | Nettoyage périodique de l'échangeur et du compartiment inférieur par un technicien qualifié |
| S5 | [Chapitre 30, alarmes](https://www.manualslib.fr/manual/282569/Mcz-Doc-Comfort-Air-9-M1.html?page=45) | Signification des alarmes, à relire sur la notice correspondant à la version exacte |

[Sommaire de la notice](https://www.manualslib.fr/manual/282569/Mcz-Doc-Comfort-Air-9-M1.html).

## Entretien annuel et ramonage

**S6 — Décret n° 2023-641 du 20 juillet 2023**, applicable depuis le 1er octobre 2023, reproduit sur le portail réglementaire AIDA de l'Ineris : [texte et dispositions du Code de la santé publique](https://aida.ineris.fr/reglementation/decret-ndeg-2023-641-200723-relatif-a-lentretien-foyers-appareils-chauffage-cuisine).

Points pertinents pour le guide :

- Article R. 1331-15 : contenu de l'entretien de l'appareil.
- Article R. 1331-16 : entretien au moins tous les douze mois, avec dérogation en cas d'absence totale d'utilisation précisée dans le texte.
- Article R. 1331-18 : définition du ramonage des conduits.
- Article R. 1331-22 : personne professionnellement qualifiée pour l'entretien et le ramonage.
- Article R. 1331-23 : remise d'une attestation à l'issue de chaque opération.

Le présent guide décrit le nettoyage courant de l'utilisateur. L'étendue d'une prestation professionnelle doit être vérifiée sur le devis et l'attestation correspondants.

## Menus et codes d'accès Maestro

Les accès sont décrits dans [la fiche des menus](docs/03-menus-et-codes.md). Les sources constructeur et les retours d'utilisateurs sont distingués ci-dessous.

| Repère | Source et emplacement | Ce qu'elle établit |
| --- | --- | --- |
| S7 | Notice MCZ DOC M1, partie 2, [page 34, « Recettes »](https://www.manualslib.fr/manual/282569/Mcz-Doc-Comfort-Air-9-M1.html?page=34) | Le code `1234` est donné pour l'accès aux recettes air et pellets. |
| S8 | Même notice, [page 41, « Menu technique »](https://www.manualslib.fr/manual/282569/Mcz-Doc-Comfort-Air-9-M1.html?page=41) | Le chemin d'accès et la demande d'un mot de passe sont décrits ; la notice ne publie pas le code du menu technique et présente cet accès comme destiné aux techniciens agréés. |
| S9 | BricoZone, [« Mot de passe menu technique poêle MCZ Maestro »](https://www.bricozone.be/t/mot-de-passe-menu-technique-poele-mcz-maestro.113086/), messages du 18 mai et du 12 octobre 2019 | Plusieurs utilisateurs rapportent l'accès au menu technique avec `0434`, notamment sur Club et Ego Maestro. Ce sont des témoignages, sans validation constructeur ni confirmation sur le DOC suivi ici. |
| S10 | Pelletkachelforum, [« MCZ Ego Maestro Service Melding Verwijderen »](https://pelletkachelforum.nl/home/topic/2233-mcz-ego-maestro-service-melding-verwijderen/), messages du 30 septembre 2024 et du 18 avril 2025 | Le code `0434` est à nouveau proposé en 2024 ; un utilisateur signale un refus en avril 2025 sans identification précise de la version. Cela ne permet pas de conclure à une modification générale du code. |

La notice DOC M1 est également accessible en [PDF, partie 2](https://chemineeo.fr/media/pdf/6d/a7/c2/FR-Mode-d-emploi-et-d-installation-Po-le-granul-s-MCZ-DOC-Comfort-Air-9-UP-M1-II.pdf). Les sources sont liées et résumées ; leurs pages et discussions ne sont pas recopiées intégralement dans le dépôt.

État au 8 novembre 2026 : aucun résultat d'essai des codes sur l'appareil du propriétaire n'a encore été communiqué.

## Domotique

Audit du 8 novembre 2026 : [compatibilité, limites et premier essai proposé](docs/04-domotique.md). Les dépôts ont été lus aux commits indiqués ci-dessous. Leurs fonctions annoncées n'ont pas été testées sur le DOC.

| Repère | Source | Élément vérifié |
| --- | --- | --- |
| S11 | Notice DOC M1, partie 2, [page 4](https://www.manualslib.fr/manual/282569/Mcz-Doc-Comfort-Air-9-M1.html?page=4) | Interface Maestro et deux modules Wi-Fi. |
| S12 | Chibald, [README au commit 4c4e551](https://github.com/Chibald/maestrogateway/blob/4c4e551907790bfcc80b6f8d78aea858090e8087/README.md) | Passerelle locale WebSocket/MQTT, réseau et prérequis. |
| S13 | Chibald, [requirements.txt](https://github.com/Chibald/maestrogateway/blob/4c4e551907790bfcc80b6f8d78aea858090e8087/requirements.txt) et [docker-compose.yml](https://github.com/Chibald/maestrogateway/blob/4c4e551907790bfcc80b6f8d78aea858090e8087/docker-compose.yml) | Dépendances figées ; exemple avec broker public et authentification désactivée. |
| S14 | roondar, [README au commit 17a0843](https://github.com/roondar/ha-mcz-maestro/blob/17a08433298218ce8c8f85dfc8f4dfeecddd7499/README.md) | Intégration HA locale directe, restriction à un contrôleur, validation déclarée sur Dynamic avec HA 2026.7.x. |
| S15 | Robbe-B, [README](https://github.com/Robbe-B/maestro_mcz/blob/110416860bad4f6502de5bd783e709a8fd50fae7/README.md), [manifest.json](https://github.com/Robbe-B/maestro_mcz/blob/110416860bad4f6502de5bd783e709a8fd50fae7/custom_components/maestro_mcz/manifest.json) et [config_flow.py](https://github.com/Robbe-B/maestro_mcz/blob/110416860bad4f6502de5bd783e709a8fd50fae7/custom_components/maestro_mcz/config_flow.py) | Solution cloud ; version 1.0.5 ; connexion par compte et mot de passe. |
| S16 | henribi, [documentation mczremote](https://henribi.github.io/jeedom-plugin-mczremote/fr_FR/stable/) et [dépôt au commit abbae78](https://github.com/henribi/jeedom-plugin-mczremote/tree/abbae78ee391f139dc7e83eb660793b61490cc41) | Jeedom, cloud et MQTT ; exclusion explicite de Maestro MCZ/Maestro+. |
| S17 | MCZ, [technologie Maestro+](https://www.mcz.it/en/maestro-technology) et [tutoriel officiel en français](https://cdn.mczgroup.com/mcz2023/files/MAESTRO-TUTORIAL-FR.pdf) | Connexions Bluetooth et Internet pour Maestro+. |
| S18 | Home Assistant, [MQTT climate](https://www.home-assistant.io/integrations/climate.mqtt/) | Possibilité de créer des entités de chauffage depuis MQTT ; ce n'est pas une certification MCZ. |
| S19 | openHAB, [MQTT Things and Channels](https://www.openhab.org/addons/bindings/mqtt/) | Topics d'état et de commande, transformations de valeurs. |
| S20 | Node-RED, [recettes MQTT](https://cookbook.nodered.org/mqtt/) | Réception, publication et messages JSON ; adaptation des flux nécessaire. |
| S21 | Home Assistant, [HomeKit Bridge](https://www.home-assistant.io/integrations/homekit/) | Exposition d'entités compatibles à Apple Maison/Siri. |
| S22 | Home Assistant, [Google Assistant](https://www.home-assistant.io/integrations/google_assistant/) | Pont vers Google Home/Assistant, avec configuration cloud ou manuelle. |
| S23 | MCZ, [FAQ](https://www.mcz.it/fr-ch/service-support-poeles-cheminees/foire-aux-questions?country=fr_CH), rubriques Alexa et durée d'arrêt | Alexa annoncé pour Maestro+ ; ventilation maintenue pendant l'arrêt. |

Les dates des projets sont issues des derniers commits des branches par défaut au moment de la consultation. L'absence de voie native Matter/Zigbee/Z-Wave dans cet audit est une limite des éléments trouvés, et non une preuve d'impossibilité technique.

## Règles éditoriales

Les observations sur l'appareil suivi et les prescriptions des notices seront distinguées dans le texte. La chute d'une pièce dans le brasier est une observation ; son rôle exact et son lien avec une alarme restent à établir. Les couples de serrage, outils ou procédures spécifiques ne seront pas inventés.

Les documents personnels, factures, coordonnées et identifiants de connexion ne font pas partie du tutoriel public. La licence de publication des textes et des photos originales reste à choisir.
