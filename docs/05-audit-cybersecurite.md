# Audit de cybersecurite - MCZ DOC Comfort Air 7117008A

[Retour a l'accueil](../README.md)

**Date : 8 novembre 2026 - phase documentaire uniquement.** Aucun acces au poele, aucune capture de trafic, aucun scan, aucune commande et aucun test d'intrusion n'ont ete effectues. Ce dossier ne certifie ni la securite ni l'existence d'une faille exploitable sur le firmware de l'exemplaire. Photo de plaque, QR code, identifiants Wi-Fi, adresse MAC et numero de serie restent exclus du depot public.

## Verdict

**Exposition plausible, vulnerabilite exploitable non demontree pour ce DOC.**

Le modele est identifie par l'etiquette comme `ST. DOC C-AIR`, reference `7117008A`, `V: 00` (non assimile au firmware). Le protocole **Maestro classique** et le mode Wi-Fi Direct sont des pistes serieuses, mais la generation du module, le logiciel embarque et les parametres reseau de l'exemplaire n'ont pas encore ete verifies.

| Surface | Observation et preuve | Consequence possible | Statut |
| --- | --- | --- | --- |
| Commandes locales | Les projets communautaires MaestroGateway [S12] et ha-mcz-maestro [S14] ouvrent un canal local WebSocket non chiffre `ws://` et emettent leurs requetes sans identifiant ou jeton applicatif additionnel visible dans leur client. | Un tiers qui **a deja acces au reseau du poele** pourrait potentiellement lire ou envoyer des ordres. La presence d'un controle interne supplementaire sur la carte reste a verifier. | **Signal de risque**, non teste sur ce DOC. |
| Association Wi-Fi directe | La notice de la famille DOC Comfort Air ancienne decrit un mot de passe local associe au QR code [S32]. | La confidentialite du mot de passe Wi-Fi est une barriere potentiellement essentielle. | Documente pour la famille, correspondance exacte a confirmer. |
| Association distante et cloud | Les notices Maestro documentent une association par numeros de serie et MAC ; Upgrade requiert un compte, et des outils communautaires pilotent les poeles depuis le cloud [S29, S30, S34]. | Vol ou abus de compte, partage non souhaite, indisponibilite du service ; controles d'association et protections du backend non audites. | Exposition structurelle, **aucun piratage ni contournement confirme**. |
| Code du menu technique | `0434` est un code rapporte sur plusieurs produits Maestro et non verifie sur celui-ci [S9, S10]. | Ce n'est pas un secret personnel et ne doit pas etre considere comme protection de la connexion reseau. | A confirmer ; ne pas modifier les reglages de combustion. |
| Passerelles domotiques | L'exemple de configuration de MaestroGateway designe un broker MQTT public et `MQTT_authentication=False` [S13]. | Une installation naive pourrait exposer une interface de **commande** par MQTT ; cela concerne la passerelle **si elle est installee**, pas le poele tel qu'il se trouve aujourd'hui. | Exemple dangereux a ne pas reutiliser tel quel ; aucune passerelle installee. |
| Securites physiques | Le poele est un appareil de combustion avec des alarmes et une procedure d'arret. L'ancienne integration locale permet des commandes classiques, pas la preuve d'un contournement de securite. | Un allumage non autorise ou inopportun est deja un risque ; une neutralisation des protections internes **n'est pas demontree**. | Ne pas conclure a un risque d'incendie provoque a distance sans validation. |

Une absence de fiche CVE publiee ou retrouvee ne signifie pas qu'un appareil est exempt de failles. Cette recherche n'est pas un audit du firmware ou du service cloud MCZ.

## Examen complementaire du protocole (8 novembre 2026)

### Perimetre et constat du proprietaire

Le proprietaire confirme que **ses deux applications MCZ fonctionnent en usage local et distant**. Les routes effectives pour chaque operation n'ont pas ete observees par capture reseau et pourraient varier selon le mode. Ne pas presenter une application qui affiche un etat comme preuve suffisante de fonctionnement totalement hors ligne.

L'audit compare quatre depots communautaires et les notices Maestro : ce sont des **preuves du comportement des clients logiciels**, pas des mesures sur le serveur, sur le firmware du DOC ni sur la securite du reseau domestique.

### Constat A - canal local : authentification applicative absente des clients communautaires

- [roondar/ha-mcz-maestro, `config_flow.py`](https://github.com/roondar/ha-mcz-maestro/blob/main/custom_components/mcz_maestro/config_flow.py) n'exige que l'hote et le port, puis interroge les informations et parametres.
- [roondar/ha-mcz-maestro, `api.py`](https://github.com/roondar/ha-mcz-maestro/blob/main/custom_components/mcz_maestro/api.py) etablit une liaison `ws://` et envoie des messages de lecture et d'ecriture sans transmettre de secret applicatif additionnel. Le module n'implemente pas `wss://`.
- [Chibald/maestrogateway, `maestro.py`](https://github.com/Chibald/maestrogateway/blob/master/maestro.py) utilise aussi un client WebSocket local sans procedure d'authentification visible. Sa notice indique que le poele emet son propre reseau Wi-Fi ; les composants de ce depot sont valides par leurs auteurs sur d'autres modeles, pas sur notre DOC.

**Interpretation :** si le DOC utilise le meme protocole et si un tiers obtient deja un acces reseau au module Wi-Fi HOME, l'absence d'authentification supplementaire des clients cree une possibilite serieuse de commande abusive. Il reste a etablir les verifications effectuees par le module et les protections du Wi-Fi HOME de cet exemplaire. **`ws://` ne signifie pas que le reseau radio est necessairement non chiffre** : le Wi-Fi peut fournir une protection distincte.

### Constat B - ancien acces distant : identifiants statiques et transport non chiffre dans les clients observes

- [davide-travaglini/node-red-contrib-mcz, `mcz-config.js`](https://github.com/davide-travaglini/node-red-contrib-mcz/blob/2cf3478322ceea58e63ebfec54ab1f9edbd87e61/nodes/mcz-config.js), dernier commit examine du 24 octobre 2026 : le client affiche par defaut une liaison Socket.IO vers un endpoint `http://` de l'ancien cloud MCZ. Dans le flux `join`, il transmet le numero de serie et l'adresse MAC ; **aucune etape de connexion au compte utilisateur ou fourniture d'un jeton n'est visible dans ce client** [S35].
- Un [journal publie dans la communaute Home Assistant en avril 2023](https://community.home-assistant.io/t/control-mcz-maestro-pellet-stove-via-hacore-trough-mqtt/238423?page=9) montre la meme famille de messages Socket.IO, une connexion HTTP et des identifiants d'appareil masques [S36].
- Les anciennes notices Maestro decrivent l'ajout d'un poele distant au moyen du numero de serie et de la MAC distante [S31]. La page de migration de MCZ Danemark indique que l'ancienne application devait fermer en avril 2024 [S30], mais l'utilisateur signale qu'elle fonctionne toujours ; **cela ne confirme pas quel endpoint elle emploie aujourd'hui**.

**Interpretation :** si ce protocole non chiffre reste effectivement accepte et si les deux identifiants techniques suffisent a autoriser des commandes, l'exposition serait importante : interception possible en transit et risque d'usurpation si les identifiants sont divulgues. **Aucune verification serveur, tentative d'usurpation ou preuve d'exploitation n'a ete effectuee**. Ne pas qualifier cette hypothese de faille exploitable du DOC tant que les controles serveur ne sont pas qualifies.

### Constat C - nouveau cloud : authentification utilisateur visible dans le client

- [Robbe-B/maestro_mcz, `config_flow.py`](https://github.com/Robbe-B/maestro_mcz/blob/main/custom_components/maestro_mcz/config_flow.py) demande un compte et un mot de passe.
- [Robbe-B/maestro_mcz, `maestro_controller.py`](https://github.com/Robbe-B/maestro_mcz/blob/main/custom_components/maestro_mcz/maestro/controller/maestro_controller.py) etablit une session et emploie un jeton pour les demandes suivantes ; le fichier [`const.py`](https://github.com/Robbe-B/maestro_mcz/blob/main/custom_components/maestro_mcz/maestro/controller/const.py) utilise un service `https://` [S37].

**Interpretation :** cette voie applique des mecanismes de compte et de jeton absents du client historique analyse. Elle reste exposee aux risques classiques de reutilisation de mot de passe, compromission de compte, erreurs de droits, panne de service et comportement du serveur inconnu. L'absence de documentation MFA ne permet pas d'affirmer que cette option est indisponible.

### Constat D - reseaux de configuration, secrets et donnees partageables

- La notice Maestro premiere generation decrit un reseau de configuration du module distant **ouvert pendant les operations de parametrage**, qui disparait lorsque le module a rejoint la box [S38]. On ne sait pas si le module de ce DOC expose actuellement ce mode. Une reinitialisation volontaire n'est pas necessaire ni recommandee pour l'audit.
- Dans une notice Maestro M1 comparable, l'ecran « SOFTWARE VERSION » comprend a la fois les versions logicielles **et le mot de passe du Wi-Fi HOME, le numero de serie et la MAC distante** [S39]. Il serait imprudent de publier une capture brute de cet ecran ou de l'envoyer dans une issue publique. Transcrire uniquement les versions utiles.
- Le code technique `0434` (non verifie sur le DOC) ne securise ni la couche Wi-Fi ni le protocole de commande normal ; il ne remplace pas une authentification reseau.

### Hierarchisation pour le DOC 7117008A

| Priorite d'investigation | Exposition | Niveau de preuve | Prochaine verification sans commande |
| --- | --- | --- | --- |
| P1 | Ancien protocole distant par identifiants techniques et HTTP dans un client communautaire | **Code client et traces historiques confirmes** ; protocole reel actuel, autorisation serveur et exploitation inconnus | Identification des applications et versions ; question documentee au fabricant sur l'authentification de l'ancien service et sa disponibilite |
| P1 | Commandes sur WebSocket Wi-Fi HOME sans secret applicatif supplementaire dans deux clients | **Code des clients confirme** ; firmware du DOC non teste | Relever la version Wi-Fi HOME, verifier passivement la protection du SSID |
| P2 | Compte cloud recent et utilisateurs invites | Authentification visible ; droits et securite serveur non audites | Mot de passe unique, revue des utilisateurs autorises |
| P2 | Reseau temporaire de configuration ouvert | Decrit dans notice familiale, pas observe sur le DOC | Regarder si un reseau de configuration anormal persiste, sans s'y connecter |
| P3 | Coupure du cloud et perennite du controle | Modes locaux annonces dans la famille, aucune preuve de fonctionnement autonome integral de l'application | Qualifier plus tard la lecture des etats en HOME sans Internet, pas d'ordres |

**Important :** il n'existe pas ici de demonstration qu'un pirate pourrait contourner les securites anti-surchauffe, de tirage, de fumee ou de fermeture. Une mise en marche inopportune reste toutefois un risque a traiter, independamment de tout contournement. Les alarmes A01/A02 et la piece tombee dans le brasier restent une question de maintenance non resolue.

### Questions a adresser a MCZ (aucune publication d'identifiants)

1. Pour `7117008A`, quelles versions de firmware sont les plus recentes pour la carte, le Wi-Fi HOME et le module distant, et comment les verifier sans mise a jour automatique ?
2. L'ancien canal distant de type Socket.IO est-il encore actif ? Exige-t-il une authentification et une autorisation **autres** que numero de serie et adresse MAC ?
3. Peut-on revoquer une association a distance compromise, renouveler les secrets Wi-Fi HOME, ou desactiver uniquement le controle distant tout en conservant la commande HOME et les fonctions physiques ?
4. Le canal WebSocket HOME exige-t-il un controle applicatif au niveau du module en plus de l'acces Wi-Fi ? Si oui, lequel ?
5. Quelles mesures d'authentification et de revocation sont disponibles pour Maestro Upgrade (utilisateurs invites, MFA eventuel, sessions) ?
6. Comment signaler en prive un defaut de securite et obtenir les consignes de mitigation pour cette generation ?

**Interdictions pendant la qualification :** pas de scan agressif, pas de brute force, pas de test d'ecriture, pas de modification des recettes de combustion, pas d'essai d'allumage, pas de desactivation des securites et pas de publication d'identifiants. Un audit de code du client ne remplace pas une qualification sous controle du constructeur.

## Protection immediate et raisonnable

1. **Preserver les donnees d'appairage hors publication** : photographie QR, mot de passe HOME / PWD, numero de serie, adresse MAC et justificatifs.
2. **Compte MCZ** : employer un mot de passe long, unique, non reutilise. Examiner dans Upgrade les utilisateurs autorises et retirer les acces inconnus. Verifier si une authentification multifacteur est proposee, sans la supposer disponible.
3. **Routeur** : utiliser le chiffrement Wi-Fi et la protection administration de la box, maintenir les mises a jour et verifier qu'aucune redirection de port ou ouverture UPnP ne rend une interface domotique accessible depuis Internet. Ceci **ne bloque pas le service cloud** : celui-ci peut utiliser des connexions sortantes.
4. **Ne pas ajouter de passerelle par defaut** : ni broker MQTT public, ni pont sans authentification, ni automatisation de mise en marche.
5. **Ne jamais couper brutalement l'alimentation d'un poele en fonctionnement** pour faire un test reseau ; respecter son cycle normal de refroidissement.

## Protocole de qualification sans modification

Le proprietaire a deja confirme l'usage des deux applications en local et a distance ; ne pas lui redemander de prouver cette declaration. Restent a determiner leurs versions, la voie de communication utilisee et les controles d'acces du module.


Condition prealable : identifier et securiser la piece tombee dans le brasier et resoudre les alarmes A01/A02 deja inscrites au [journal](../JOURNAL.md). Pas d'allumage distant ni d'essais de commandes tant que le fonctionnement mecanique n'a pas ete valide.

- [ ] Relever en prive les noms et versions des **deux applications iOS**, et la version logicielle du poele si l'application l'affiche.
- [ ] Observer le nom du reseau Wi-Fi propre au poele sans reveler ses identifiants ; identifier si ce reseau est protege (sans tentative de deviner le mot de passe).
- [ ] Observer le mode de connexion de chaque application (HOME/DIRECT, REMOTE) et les utilisateurs partages.
- [ ] Sur la box, recenser les clients MCZ, les ouvertures de ports et UPnP en lecture seule ; ne pas divulguer les adresses MAC.
- [ ] Tester, uniquement en presence d'un adulte et **en lecture seule**, si les etats restent consultables en mode direct lorsque l'acces Internet du telephone est desactive ; ne pas toucher a l'alimentation ni aux commandes de chauffage.
- [ ] A terme, examiner sur un reseau de test autorise si le firmware exige une autorisation applicative en plus de l'acces Wi-Fi ; aucune commande physique pendant ce test.
- [ ] Apres validation du mode direct, envisager un cloisonnement du poele et/ou un blocage de son trafic Internet ; documenter les fonctions perdues et la procedure de retour arriere.

## Sources

- [S12/S13 - MaestroGateway](https://github.com/Chibald/maestrogateway) : protocole local et exemple de configuration MQTT.
- [S14 - client WebSocket Home Assistant](https://github.com/roondar/ha-mcz-maestro/blob/main/custom_components/mcz_maestro/api.py) : connexion `ws://`, sans credentiel applicatif dans le client.
- [S29 - MCZ Maestro Upgrade](https://play.google.com/store/apps/details?id=it.mcz.maestro.one) : commande Internet ou Wi-Fi Direct.
- [S30 - Migration des comptes](https://mcz.dk/service/mcz-driftsstatus/) : compte et association distante.
- [S32 - documentation de l'ancienne famille DOC Comfort Air](https://www.scribd.com/document/760360651/Mode-d-Emploi-MCZ-DOC-Confort-Air) : modes DIRECT/REMOTE, mot de passe local et identifiants.
- [S34 - integration Gladys MCZ](https://gladysassistant.com/docs/integrations/external/mcz-maestro/) : commandes depuis le cloud et canal WebSocket local distinct.

[Registre complet des sources](../SOURCES.md)
