# Configuration Giscus — Guide pour l'administrateur

Ce document décrit les étapes manuelles à effectuer **une seule fois** pour activer les commentaires Giscus sur FlowCon France.

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

### 3. Créer la catégorie de discussion "Site Comments"

Dans l'onglet **Discussions** du dépôt :

1. Cliquer sur **Categories** (colonne de gauche) → icône crayon
2. Cliquer sur **New category**
3. Nom : **`Site Comments`** (doit correspondre exactement à la valeur dans `hugo.toml`)
4. Type : **Announcement** — seuls les mainteneurs peuvent ouvrir des fils ; les visiteurs peuvent uniquement répondre (évite la pollution de la catégorie)
5. Valider

### 4. Générer les identifiants Giscus

Rendez-vous sur <https://giscus.app> et renseignez :

| Champ | Valeur |
|---|---|
| Repository | `dbaelipro/hugo-with-comments` |
| Page ↔ Discussion mapping | `pathname` |
| Category | `Site Comments` |
| Features | ✅ Enable reactions, ✅ Load lazily |
| Theme | `preferred_color_scheme` |
| Language | `fr` |

En bas de la page, Giscus génère un bloc `<script>`. Notez les deux valeurs :

- `data-repo-id` → c'est votre **`repoId`**
- `data-category-id` → c'est votre **`categoryId`**

Ces valeurs sont publiques (elles apparaissent dans le HTML rendu) — les commiter est la pratique documentée par Giscus.

### 5. Mettre à jour `hugo.toml`

Ouvrez `hugo.toml` et remplacez les valeurs dans le bloc `[params.giscus]` :

```toml
[params.giscus]
  repoId     = "REPLACE_WITH_REPO_ID"      # ← remplacer ici
  categoryId = "REPLACE_WITH_CATEGORY_ID"  # ← remplacer ici
```

Commitez et poussez sur `feature/hugo-site` (ou directement sur `main` après fusion) :

```bash
git add hugo.toml
git commit -m "chore: set Giscus repoId and categoryId"
git push
```

### 6. Activer GitHub Pages (si pas déjà fait)

**Settings → Pages → Build and deployment → Source → GitHub Actions**

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
- **Supprimer tous les commentaires d'une page** : supprimer la discussion correspondante dans la catégorie *Site Comments* — le widget affichera "Soyez le premier à commenter" à la prochaine visite

## Sécurité

Giscus ne nécessite **aucun token ni secret**. Si un service vous demande un token pour afficher des commentaires, il ne s'agit pas de Giscus.
