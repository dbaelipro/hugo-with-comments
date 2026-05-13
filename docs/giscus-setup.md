# Configuration Giscus — Guide pour l'administrateur

Ce document décrit les étapes manuelles à effectuer **une seule fois** pour activer les commentaires Giscus sur FlowCon France.

> ✅ **Les identifiants Giscus (`repoId` et `categoryId`) sont déjà configurés dans `hugo.toml`.** Les étapes ci-dessous concernent uniquement la configuration côté GitHub (Discussions, application Giscus) qui doit être faite par un administrateur du dépôt.

---

## Prérequis

- Être administrateur du dépôt `dbaelipro/hugo-with-comments`
- Avoir un compte GitHub

---

## Étapes

### 1. Activer GitHub Discussions

Dans le dépôt GitHub :

**Settings → General → Features → ✅ Discussions**

### 2. Installer l'application Giscus

Rendez-vous sur <https://github.com/apps/giscus> et cliquez sur **Install**.

Sélectionnez **Only select repositories** puis choisissez `hugo-with-comments`. Validez.

### 3. Vérifier la catégorie de discussion "Q&A"

La catégorie utilisée est la catégorie **Q&A** intégrée par défaut à GitHub Discussions — aucune création manuelle n'est nécessaire.

Vérifiez simplement qu'elle est bien présente dans l'onglet **Discussions** du dépôt.

### 4. Activer GitHub Pages (si pas déjà fait)

**Settings → Pages → Build and deployment → Source → GitHub Actions**

Ajouter ensuite le fichier `.github/workflows/deploy.yml` sur la branche (voir description de la PR).

---

## Résultat attendu

Une fois ces étapes effectuées et le site déployé, la section de commentaires Giscus apparaîtra en bas de la page `/manifesto/`. Les pages sans `comments: true` dans leur front matter n'afficheront aucun widget.

---

## Pages activées pour les commentaires

| Page | Front matter | Commentaires |
|---|---|---|
| `/manifesto/` | `comments: true` | ✅ Activés |
| `/about/` | `comments: false` | ❌ Désactivés |

Pour activer les commentaires sur `/about/`, modifier `content/about.md` :

```yaml
comments: true
```

---

## Modération

- **Masquer un commentaire** : Discussions → commentaire → *Hide* (choisir la raison)
- **Supprimer du spam** : *Edit → Delete*
- **Verrouiller un fil** : Discussion → *Lock conversation*
- **Bannir un utilisateur** : Settings → Moderation → Blocked users
- **Supprimer tous les commentaires d'une page** : supprimer la discussion correspondante dans la catégorie *Q&A* — le widget affichera "Soyez le premier à commenter" à la prochaine visite

## Sécurité

Giscus ne nécessite **aucun token ni secret**. Si un service vous demande un token pour afficher des commentaires, il ne s'agit pas de Giscus.
