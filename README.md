# 🎬 Canal-U WordPress Shortcode

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![WordPress](https://img.shields.io/badge/WordPress-5.0%2B-blue.svg)](https://wordpress.org/)

Un shortcode WordPress puissant pour afficher automatiquement les vidéos d'une chaîne [Canal-U](https://www.canal-u.tv/) dans une grille responsive sur votre site WordPress.

![Screenshot](https://via.placeholder.com/800x400/2563eb/ffffff?text=Canal-U+WordPress+Grid)

## 📋 Fonctionnalités

- ✅ **Grille responsive** : 1/2/3/4 colonnes selon la taille de l'écran
- ✅ **Scraping automatique** : Récupère toutes les vidéos avec pagination automatique
- ✅ **Extraction complète** : vignette, titre, auteurs, description, type, durée, date, niveau, documents
- ✅ **Gestion intelligente** : Supporte les espaces, majuscules et tirets dans les noms de chaîne
- ✅ **Cache WordPress** : Optimisé avec cache d'1 heure pour ne pas surcharger Canal-U
- ✅ **Mode debug** : Pour diagnostiquer facilement les problèmes
- ✅ **Mobile-friendly** : Interface adaptative pour tous les appareils
- ✅ **Personnalisable** : CSS entièrement personnalisable

## 🔧 Prérequis

Avant d'installer ce shortcode, assurez-vous d'avoir :

- **WordPress 5.0 ou supérieur**
- **Plugin Code Snippets** : Ce plugin est **obligatoire** pour faire fonctionner le shortcode
  - [Télécharger Code Snippets](https://wordpress.org/plugins/code-snippets/)
  - Le plugin permet d'ajouter du code PHP directement depuis l'interface WordPress sans modifier le fichier `functions.php`

> **💡 Pourquoi Code Snippets ?**
> Code Snippets est un plugin WordPress gratuit et sécurisé qui permet d'ajouter du code PHP personnalisé sans risquer de casser votre thème lors des mises à jour. Il gère aussi automatiquement les erreurs PHP pour protéger votre site.

## 🚀 Installation

### Étape 1 : Installer le plugin Code Snippets

1. Connectez-vous à votre administration WordPress
2. Allez dans **Extensions** → **Ajouter**
3. Recherchez **"Code Snippets"**
4. Cliquez sur **Installer** puis **Activer**

![Code Snippets Installation](https://via.placeholder.com/600x200/10b981/ffffff?text=Installer+Code+Snippets)

### Étape 2 : Télécharger le code du shortcode

1. Téléchargez le fichier [`snippet-canalu`](snippet-canalu) depuis ce dépôt
2. Ouvrez-le avec un éditeur de texte

### Étape 3 : Ajouter le snippet dans WordPress

1. Dans WordPress, allez dans **Snippets** → **Add New** (dans le menu latéral)
2. Donnez un nom à votre snippet : **"Shortcode Canal-U"**
3. **⚠️ IMPORTANT** : Copiez le contenu du fichier `snippet-canalu` **EN RETIRANT la toute première ligne `<?php`**
   - Le fichier contient `<?php` uniquement pour la coloration syntaxique
   - Code Snippets ajoute automatiquement cette balise
4. Dans les options du snippet :
   - Cochez **"Run snippet everywhere"**
   - Ou sélectionnez **"Only run in site front-end"** si vous voulez l'utiliser uniquement côté public
5. Cliquez sur **Save Changes and Activate**

![Ajouter le snippet](https://via.placeholder.com/600x300/3b82f6/ffffff?text=Copier+le+code+dans+Code+Snippets)

### Étape 4 : Vérification

Votre shortcode est maintenant actif ! Vous pouvez l'utiliser dans n'importe quelle page ou article WordPress.

## 📖 Utilisation

### Syntaxe basique

```
[canalu chaine="drones-cap"]
```

### Paramètres disponibles

| Paramètre | Description | Valeur par défaut | Exemple |
|-----------|-------------|-------------------|---------|
| `chaine` | Slug de la chaîne Canal-U (obligatoire) | - | `drones-cap` |
| `limite` | Nombre maximum de vidéos à afficher | 200 | `limite="50"` |
| `debug` | Active le mode debug | `false` | `debug="true"` |

### Exemples

```
[canalu chaine="drones-cap"]
[canalu chaine="drones-cap" limite="20"]
[canalu chaine="drones-cap" debug="true"]
[canalu chaine="Drones Cap"]
```

Le shortcode gère automatiquement les différentes variations du nom de chaîne (espaces, tirets, majuscules).

## 🔍 Mode Debug

Pour diagnostiquer les problèmes, utilisez le mode debug :

```
[canalu chaine="drones-cap" debug="true"]
```

Cela affichera :
- L'ID de la chaîne trouvé
- Les tentatives de slugs testées
- Le nombre de pages scrapées
- Le nombre de vidéos trouvées
- Les détails de la première vidéo
- Les informations de parsing (status HTTP, nombre de blocs trouvés, etc.)

## 🎨 Personnalisation CSS

Le shortcode génère du HTML avec des classes CSS que vous pouvez personnaliser :

```css
.canalu-wrapper { }          /* Conteneur principal */
.canalu-header { }           /* En-tête avec titre */
.canalu-grid { }             /* Grille de vidéos */
.canalu-video-card { }       /* Carte de vidéo */
.canalu-thumbnail { }        /* Vignette */
.canalu-title { }            /* Titre */
.canalu-auteurs { }          /* Auteurs */
.canalu-description { }      /* Description */
.canalu-badge-type { }       /* Badge type de production */
.canalu-badge-duree { }      /* Badge durée */
```

## 🐛 Dépannage

### "Aucune vidéo trouvée"

1. Activez le mode debug : `[canalu chaine="drones-cap" debug="true"]`
2. Vérifiez les informations affichées :
   - **slug_attempts** : les URLs testées et leurs codes HTTP
   - **rows_found** : nombre de blocs vidéo trouvés sur chaque page
   - Si `rows_found = 0`, regardez `html_excerpt` pour voir le contenu de la page

### Solutions courantes

- **Nom de chaîne incorrect** : Vérifiez l'URL de la chaîne sur canal-u.tv (ex: `/chaines/drones-cap`)
- **Structure HTML changée** : Canal-U peut avoir modifié sa structure HTML
- **Blocage par Canal-U** : Trop de requêtes peuvent être bloquées (le cache d'1h aide)

Pour plus de solutions, consultez le [Guide d'installation détaillé](INSTALL.md#dépannage).

## 🔧 Architecture technique

Le shortcode fonctionne en 3 étapes :

1. **Extraction de l'ID de chaîne**
   - Teste plusieurs variantes du slug (minuscules, tirets, espaces)
   - Scrape la page `/chaines/{slug}` pour trouver l'ID

2. **Scraping des pages de résultats**
   - Parcourt `/recherche?f[0]=chaine:{ID}&page=0,1,2...`
   - S'arrête quand il n'y a plus de résultats

3. **Extraction des données**
   - Parse chaque bloc `<article>` pour extraire les métadonnées
   - Gère les cas limites (vignette manquante, titre vide, etc.)

## 📝 Notes importantes

- **Cache** : Les résultats sont mis en cache pendant 1 heure pour éviter de surcharger Canal-U
- **Performance** : Le premier chargement peut prendre quelques secondes (scraping de toutes les pages)
- **Limitations** : Dépend de la structure HTML de Canal-U (peut nécessiter des mises à jour si le site change)
- **User-Agent** : Utilise un user-agent standard pour éviter d'être bloqué

## 🤝 Contribution

Les contributions sont les bienvenues ! N'hésitez pas à :
- 🐛 Signaler des bugs via les [Issues](https://github.com/sbonaime/canalu-wordpress/issues)
- 💡 Proposer des améliorations
- 🔧 Soumettre des Pull Requests

## 📚 Documentation

- **[Guide d'installation détaillé](INSTALL.md)** - Instructions pas à pas avec captures d'écran
- **[Code Snippets Plugin](https://wordpress.org/plugins/code-snippets/)** - Plugin WordPress requis

## 🆘 Support

Si vous rencontrez des problèmes :

1. ✅ Consultez le [Guide d'installation](INSTALL.md#dépannage)
2. ✅ Activez le mode debug : `[canalu chaine="votre-chaine" debug="true"]`
3. ✅ Vérifiez que Code Snippets est bien activé
4. ✅ Ouvrez une [Issue](https://github.com/sbonaime/canalu-wordpress/issues) si le problème persiste

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

## 👤 Auteur

**sbonaime**

- GitHub: [@sbonaime](https://github.com/sbonaime)

---

⭐ Si ce projet vous est utile, n'hésitez pas à lui donner une étoile sur GitHub !
