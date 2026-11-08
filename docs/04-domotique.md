# Audit basique de compatibilité domotique

[Retour à l'accueil](../README.md)

**Date : 8 novembre 2026.** Audit documentaire : notices, documentations de projets, métadonnées GitHub et quelques fichiers de configuration. Aucune intégration n'a été installée et aucun essai n'a été effectué sur le poêle. Ce document ne constitue pas un audit complet du code ou de la sécurité des projets cités.

## Conclusion

**Des voies d'intégration existent. La compatibilité du DOC suivi reste à confirmer après identification de sa connectivité.** Si son interface Maestro classique est confirmée, une liaison locale constitue la première piste à essayer. MQTT permet ensuite de choisir la plateforme domotique ; Home Assistant dispose aussi d'une piste locale directe.

## Identifier d'abord la génération

La notice DOC M1 décrit Maestro avec deux modules Wi-Fi [S11]. L'étiquette désormais reçue indique DOC Comfort Air `7117008A`, famille `7117008` présente au catalogue 2018 [S24, S25]. Une notice de l'ancienne famille décrit également Maestro avec Wi-Fi local et distant [S26]. Cela renforce la piste Maestro classique, sans prouver l'état actuel des modules ou leur protocole accessible. La notice DOC 9 M1 citée initialement concerne une autre référence [S27].

Maestro+ utilise notamment Bluetooth et Internet [S17]. Les noms **MCZ Maestro**, **Maestro MCZ**, **Maestro Upgrade** et **Maestro+** doivent être relevés exactement sur l'application utilisée. Une compatibilité annoncée pour une génération ne se transpose pas automatiquement aux autres : le plugin Jeedom mczremote exclut explicitement les appareils utilisant Maestro MCZ ou Maestro+ [S16].

## Compatibilité par outil

« Piste documentée » signifie qu'une voie est décrite par ses auteurs ; cela ne vaut pas validation sur ce DOC.

| Outil | Voie repérée | Local ou cloud | Évaluation pour le DOC suivi |
| --- | --- | --- | --- |
| Home Assistant, accès direct | [roondar/ha-mcz-maestro](https://github.com/roondar/ha-mcz-maestro) | Local, WebSocket | Candidate. Auteur : validation sur MCZ Dynamic et HA 2026.7.x ; DOC et HA actuel à tester [S14]. |
| Home Assistant, via MQTT | [MaestroGateway](https://github.com/Chibald/maestrogateway) et intégration MQTT climate | Local si le broker est local | Piste documentée ; configuration des entités et correspondance des paramètres nécessaires [S12, S18]. |
| Home Assistant, accès cloud | [Robbe-B/maestro_mcz](https://github.com/Robbe-B/maestro_mcz) | Cloud MCZ | Composant communautaire, compte utilisateur requis. Compatibilité du compte et de la génération à vérifier [S15]. |
| Jeedom, accès local | Passerelle locale puis MQTT | Local | Assemblage possible, commandes à configurer. La compatibilité MQTT n'est pas une installation automatique propre au DOC [S12, S16]. |
| Jeedom, mczremote | [Plugin de henribi](https://henribi.github.io/jeedom-plugin-mczremote/fr_FR/stable/) | Cloud MCZ, puis MQTT | Prévu pour Maestro classique accessible à distance ; exclut Maestro MCZ/Maestro+ selon sa documentation [S16]. |
| openHAB / Node-RED | MQTT avec adaptation des topics et valeurs | Local avec une passerelle locale | Voie générique documentée ; configuration à réaliser, sans validation DOC [S19, S20]. |
| Apple Maison / Siri | HomeKit Bridge après intégration dans Home Assistant | Pont local ; dépendance amont héritée de l'intégration du poêle | Envisageable pour les entités prises en charge. Aucun support HomeKit natif du DOC n'est établi ici [S21]. |
| Google Home / Assistant | Pont Google Assistant de Home Assistant | Dépendance aux services Google | Envisageable après intégration du poêle et exposition des entités compatibles ; aucun support direct du DOC n'est établi ici [S22]. |
| Alexa | Support annoncé par MCZ pour Maestro+ | Services connectés ; parcours à confirmer | L'annonce du fabricant ne confirme pas un accès direct pour un DOC Maestro classique [S23]. |
| Matter / Zigbee / Z-Wave directs | Aucune voie native établie par les sources examinées | Non déterminé | Ne pas considérer le DOC comme compatible nativement sur la seule base du Wi-Fi. |

## Projets examinés et état des sources

Les dates ci-dessous sont celles du dernier commit de la branche par défaut consulté, et non une mesure de fiabilité ou une garantie de support.

| Projet | Dernier commit consulté | Date | Point à retenir |
| --- | --- | --- | --- |
| Chibald/maestrogateway | [4c4e551](https://github.com/Chibald/maestrogateway/commit/4c4e551907790bfcc80b6f8d78aea858090e8087) | 15/10/2022 | Passerelle ancienne ; dépendances figées à examiner avant utilisation actuelle [S12, S13]. |
| roondar/ha-mcz-maestro | [17a0843](https://github.com/roondar/ha-mcz-maestro/commit/17a08433298218ce8c8f85dfc8f4dfeecddd7499) | 22/07/2026 | Piste directe récente ; périmètre de validation de l'auteur limité au modèle indiqué [S14]. |
| Robbe-B/maestro_mcz | [1104168](https://github.com/Robbe-B/maestro_mcz/commit/110416860bad4f6502de5bd783e709a8fd50fae7) | 06/11/2026 | Manifeste version 1.0.5, classe `cloud_polling` ; le README présente encore le projet comme bêta [S15]. |
| henribi/jeedom-plugin-mczremote | [abbae78](https://github.com/henribi/jeedom-plugin-mczremote/commit/abbae78ee391f139dc7e83eb660793b61490cc41) | 06/10/2024 | Limite de génération explicitée dans la documentation du plugin [S16]. |

La référence historique Anthony-55/maestro renvoie une erreur 404 lors de cette vérification. Elle n'est pas retenue comme solution directement récupérable à cette adresse.

## Points concrets à vérifier

- **Réseau local :** MaestroGateway décrit un pont entre Wi-Fi du poêle et Ethernet domestique, avec `192.168.120.1:81` par défaut. La joignabilité de cette interface reste à vérifier [S12].
- **Exemple MQTT à adapter :** le fichier Docker Compose consulté utilise un broker public et désactive l'authentification. Pour un essai domestique, prévoir un broker privé, authentifié et des droits adaptés aux topics de commande [S13].
- **Dépendances anciennes :** le fichier requirements consulté fixe `paho-mqtt===1.5.0` et `websocket-client===0.57.0`. Leur fonctionnement avec un environnement actuel n'a pas été testé ici ; aucune conclusion de vulnérabilité n'est tirée de leur seul âge [S13].
- **Concurrence des commandes :** le projet local direct demande un seul contrôleur WebSocket. Vérifier la coexistence avec l'application et éviter de lancer simultanément deux pilotes locaux [S14].
- **Alimentation :** une prise connectée ne doit pas servir de commande d'arrêt courante : le poêle doit terminer son cycle, pendant lequel les ventilateurs continuent de fonctionner [S23]. Utiliser les commandes normales du poêle.
- **Code technique :** les prérequis de la passerelle ne mentionnent pas `0434` [S12].

## Premier essai proposé

| Étape | Vérification | Résultat attendu |
| --- | --- | --- |
| 1. Identifier | Référence relevée : `7117008A`. Restent la version logicielle, le nom exact de l'application et le mode de connexion disponible | Choisir la bonne famille d'intégration. |
| 2. Choisir une seule liaison | Pour Maestro classique, examiner l'accès local ; tester la passerelle ou l'intégration directe séparément | Obtenir une connexion stable. |
| 3. Observer d'abord | Comparer état, température, alarmes et disponibilité avec l'application, sans modifier les réglages | Identifier les valeurs fiables et les données absentes. La précédente indication de sonde Wi-Fi débranchée doit être clarifiée si elle est encore présente. |
| 4. Vérifier la perte de réseau | Interrompre la liaison Internet ou réseau de test, sans couper l'alimentation du poêle | Détecter l'indisponibilité et éviter l'affichage de valeurs anciennes comme actuelles. |
| 5. Valider les commandes usuelles | Seulement après les contrôles précédents, en présence d'une personne : consigne et commande normale d'arrêt | Retour d'état cohérent et cycle d'arrêt conservé. L'allumage automatisé restera un essai distinct. |

Aucune de ces étapes n'est encore réalisée. Les droits MQTT, l'absence de commandes anciennes rejouées après reconnexion et le comportement en alarme restent à vérifier avant des automatismes.

## Choix conseillé à ce stade

**Pour Maestro classique, commencer par observer une liaison locale.** Choisir ensuite l'intégration directe si Home Assistant est l'outil retenu et si les paramètres du DOC sont reconnus ; choisir la passerelle MQTT pour relier plusieurs outils. Les limites du projet choisi devront être vérifiées sur l'appareil.

Le cloud reste une autre voie si l'application et le compte sont pris en charge ; il ajoute une dépendance à Internet et au service distant. Aucun achat ni choix définitif d'intégration n'est nécessaire avant d'avoir relevé les informations de l'étape 1.

[Sources détaillées S11 à S23](../SOURCES.md#domotique).
