# 📦 Guide d'installation détaillé

Ce guide vous accompagne pas à pas pour installer le shortcode Canal-U sur votre site WordPress.

## Table des matières

1. [Prérequis](#prérequis)
2. [Installation de Code Snippets](#installation-de-code-snippets)
3. [Installation du shortcode](#installation-du-shortcode)
4. [Utilisation](#utilisation)
5. [Dépannage](#dépannage)

---

## Prérequis

### WordPress

- **Version minimale** : WordPress 5.0 ou supérieur
- **Accès administrateur** : Vous devez avoir les droits d'administration
- **PHP** : Version 7.0 ou supérieur (recommandé : 7.4+)

### Plugin obligatoire : Code Snippets

Le shortcode Canal-U nécessite le plugin **Code Snippets** pour fonctionner. Ce plugin est :
- ✅ **Gratuit** et open-source
- ✅ **Sûr** : Plus de 400 000 installations actives
- ✅ **Maintenu** : Mis à jour régulièrement
- ✅ **Compatible** : Fonctionne avec tous les thèmes WordPress

> **🤔 Pourquoi Code Snippets ?**
>
> Code Snippets permet d'ajouter du code PHP personnalisé dans WordPress sans modifier directement les fichiers du thème. Cela présente plusieurs avantages :
> - Votre code survit aux mises à jour du thème
> - Protection contre les erreurs PHP fatales
> - Activation/désactivation facile des snippets
> - Interface conviviale pour gérer votre code

---

## Installation de Code Snippets

### Méthode 1 : Depuis l'interface WordPress (Recommandée)

1. **Connectez-vous** à votre administration WordPress (`https://votre-site.com/wp-admin`)

2. **Accédez aux extensions** :
   ```
   Menu latéral → Extensions → Ajouter
   ```

3. **Recherchez le plugin** :
   - Dans la barre de recherche, tapez : `Code Snippets`
   - Le plugin à installer est celui par **Code Snippets Pro**
   - Logo : Un bloc de code bleu

4. **Installez et activez** :
   - Cliquez sur **Installer maintenant**
   - Attendez quelques secondes
   - Cliquez sur **Activer**

5. **Vérification** :
   - Un nouveau menu **Snippets** devrait apparaître dans le menu latéral

### Méthode 2 : Installation manuelle (Avancée)

1. Téléchargez Code Snippets depuis [WordPress.org](https://wordpress.org/plugins/code-snippets/)
2. Décompressez le fichier ZIP
3. Uploadez le dossier via FTP dans `/wp-content/plugins/`
4. Activez le plugin depuis l'interface WordPress

---

## Installation du shortcode

### Étape 1 : Télécharger le code

1. **Téléchargez** le fichier [`snippet-canalu`](snippet-canalu) depuis ce dépôt GitHub
2. **Ouvrez-le** avec un éditeur de texte (Notepad++, Sublime Text, VS Code, etc.)

### Étape 2 : Préparer le code

⚠️ **ACTION IMPORTANTE** :

Le fichier `snippet-canalu` commence par `<?php`. Cette ligne doit être **supprimée** avant de copier le code dans Code Snippets.

**AVANT** (ne copiez pas ceci) :
```php
<?php
/**
 * Shortcode Canal-U pour WordPress
 * Usage: [canalu chaine="drones-cap"]
 */
function canalu_shortcode($atts) {
```

**APRÈS** (copiez à partir de cette ligne) :
```php
/**
 * Shortcode Canal-U pour WordPress
 * Usage: [canalu chaine="drones-cap"]
 */
function canalu_shortcode($atts) {
```

> 💡 **Pourquoi ?** Code Snippets ajoute automatiquement `<?php` au début de chaque snippet. Si vous le laissez, vous aurez une erreur de syntaxe.

### Étape 3 : Créer le snippet dans WordPress

1. **Accédez à Code Snippets** :
   ```
   Menu latéral → Snippets → Add New
   ```

2. **Configurez le snippet** :

   - **Title (Titre)** : `Shortcode Canal-U`
   - **Code** : Collez le code préparé à l'étape 2 (sans le `<?php`)
   - **Description** (optionnel) : `Affiche les vidéos d'une chaîne Canal-U avec le shortcode [canalu]`

3. **Paramètres d'exécution** :

   Cochez une de ces options :
   - ✅ **"Run snippet everywhere"** (Recommandé) : Le shortcode fonctionnera partout
   - ⚪ **"Only run in site front-end"** : Le shortcode fonctionnera uniquement côté visiteur (pas dans l'admin)

4. **Enregistrer et activer** :
   - Cliquez sur le bouton **"Save Changes and Activate"**
   - Une notification verte devrait confirmer l'activation

5. **Vérification** :
   - Retournez dans `Snippets → All Snippets`
   - Votre snippet "Shortcode Canal-U" devrait être marqué comme **Active** ✅

---

## Utilisation

### Test rapide

1. **Créez une nouvelle page** ou **éditez une page existante**
2. **Ajoutez un bloc** (Gutenberg) ou passez en mode texte (éditeur classique)
3. **Insérez le shortcode** :
   ```
   [canalu chaine="drones-cap"]
   ```
4. **Publiez ou prévisualisez** la page
5. Vous devriez voir apparaître une grille de vidéos !

### Exemples d'utilisation

**Afficher toutes les vidéos (max 200)** :
```
[canalu chaine="drones-cap"]
```

**Limiter à 20 vidéos** :
```
[canalu chaine="drones-cap" limite="20"]
```

**Activer le mode debug** :
```
[canalu chaine="drones-cap" debug="true"]
```

**Nom de chaîne avec espaces** :
```
[canalu chaine="Drones Cap"]
```

---

## Dépannage

### "Aucune vidéo trouvée"

**Solutions** :

1. **Vérifiez le nom de la chaîne** :
   - Allez sur https://www.canal-u.tv/chaines/VOTRE-CHAINE
   - Copiez exactement le slug de l'URL
   - Exemple : pour `https://www.canal-u.tv/chaines/drones-cap`, utilisez `chaine="drones-cap"`

2. **Activez le mode debug** :
   ```
   [canalu chaine="drones-cap" debug="true"]
   ```
   Cela affichera des informations de diagnostic

3. **Videz le cache** :
   - Créez un nouveau snippet temporaire en mode "Run once"
   - Copiez le contenu du fichier `vider-cache-drones.php` (disponible sur demande)
   - Exécutez-le une fois, puis supprimez-le

### Erreur PHP

Si vous voyez un message d'erreur PHP :

1. **Vérifiez que vous avez bien supprimé le `<?php`** au début du code
2. **Vérifiez que le code est complet** : Le fichier fait environ 550 lignes
3. **Désactivez temporairement le snippet** pour restaurer votre site
4. Contactez-nous en ouvrant une [issue GitHub](https://github.com/sbonaime/canalu-wordpress/issues)

### Le cache ne se rafraîchit pas

Le cache est stocké pendant 1 heure. Pour le vider manuellement :

1. Créez un snippet en mode "Run once"
2. Utilisez ce code (remplacez `drones-cap` par votre chaîne) :
   ```php
   $transient_key = 'canalu_v2_' . md5('drones-cap');
   delete_transient($transient_key);
   echo 'Cache vidé !';
   ```

### Problème de mise en page

Si la grille ne s'affiche pas correctement :

1. **Vérifiez les conflits CSS** : Votre thème peut avoir des styles qui interfèrent
2. **Ajoutez du CSS personnalisé** dans `Apparence → Personnaliser → CSS additionnel`

---

## Support

- **Documentation complète** : [README.md](README.md)
- **Signaler un bug** : [GitHub Issues](https://github.com/sbonaime/canalu-wordpress/issues)
- **Proposer une amélioration** : [Pull Requests](https://github.com/sbonaime/canalu-wordpress/pulls)

---

## Licence

MIT License - Voir le fichier [LICENSE](LICENSE) pour plus de détails.
