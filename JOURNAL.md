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

### Audit de code et protocoles - complement du 8 novembre 2026

- Le proprietaire confirme le fonctionnement des deux applications a la fois en local et a distance. Le test d'isolement des chemins de communication reste a faire ; ne pas redemander l'observation deja apportee.
- Lecture du code de deux clients WebSocket locaux et d'un client communautaire pour l'ancien service distant ; comparaison avec une integration du cloud moderne utilisant HTTPS et jeton d'acces.
- Identification d'un risque conditionnel de l'ancien canal distant (identifiants techniques et HTTP dans le code client), **sans preuve de faille exploitable du service actuel**.
- Documentation du risque Wi-Fi HOME, d'un reseau temporaire de configuration ouvert et des secrets visibles dans la page de version logicielle.
- Priorites P1/P2/P3, questions au fabricant et precaution de masquage detaillees dans [l'audit](docs/05-audit-cybersecurite.md).
- Aucun contact avec le poele ni avec les services de commande MCZ ; aucun scan, changement de configuration, essai de code technique ou commande. Aucune donnee privee enregistree dans le depot.

## 21 novembre 2026 - Controle complementaire du brasier

- Cinq photographies privees supplementaires apres decrassage : interieur, parois, dessous et marquage moule.
- Depots importants retires ; perforations majoritairement ouvertes. Traces orange et sombres residuelles ; pas de fissure traversante evidente, mais aucun controle physique de la fonte.
- Reference de remplacement du brasier DOC Comfort Air ancien identifiee : **`4130170030100`**, repere 12 [S42, S43]. Ne pas assimiler directement le marquage moule a cette reference ; compatibilite revision A a confirmer.
- Verifier la position du brasier et la piece tombee a l'arrivee des pellets avant remise en service ; anciennes alarmes A01/A02 non expliquees.
- Aucune photographie personnelle publiee ni test de remise en route realise par l'assistant.

## 21 novembre 2026 - Brasier photographie

- Reception de trois vues du brasier extrait, **non publiees** : vue generale, gros plan du fond et de la paroi arriere, vue oblique.
- Depots de combustion abondants et trous visiblement encrasses ; fissure ou alteration du metal **non etablie** sous les depots.
- Comparaison au chapitre 34, pages 50-51 de la notice DOC Comfort Air ancienne [S41], en conservant l'incertitude de revision A.
- Nettoyage, contre-vues du dessous et controle du logement a documenter ; pas de reallumage si doute sur une fissure, le positionnement du brasier ou la piece tombee precedemment.
- Les alarmes A01/A02 sont conservees comme observation anterieure, sans attribution causale certaine.
- Aucune intervention physique, commande, mise a jour de firmware ou publication des photos effectuee par l'assistant.

### 21 novembre 2026 - Sauvegarde des images du brasier

- Les **8 originaux** de la serie avant/apres ont ete archives dans une [page privee](https://chatgpt.com/space/page_71a5cbe16810819182d5ffaf137c559b) : 3 avant et 5 apres. Une archive ZIP verifiee contient les 8 JPEG, les planches contacts, l'inventaire et les SHA-256.
- Inventaire ajoute au depot public dans [`docs/06-brasier-photos-2026-11-21.md`](docs/06-brasier-photos-2026-11-21.md) ; **aucun JPEG original n'est televerse sur GitHub** a ce stade.
- Le marquage de fonderie sous le creuset est photographie mais non lisible integralement. Le numero de serie du poele est absent des huit cliches et n'est ni invente ni publie.
