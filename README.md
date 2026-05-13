# FlowCon France — Hugo Site

Site statique Hugo pour FlowCon France, déployé sur GitHub Pages avec le thème PaperMod.

## Développement local

```bash
# Cloner avec le sous-module du thème
git clone --recurse-submodules https://github.com/dbaelipro/hugo-with-comments.git
cd hugo-with-comments

# Lancer le serveur de développement
hugo server -D
```

## Déploiement

Le site est déployé automatiquement sur GitHub Pages à chaque push sur `main` via GitHub Actions.

**URL :** https://dbaelipro.github.io/hugo-with-comments/

## Structure

- `content/` — pages Markdown
- `layouts/partials/comments.html` — stub pour le futur système de commentaires
- `.github/workflows/deploy.yml` — pipeline CI/CD GitHub Pages *(à ajouter manuellement — voir description de la PR #1)*
- `themes/PaperMod/` — thème Git submodule
