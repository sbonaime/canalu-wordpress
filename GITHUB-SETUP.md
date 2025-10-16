# 🚀 Instructions pour créer le dépôt GitHub

Votre projet est maintenant prêt à être publié sur GitHub ! Suivez ces étapes :

## Étape 1 : Créer le dépôt sur GitHub

1. **Allez sur GitHub** : https://github.com/new
2. **Remplissez les informations** :
   - **Repository name** : `canalu-wordpress`
   - **Description** : `🎬 Shortcode WordPress pour afficher les vidéos d'une chaîne Canal-U dans une grille responsive`
   - **Visibilité** : 
     - ✅ **Public** (recommandé pour un projet open-source)
     - ⚪ Private (si vous préférez)
   - **Important** : Ne cochez PAS les options suivantes :
     - ❌ Add a README file
     - ❌ Add .gitignore
     - ❌ Choose a license
     
     *(Ces fichiers existent déjà dans votre projet)*

3. **Cliquez sur** : `Create repository`

## Étape 2 : Pousser votre code sur GitHub

Une fois le dépôt créé, GitHub vous affichera des instructions. Utilisez la section **"push an existing repository from the command line"**.

**Dans votre terminal**, exécutez :

```bash
cd /Users/bonaime/nextcloud_CNRS/canalu-wordpress
git remote add origin https://github.com/sbonaime/canalu-wordpress.git
git push -u origin main
```

Si vous préférez utiliser SSH (recommandé) :

```bash
git remote add origin git@github.com:sbonaime/canalu-wordpress.git
git push -u origin main
```

## Étape 3 : Vérifier votre dépôt

1. Rechargez la page de votre dépôt : https://github.com/sbonaime/canalu-wordpress
2. Vous devriez voir :
   - ✅ Le fichier `README.md` affiché automatiquement
   - ✅ Les badges (License MIT, WordPress)
   - ✅ Tous vos fichiers : `snippet-canalu`, `INSTALL.md`, `LICENSE`

## Étape 4 : Configurer les topics (optionnel mais recommandé)

Sur la page de votre dépôt :

1. Cliquez sur **⚙️ à côté de "About"**
2. Ajoutez des **Topics** :
   - `wordpress`
   - `shortcode`
   - `canal-u`
   - `php`
   - `wordpress-plugin`
   - `code-snippets`
3. Cliquez sur **Save changes**

Cela rendra votre projet plus visible dans les recherches GitHub !

## 🎉 C'est terminé !

Votre projet est maintenant public sur GitHub et prêt à être utilisé par la communauté !

### Prochaines étapes possibles

- 📢 **Partagez votre projet** sur les réseaux sociaux ou forums WordPress
- 🐛 **Activez les Issues** pour que les utilisateurs puissent signaler des bugs
- 📝 **Ajoutez un CHANGELOG.md** pour suivre les versions
- 🏷️ **Créez un release** : `Releases` → `Create a new release` → Tag `v1.0.0`

---

## ❓ Aide

### Problème d'authentification GitHub

Si Git vous demande un mot de passe et que ça ne fonctionne pas :

1. **Utilisez un Personal Access Token** :
   - Allez sur : https://github.com/settings/tokens
   - Cliquez sur `Generate new token (classic)`
   - Donnez-lui un nom : `canalu-wordpress`
   - Cochez : `repo` (Full control of private repositories)
   - Générez et copiez le token
   - Utilisez ce token comme mot de passe lors du `git push`

2. **Ou configurez SSH** :
   - Suivez le guide : https://docs.github.com/en/authentication/connecting-to-github-with-ssh

### Besoin d'aide ?

Consultez la documentation GitHub : https://docs.github.com/en/get-started
