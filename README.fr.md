# Luma Home — Tableau de bord multilingue pour Home Assistant

[English](README.md) | [Français](README.fr.md) | [Italiano](README.it.md)

Version dérivée non officielle d’Aurora Glass v3, adaptée par Fonkyup avec une interface en français, en anglais et en italien.

> Convention actuelle : le type de carte est `custom:luma-home-card`. Le fichier JavaScript conserve le nom `aurora-v3.js`. Pour l’installation manuelle décrite ci-dessous, les fichiers sont placés dans `www/luma-home/`. Le dossier source du dépôt reste `luma-home/www/aurora-v3/` : copiez son contenu vers le dossier d’installation, sans supposer que leurs noms doivent être identiques.

![Interface héritée d’Aurora Glass v3, projet d’origine](docs/dashboard-casa-notte-intera.webp)

Une carte personnalisée qui transforme le tableau de bord de Home Assistant en une scène vivante : le ciel, le soleil, la lune et les fenêtres de la petite maison suivent l’heure réelle. Dix univers animés, onze effets météo, des boutons composés d’images et de GIF, une alarme, le contrôle du climat, des caméras et une vue Énergie calculant les coûts selon votre tarif.

## Origine et contributions

Cette version repose sur Aurora Glass v3, créé par DomotikPro.it (Luca Pinelli).

Mention originale conservée : © 2026 DomotikPro.it (Luca Pinelli).

Adaptation et traductions : Fonkyup.

Les contributions comprennent :
- l’ajout des traductions française et anglaise de l’interface ;
- l’adaptation des textes et messages dynamiques ;
- la traduction des guides d’installation et des exemples de configuration ;
- l’adoption du nom public Luma Home et du type `custom:luma-home-card` ;
- la documentation de la structure d’installation manuelle.

Documentation mise à jour le 26 octobre 2026. Les dates de modification figurent également dans les notices des fichiers source et dans l’historique du dépôt.

L’italien du projet original est conservé. Cette version n’est ni une publication officielle ni une version présentée comme approuvée par DomotikPro.it ou Luca Pinelli.

Les captures ci-dessous proviennent du projet d’origine ; elles ne constituent pas une validation visuelle de toutes les traductions.

| Tablette | Énergie | Téléphone |
|---|---|---|
| ![Tablette](docs/tablet-casa-tramonto.webp) | ![Énergie](docs/energia-vista.webp) | ![Téléphone](docs/mobile-casa-notte-sm.webp) |

## Ressources du projet original

Ces liens concernent Aurora Glass v3, pas nécessairement la version traduite :
- Démonstration originale, en italien : https://domotikpro.it/aurora-glass-v3-demo/index.html
- Guide illustré original, en italien : https://domotikpro.it/progetti/aurora-glass-v3
- Vidéos de l’auteur original, en italien : https://www.youtube.com/@domotikproit
- Dépôt original : https://github.com/lucalux00/aurora-glass-v3

## Fonctionnalités

Fonctionnalités héritées du projet original :
- 10 univers animés et 11 effets météo : pluie, neige, orage, lucioles, pétales, feux d’artifice…
- Ciel suivant l’heure réelle.
- 50 images et GIF prêts à utiliser pour les boutons : éclairage, scènes, capteurs, alarme et climat.
- Panneau d’alarme, contrôle du climat et caméras.
- Vue Énergie : puissance, consommation en kWh d’aujourd’hui, d’hier, du mois et de l’année ; coût calculé par kWh × tarif.
- Carte distribuée sous la forme d’un fichier JavaScript, sans compilation nécessaire pour l’installation.

Ajout de cette version : sélection de la langue de l’interface par `language: fr`, `language: en` ou `language: it`.

## Confidentialité et connexions

Selon la documentation originale, la carte fonctionne localement et charge les polices Google Fonts Manrope et Sora par une requête externe. L’auteur indique qu’aucune donnée n’est collectée ni envoyée par la carte.

Cette description n’est pas un audit de sécurité ou du trafic réseau. Les intégrations Home Assistant utilisées pour vos appareils peuvent avoir leurs propres connexions externes.

## Guides et exemples

Guides courts :
- [Français](luma-home/LISEZMOI.fr.txt)
- [English](luma-home/README.en.txt)
- [Italiano](luma-home/LEGGIMI.txt)

Exemples en français :
- [Tableau de bord complet](luma-home/dashboard-example.fr.yaml)
- [Options détaillées de la carte](luma-home/card-example.fr.yaml)
- [Compteurs d’énergie facultatifs](luma-home/aurora-energia.fr.yaml)

Les exemples doivent utiliser `custom:luma-home-card`. Pour l’installation manuelle ci-dessous, leur chemin d’images doit être `/local/luma-home/btn/`.

## Installation manuelle

### 1. Copier les fichiers

