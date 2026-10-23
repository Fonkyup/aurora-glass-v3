```markdown
# Aurora Glass v3 — Tableau de bord animé pour Home Assistant

🇬🇧 [Lire en anglais](README.md) · 🇮🇹 [Lire en italien](README.it.md)

![Aurora Glass v3](docs/dashboard-casa-notte-intera.webp)

Une seule carte personnalisée qui transforme le tableau de bord de Home Assistant en une scène vivante : le ciel, le soleil, la lune et les fenêtres de la petite maison suivent l’heure réelle. Dix univers animés, onze effets météo, des boutons utilisant des images et des GIF, une alarme, le contrôle de la climatisation et du chauffage, des caméras et un suivi de l’énergie avec les coûts en euros calculés selon votre tarif.

- Démonstration en ligne, sans rien installer : https://domotikpro.it/aurora-glass-v3-demo/index.html
- Guide complet avec captures d’écran : https://domotikpro.it/progetti/aurora-glass-v3
- Vidéos pas à pas : https://www.youtube.com/@domotikproit

| Tablette | Énergie | Téléphone |
|---|---|---|
| ![Tablette](docs/tablet-casa-tramonto.webp) | ![Énergie](docs/energia-vista.webp) | ![Téléphone](docs/mobile-casa-notte-sm.webp) |

## Fonctionnalités

- 10 univers animés et 11 effets météo : pluie, neige, orage, lucioles, pétales, feux…
- Un ciel qui suit l’heure réelle.
- 50 images et GIF prêts à utiliser pour les boutons : éclairage, scènes, capteurs, alarme et contrôle de la climatisation et du chauffage.
- Panneau d’alarme, contrôle de la climatisation et du chauffage, caméras.
- Vue Énergie : puissance, consommation en kWh pour aujourd’hui, hier, le mois et l’année, avec un coût calculé ainsi : kWh × votre tarif.
- Un seul fichier JavaScript, aucune compilation et aucun service cloud.
- **Confidentialité :** tout fonctionne localement. Les seules requêtes externes concernent les polices Google Fonts, Manrope et Sora. Aucune donnée n’est collectée ni transmise.

## Installation — environ 10 minutes

Les instructions commentées se trouvent dans [`aurora-glass-v3/LEGGIMI.txt`](aurora-glass-v3/LEGGIMI.txt).

Voici les étapes principales.

### Avec HACS

HACS copie la carte et les images, puis ajoute automatiquement la ressource.

HACS → ⋮ → Dépôts personnalisés → ajoutez `https://github.com/lucalux00/aurora-glass-v3`, de type Tableau de bord → recherchez Aurora Glass v3 → Télécharger → rechargez le navigateur, puis passez à l’étape 3.

Sans HACS, commencez par les étapes 1 et 2.

### Étapes d’installation

1. Copiez les fichiers.

   Placez le dossier `aurora-glass-v3/www/aurora-v3` dans le dossier `www` de Home Assistant à l’aide de File editor, Samba ou Studio Code Server.

   Vous devez obtenir :

   - `www/aurora-v3/aurora-v3.js`
   - `www/aurora-v3/btn/…`

   Dans l’application File editor, le dossier de configuration porte le nom `/homeassistant` : il s’agit du même dossier.

   Si vous venez de créer le dossier `www`, redémarrez Home Assistant une fois.

   Pour vérifier, ouvrez `/local/aurora-v3/aurora-v3.js` dans le navigateur de votre instance Home Assistant : si du texte s’affiche, les fichiers sont accessibles.

2. Ajoutez la ressource.

   Dans votre profil, activez le Mode avancé.

   Paramètres → Tableaux de bord → ⋮ → Ressources → Ajouter une ressource :

   - URL : `/local/aurora-v3/aurora-v3.js?v=1`
   - Type : Module JavaScript

   Lorsque vous mettez la carte à jour, augmentez le nombre après `?v=`.

3. Créez le tableau de bord.

   Paramètres → Tableaux de bord → Ajouter un tableau de bord → Nouveau tableau de bord à partir de zéro.

4. Collez la configuration du tableau de bord.

   Ouvrez le tableau de bord → icône de crayon → ⋮ → Éditeur de configuration brute.

   Supprimez le contenu existant, puis collez le contenu de [`dashboard-esempio.yaml`](aurora-glass-v3/dashboard-esempio.yaml) et enregistrez.

   Les lumières resteront grises tant que vous n’aurez pas indiqué vos propres entités.

5. Associez vos entités.

   Dans Outils de développement → États, recherchez les noms de vos entités, par exemple `light.` ou `binary_sensor.`.

   Ajoutez-les sous `entities:`, comme dans [`scheda-esempio.yaml`](aurora-glass-v3/scheda-esempio.yaml), qui présente toutes les options avec des commentaires.

6. Configurez l’énergie et le tarif — facultatif.

   Indiquez votre capteur de puissance, en watts, dans `energy.power`.

   Pour la consommation en kWh d’aujourd’hui, du mois et de l’année, utilisez [`aurora-energia.yaml`](aurora-glass-v3/aurora-energia.yaml).

   Dans la vue Énergie, appuyez sur la barre Tarif, puis saisissez le prix que vous payez pour un kWh.

   Vous pouvez aussi le calculer à partir de votre facture :

   Prix par kWh = montant total à payer ÷ consommation en kWh.

L’identifiant de la carte est `custom:aurora-v3-card`.

## Dépannage

- Carte rouge avec le message « Custom element doesn't exist » : vérifiez la ressource et rechargez la page avec Ctrl+F5.
- Images absentes : la valeur de `assets` doit être `/local/aurora-v3/btn/`, avec la barre oblique finale.
- Lumières grises : le nom de l’entité n’existe pas ou l’appareil est hors ligne.
- Coûts à zéro : appuyez sur la barre Tarif et définissez le prix par kWh.

## Désinstallation

Supprimez le tableau de bord, la ressource et le dossier `www/aurora-v3`.

Aucun autre élément n’est modifié.

## État du projet

Version 3, testée par l’auteur sur Home Assistant 2026.9.

Les signalements et les suggestions sont les bienvenus : ouvrez une issue.

## Licence

[GPL-3.0](LICENSE).

Vous pouvez utiliser, étudier, modifier et partager la carte, y compris à des fins commerciales, à condition que toute version modifiée que vous distribuez reste sous licence GPL-3.0, soit accompagnée de son code source et conserve la mention originale :

© 2026 DomotikPro.it (Luca Pinelli).

Le nom « Aurora Glass » et la marque DomotikPro.it ne sont pas couverts par la licence : une version modifiée doit utiliser un nom différent.

---

Réalisé par [DomotikPro.it](https://domotikpro.it) — des guides pratiques pour une maison connectée fiable.
```
