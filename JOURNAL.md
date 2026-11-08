# Journal de préparation

[Retour à l'accueil](README.md)

## 7 novembre 2026

### Observations rapportées par le propriétaire

- Poêle identifié comme un MCZ DOC ; version complète à relever.
- Nettoyage par aspiration effectué la veille.
- Une pièce appelée « clapet de l'arrivée des granulés » est tombée dans le brasier pendant ce nettoyage.
- Cette pièce a ensuite été remise en place par le propriétaire.
- Alarmes A02 puis A01 affichées dans l'application.
- Une relance a été effectuée sans vider de nouveau le brasier.

### Ce qui reste à vérifier sur l'appareil

- Référence exacte et notice correspondante.
- Identification de la pièce appelée « clapet » et de son maintien dans son logement.
- État du brasier après les tentatives d'allumage.
- Résultat de la remise en route : non communiqué à ce stade.
- Photos réelles de chaque étape de nettoyage et de remontage.

### Préparation éditoriale

- [x] Première trame et sources réunies.
- [x] Liste des prises de vue préparée.
- [ ] Référence exacte confirmée.
- [ ] Intervention photographiée.
- [ ] Légendes et gestes vérifiés sur l'appareil.
- [ ] Relecture finale et choix de licence avant publication.

## 8 novembre 2026

- Ajout d'une fiche consacrée aux accès de l'application MCZ Maestro.
- Code `0434` documenté comme accès au menu technique rapporté par des utilisateurs, à confirmer sur le DOC suivi.
- Code `1234` documenté pour le menu Recettes de la notice DOC M1.
- Sources constructeur et forums référencées, avec leurs limites et un signalement de refus de `0434` en 2025 sur un appareil non précisément identifié.
- Aucun essai accepté ou refusé sur le DOC du propriétaire n'est encore rapporté ; aucun réglage du poêle n'a été modifié dans le cadre de cette mise à jour documentaire.

### Audit basique de compatibilité domotique

- Ajout d'une comparaison Home Assistant, Jeedom, openHAB, Node-RED et ponts vocaux, avec distinction local/cloud et générations Maestro.
- Quatre projets consultés à des commits précis ; configuration MQTT d'exemple et dépendances anciennes relevées.
- Limites de compatibilité du DOC conservées ; plan d'essai proposé en commençant par l'observation des états.
- Recherche documentaire uniquement : aucune intégration installée, aucune connexion au poêle et aucune commande effectuée.

### Identification par l'étiquette

- Étiquette reçue : `ST. DOC C-AIR`, code `7117008A`, mention `V: 00`.
- Base `7117008` rapprochée du DOC Comfort Air du catalogue 2018. Date de fabrication et signification du suffixe A non établies.
- Correction du choix de notice : le DOC 9 M1 à sortie arrière utilise `7118016`. Les références M1 du guide restent comparatives ; une notice DOC Comfort Air de l'ancienne famille a été repérée.
- Fiche d'appareil ajoutée. Photo originale et numéro de série non publiés.
- Aucun essai domotique ni validation des codes d'accès effectué.

### Conservation des applications et risque cloud

- Signalement des deux applications iOS conservees : l'ancienne MCZ Maestro (bandeau inferieur devenu inutilisable) et la nouvelle application avec compte utilisateur. Nom et versions exacts a relever localement.
- Confirmation documentaire du bug de bandeau apparu chez plusieurs utilisateurs sous iOS 16.4 au printemps 2023, et de la mise a disposition de Maestro - Upgrade.
- Mode Wi-Fi Direct/HOME sans Internet documente pour Maestro classique, mais **pas encore valide sur ce DOC**.
- Audit de risque : confidentialite et disponibilite du cloud, commandes distantes non autorisees, securites physiques distinguees ; aucune faille exploitable n'est ici etablie.
- Aucun test sur le poele, aucune modification des reseaux ou des parametres ; numero de serie, MAC, QR code et identifiants non publies.

### Observation complementaire sur les applications (8 novembre 2026)

- Le proprietaire signale que les deux applications fonctionnent et semblent utilisables en local comme a distance.
- Cette distinction n'a pas ete verifiee par un test avec le Wi-Fi de l'iPhone desactive : **le fonctionnement effectif en 4G/5G reste incertain**.
- Essai propose : desactiver le Wi-Fi de l'iPhone dans Reglages, conserver les donnees cellulaires, observer uniquement la remontee des etats dans chaque application, sans commande ni modification des reglages du poele.
- Le succes de ce test etablirait une voie distante, mais non une exposition entrante directe du poele a Internet ni une vulnerabilite exploitable.