Depuis le dossier `luma-home/www/aurora-v3/` du dépôt, copiez le fichier `aurora-v3.js` et le dossier complet `btn` dans un dossier nommé `luma-home`, à l’intérieur du dossier `www` de votre configuration Home Assistant.

Vous devez obtenir :

```text
www/
└── luma-home/
    ├── aurora-v3.js
    └── btn/
        └── images et GIF des boutons
```

Le chemin source et le chemin de destination sont volontairement différents :

```text
Source dans le dépôt :
luma-home/www/aurora-v3/aurora-v3.js

Destination dans Home Assistant :
www/luma-home/aurora-v3.js
```

Utilisez le JavaScript et les images de la même version. Le dossier `dist` contient la copie de distribution ; ne mélangez pas des fichiers provenant de révisions différentes.

Si vous venez de créer le dossier `www`, redémarrez Home Assistant une fois.

Ouvrez cette adresse dans votre navigateur :

```text
<adresse de Home Assistant>/local/luma-home/aurora-v3.js
```

Du texte JavaScript doit s’afficher.

### 2. Ajouter ou modifier la ressource

Dans votre profil, activez le Mode avancé.

Paramètres → Tableaux de bord → menu ⋮ → Ressources :

- URL : `/local/luma-home/aurora-v3.js?v=1`
- Type : Module JavaScript.

Si la ressource existe déjà, modifiez-la au lieu d’en ajouter une deuxième.

Augmentez le nombre après `?v=` lors des mises à jour, puis rechargez complètement le navigateur. Évitez de charger plusieurs versions de la même carte.

### 3. Créer le tableau de bord

Paramètres → Tableaux de bord → Ajouter un tableau de bord → Nouveau tableau de bord à partir de zéro.

Titre suggéré : `Luma Home`.

### 4. Coller la configuration du tableau de bord

Ouvrez le tableau de bord → crayon → menu ⋮ → Éditeur de configuration brute.

Sur un nouveau tableau de bord, collez le contenu de l’[exemple français de tableau de bord](luma-home/dashboard-example.fr.yaml), puis enregistrez.

Sauvegardez la configuration avant de remplacer celle d’un tableau de bord existant.

L’exemple détaillé de carte décrit une seule carte, pas un tableau de bord complet. Ne le collez pas directement à la racine de la configuration du tableau de bord.

Les lumières peuvent rester grisées tant que vos entités ne sont pas renseignées.

### 5. Choisir la langue et associer les entités

La configuration minimale de la carte pour cette installation manuelle est :

```yaml
type: custom:luma-home-card
language: fr
assets: /local/luma-home/btn/
```

Valeurs possibles pour `language` :
- `fr` : français ;
- `en` : anglais ;
- `it` : italien.

Sans option de langue, le code actuel utilise l’italien.

Outils de développement → États : retrouvez vos identifiants d’entités.

Ajoutez `entities` au même niveau que `type`, `language` et `assets` :

```yaml
type: custom:luma-home-card
language: fr
assets: /local/luma-home/btn/

entities:
  lights:
    salotto: light.salotto
```

Remplacez `light.salotto` par votre véritable entité. Conservez les clés techniques comme `salotto`, `cucina` et `ingresso` : la traduction de l’interface ne renomme pas ces clés.

Consultez l’[exemple détaillé de carte](luma-home/card-example.fr.yaml) pour les autres options.

### 6. Configurer l’énergie — facultatif

Configurez votre capteur de puissance en watts dans `entities.energy.power` :

```yaml
type: custom:luma-home-card
language: fr
assets: /local/luma-home/btn/

entities:
  energy:
    power: sensor.potenza_casa
```

Remplacez `sensor.potenza_casa` par votre capteur. Fusionnez ce bloc avec votre section `entities` existante, sans créer une deuxième section du même nom.

Pour les compteurs en kWh, consultez la [configuration énergie en français](luma-home/aurora-energia.fr.yaml).

Utilisez une seule variante linguistique du fichier énergie : italienne, française ou anglaise. Elles définissent les mêmes compteurs et ne doivent pas être installées ensemble.

Remplacez le capteur d’exemple par votre capteur d’énergie cumulée en kWh, et non par un capteur de puissance en watts. Conservez les identifiants des compteurs, sauf si vous adaptez également toutes leurs références.

Vérifiez la configuration Home Assistant avant de redémarrer.

Dans la vue Énergie, renseignez votre prix par kWh. Les coûts affichés sont des estimations calculées à partir des consommations et du tarif configurés.

Diviser une facture entière par les kWh donne un coût moyen pouvant inclure des frais fixes ; ce n’est pas nécessairement le tarif variable réel.

## Migration d’une installation existante

Avant de quitter l’ancienne structure d’installation :

