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

## Protection immediate et raisonnable

1. **Preserver les donnees d'appairage hors publication** : photographie QR, mot de passe HOME / PWD, numero de serie, adresse MAC et justificatifs.
2. **Compte MCZ** : employer un mot de passe long, unique, non reutilise. Examiner dans Upgrade les utilisateurs autorises et retirer les acces inconnus. Verifier si une authentification multifacteur est proposee, sans la supposer disponible.
3. **Routeur** : utiliser le chiffrement Wi-Fi et la protection administration de la box, maintenir les mises a jour et verifier qu'aucune redirection de port ou ouverture UPnP ne rend une interface domotique accessible depuis Internet. Ceci **ne bloque pas le service cloud** : celui-ci peut utiliser des connexions sortantes.
4. **Ne pas ajouter de passerelle par defaut** : ni broker MQTT public, ni pont sans authentification, ni automatisation de mise en marche.
5. **Ne jamais couper brutalement l'alimentation d'un poele en fonctionnement** pour faire un test reseau ; respecter son cycle normal de refroidissement.

## Protocole de qualification sans modification

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
