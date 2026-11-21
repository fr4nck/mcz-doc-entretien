# Releve des consignes de l'extracteur de fumees - 21 novembre 2026

[Accueil](../README.md) · [Dossier des reglages](07-reglages.md) · [Appareil](00-appareil.md)

**Poele :** MCZ DOC Comfort Air, code produit `7117008A`, etiquette `V: 00` (ce n'est pas une version firmware).
**Interface :** menu technique Maestro, rubrique `SPEED 'FAN SMOKE`.
**Nature du releve :** valeurs numeriques affichees dans des champs modifiables de l'application, **pas des mesures tachymetriques en temps reel, ni des reglages d'usine certifies**.
**Operation :** lecture de deux captures uniquement. L'assistant n'a envoye aucune commande et n'a modifie aucun parametre.

## Captures originales et confidentialite

Deux captures ont ete sauvegardees dans une [archive privee ChatGPT](https://chatgpt.com/space/page_ab43d120243c81918729216505e564ab) ; elles ne sont pas publiees sur ce depot GitHub public.
L'en-tete affiche un **surnom personnel de l'appareil**, volontairement non reproduit ici. Les captures n'affichent pas de code produit, de numero de serie ni de version firmware permettant de qualifier de facon autonome le profil d'usine.

- Capture 1 : SHA-256 `7b3618b269dec674af986f05c9d79fc7d7240b34c35490c0610c9e3035cb2c0c`
- Capture 2 : SHA-256 `93abf8f23beded30dfe46acdde977258a49491053d2ef983542263ea9a3584fe`

## Valeurs lues sur les captures

Ces valeurs sont relevees dans **l'ordre de l'application**, sans traduction des noms de champs dans la colonne de gauche. L'unite `tr/min` est documentee par la notice de la famille DOC pour les vitesses de l'extracteur [S44] ; le rapport entre consigne et regime reel reste a verifier.

| Libelle exact sur l'application | Valeur visible | Commentaire |
| --- | ---: | --- |
| `PHASE CLEAN FROID` | 2500 | Nettoyage a froid |
| `PHASE CLEAN CHAUD` | 2500 | Nettoyage a chaud |
| `PHASE LOAD FROID` | 1800 | Chargement a froid |
| `PHASE LOAD CHAUD` | 1800 | Chargement a chaud |
| `PHASE START 1 FROID` | 1800 | Allumage, 1re phase a froid |
| `PHASESTART 2 FROID` | 1800 | Allumage, 2e phase a froid |
| `PHASE START 1 CHAUD` | 1800 | Allumage, 1re phase a chaud |
| `PHASE START 2 CHAUD` | 1800 | Allumage, 2e phase a chaud |
| `PHASE STABILISATION` | 1700 | Stabilisation apres allumage |
| `PUISSANCE 1` | 1000 | Palier 1 |
| `PUISSANCE 2` | 1125 | Palier 2 |
| `PUISSANCE 3` | 1250 | Palier 3 |
| `PUISSANCE 4` | 1375 | Palier 4 |
| `PUISSANCE 5` | 1500 | Palier 5 |
| `PHASE EXTINCION` | 2000 | L'ecran affiche **EXTINCION** : extinction |
| `PHASE REFROIDISSEMENT` | 1000 | Refroidissement |
| `NETTOYAGE LOW` | 2300 | Nettoyage a regime plus bas |
| `NETTOYAGE HAUTE` | 2500 | Nettoyage a regime plus haut |
| `RANGE TRIAC MIN` | 10 | Unite non identifiee |
| `RANGE TRIAC MAX` | 115 | Unite non identifiee |
| `SEUIL TR/MIN NETT. MEC.` | **Aucune valeur visible** | Capture de l'ecran vide ; ne prouve ni zero, ni absence de reglage, ni defaut |

**Precision de transcription :** les captures montrent le libelle `PHASE EXTINCION` (sans T). L'etiquette `PHASESTART 2 FROID` ne comporte pas d'espace entre les deux premiers mots sur la capture.

## Ce que les valeurs permettent de conclure

1. Le menu concerne l'**extracteur de fumees**, et non les ventilateurs de convection Comfort Air. Les phases `CLEAN`, `LOAD`, `START`, `STABILISATION`, `PUISSANCE`, `EXTINCION`, `REFROIDISSEMENT` correspondent a des etapes distinctes de la regulation.
2. Pour P1-P5, la suite **1000, 1125, 1250, 1375, 1500** augmente de **125 par palier**. C'est une progression numeriquement reguliere. **Elle n'etablit ni l'origine constructeur ni la securite des consignes.**
3. `RANGE TRIAC MIN/MAX` suggere une plage de commande du composant electrique TRIAC ; il manque une documentation de cette carte pour en etablir la signification et les unites. **Ne pas assimiler 10/115 a des tr/min ou a des pourcentages sans preuve.**
4. Aucune valeur « usine » certifiee pour la combinaison exacte du DOC `7117008A`, de sa banque de donnees et de son firmware n'a ete retrouvee. Les tableaux MCZ d'autres poeles/generations ne sont pas des seuils applicables par transposition.
5. Les consignes affichees ne prouvent pas le **regime mesure en marche** ni la **depression effective** dans le circuit. Une mesure de tirage et une qualification de la combustion par un technicien sont necessaires avant un changement de vitesses [S44, S46].

## Contexte de maintenance du cas suivi

Le creuset etait tres encrasse de machefer avant le nettoyage photographie, puis les orifices ont ete majoritairement debouches. Des alarmes **A01/A02** ont ete rapportees lors d'une intervention precedente, de meme qu'une piece tombee du cote de l'arrivee des granules. **Aucun lien causal entre ces evenements et une consigne de vitesse particuliere n'est prouve.**

La notice de la famille DOC cite notamment les orifices bouches, la prise d'air, les joints, l'evacuation des fumees, l'etat du conduit et les granules comme causes possibles de dysfonctionnement [S44]. Le reglage de l'extracteur doit etre precede de la remise en etat et de la verification physique de l'installation.

**A ne pas faire :** appuyer sur `OK` dans les champs, modifier les vitesses P1-P5, `RANGE TRIAC`, l'activation du systeme ACTIVE, les protections ou la banque de donnees en l'absence de diagnostic et des donnees propres au DOC. Ne pas faire d'essai d'allumage alors que l'etat de la piece d'arrivee des granules est incertain.

## Releves complementaires utiles - lecture seule

- La **version firmware de la carte**, la version du Wi-Fi HOME et la revision de la banque de donnees (attention aux secrets affiches sur la meme page).
- Menu **INFO** : la vitesse **LIVE** du ventilateur, si releve possible lors d'un fonctionnement deja valide par un professionnel. Ne pas confondre avec la valeur `SET`.
- Existence et valeur de la recette AIR, recette PELLET, et statut **ACTIVE ON/OFF**, sans modification.
- Historique precis des alarmes A01/A02, entretien du circuit d'air et de fumees, nettoyage des echangeurs, et controle du montage de la piece tombee.
- Sur la base des valeurs constructeur propres au poele, mesure du tirage/depression par un professionnel competent, plutot que modification empirique des tr/min.

## Enjeux de securite logicielle

Ces captures prouvent qu'une **interface de modification individuelle des vitesses de l'extracteur est presente dans l'application** de cet exemplaire. Elles ne prouvent pas que ce menu est accessible a distance sans autorisation, ni qu'un attaquant pourrait imposer un changement. La securite de la liaison locale/cloud est documentee separement dans [l'audit](05-audit-cybersecurite.md).

Sources techniques : [S44, S46](../SOURCES.md#reglages-de-lancienne-generation-doc-comfort-air). Observation directe : les deux captures de l'utilisateur dans l'archive privee.