1. Sauvegardez le JavaScript fonctionnel et la configuration YAML.
2. Copiez le JavaScript et les images dans `www/luma-home/`.
3. Modifiez la ressource existante vers `/local/luma-home/aurora-v3.js?v=…`.
4. Utilisez le type `custom:luma-home-card`.
5. Définissez `assets: /local/luma-home/btn/`.
6. Rechargez le navigateur et testez les images, les langues et les commandes.
7. Ne supprimez l’ancienne ressource ou l’ancien dossier que lorsqu’ils ne sont plus utilisés ailleurs.

Renommer un dossier dans le dépôt GitHub ne déplace pas les fichiers dans Home Assistant.

Ne renommez pas les identifiants des capteurs d’énergie ni les clés de stockage du navigateur pendant cette migration de chemins.

## HACS

La procédure HACS du projet original utilise `lucalux00/aurora-glass-v3`. Elle installe le projet original, pas cette adaptation.

Le workflow de validation HACS a réussi pendant le développement. Cette réussite ne publie pas automatiquement le projet dans le catalogue HACS et ne valide pas tous les scénarios d’installation.

Un test complet d’installation et de mise à jour par HACS reste un contrôle distinct à effectuer avant publication.

Les chemins `/local/luma-home/` ci-dessus concernent l’installation manuelle. Pour HACS, utilisez les chemins des fichiers réellement installés ; ne remplacez pas automatiquement les URL `/hacsfiles/` par celles de l’installation manuelle.

Le JavaScript distribué est `dist/aurora-v3.js`. Le champ `filename` de `hacs.json` reste `aurora-v3.js` tant que ce nom de fichier est conservé.

## Dépannage

- « Custom element doesn't exist » : vérifiez le JavaScript chargé, l’URL de la ressource et le type `custom:luma-home-card`, puis rechargez complètement la page.
- Images absentes : pour l’installation manuelle décrite ici, vérifiez `assets: /local/luma-home/btn/`, avec la barre finale, et la présence des images dans `www/luma-home/btn/`.
- Lumières grisées : vérifiez l’identifiant et la disponibilité de l’entité.
- Coûts à zéro : définissez le tarif et vérifiez les capteurs de consommation.
- Langue incorrecte : vérifiez `language: fr`, `language: en` ou `language: it`, ainsi que la version du JavaScript réellement chargée.
- Textes anciens après mise à jour : augmentez le paramètre `?v=` de la ressource et rechargez le navigateur.

## Désinstallation

Supprimez le tableau de bord concerné, sa ressource si elle n’est pas utilisée ailleurs, puis le dossier `www/luma-home` si aucune autre installation ne l’utilise.

Ces étapes ne suppriment pas automatiquement les préférences du navigateur ni les capteurs d’énergie configurés séparément.

Pour une installation HACS, utilisez la procédure de suppression correspondante et vérifiez qu’aucun autre tableau de bord n’a encore besoin des fichiers.

## État et limites

L’interface française et anglaise a été vérifiée visuellement par le mainteneur. Tous les messages rares et tous les parcours ne sont pas nécessairement validés.

Les contrôles automatisés portent sur les exigences HACS, la syntaxe JavaScript et l’identité entre le fichier de référence et la distribution aux révisions contrôlées. Ils ne remplacent pas les tests fonctionnels de l’installation finale. Toute modification des URL de ressources, des chemins d’installation ou du type de carte nécessite un nouveau test.

Le README d’origine indique qu’Aurora Glass v3 a été testé par son auteur sur Home Assistant 2026.9. Cette indication ne constitue pas une certification de cette version dérivée.

Pour un signalement sur cette adaptation, ouvrez une issue dans le dépôt où cette version est publiée, en précisant la langue, la version chargée et les étapes de reproduction.

## Licence et attribution

Le logiciel dérivé est distribué sous [GNU GPL version 3](LICENSE).

Vous pouvez utiliser, étudier, modifier et redistribuer le logiciel, y compris à des fins commerciales, sous réserve des conditions de la licence. Les versions dérivées distribuées doivent notamment conserver les notices applicables, identifier les modifications et leur date, et respecter les obligations de licence et de fourniture du code source correspondant.

Mention originale conservée : © 2026 DomotikPro.it (Luca Pinelli).

Les contributions de Fonkyup ne remplacent pas les droits et les crédits du projet d’origine. Les éventuelles conditions propres aux composants tiers restent applicables.

Le nom Aurora Glass et la marque DomotikPro.it sont cités pour identifier le projet d’origine. Aucun droit de marque ni aucune approbation n’est revendiqué. Le nom public de cette version dérivée est Luma Home.

Le logiciel est fourni sans garantie, dans les limites de la licence et du droit applicable. Le texte intégral de LICENSE fait référence ; cette section n’en est qu’un résumé.

Le texte du fichier LICENSE doit être conservé sans modification. Les notices de projet et de contribution figurent dans la documentation et les fichiers source, pas à l’intérieur du texte de la GPL.

---

Projet d’origine : [DomotikPro.it](https://domotikpro.it) — Luca Pinelli.

Adaptation multilingue non officielle : Fonkyup.
