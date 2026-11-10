# Portfolio — Livio SANTIN

Portfolio professionnel de BUT Génie Mécanique et Productique (GMP), IUT de Troyes (URCA). Site bilingue français / anglais.

**Voir le site :** https://santinlivio9-hub.github.io/Portfolio-Santin/
**Version anglaise directe (à envoyer à un recruteur) :** https://santinlivio9-hub.github.io/Portfolio-Santin/?lang=en

## Organisation du dépôt

| Chemin | Contenu |
| --- | --- |
| `index.html` | Version actuelle (v2, 2e année), FR/EN : accueil, compétences, SAÉ par semestre, stage, engagements, contact. CSS et JS intégrés, non minifiés. |
| `v1/index.html` | Archive de la version 1 (1re année), en français uniquement |
| `404.html` | Page « introuvable » servie par GitHub Pages |
| `images/` | Visuels en WebP / SVG, partagés par les deux versions |
| `images/banniere.svg` | Bannière d'accueil (plan technique original, SVG) |
| `images/sae22.svg` | Illustration de la SAÉ 2.2 (implantation de cellule robotisée, SVG original) |
| `images/og-image.jpg` | Image d'aperçu pour le partage (LinkedIn, messageries) — 1200×630 |
| `documents/` | CV et comptes rendus de SAÉ en PDF (en français) |
| `favicon.svg`, `apple-touch-icon.png` | Icônes du site |

Publication : GitHub Pages, branche `main`, dossier racine.

## Langue (FR / EN)

- Ordre de priorité : paramètre `?lang=en` ou `?lang=fr` dans l'URL, puis choix mémorisé (`localStorage`, clé `livio-lang`), sinon français.
- **Textes fixes de la page** : chaque élément traduit porte `data-i18n="cle"` (son contenu HTML) ou `data-i18n-attr="alt:cle"` (attributs `alt`, `aria-label`, `title`, `href`).
  Le français est lu directement dans le HTML : pour modifier un texte français, il suffit de modifier le HTML.
  La traduction anglaise se trouve dans le dictionnaire `I18N.en` du script (section « A bis. TRADUCTIONS »).
- **Ajouter un texte traduit** : mettre `data-i18n="ma.cle"` sur l'élément, puis ajouter `'ma.cle': 'English text'` dans `I18N.en`.
- Les PDF restent en français ; la version anglaise l'indique (« in French »).

## Ajouter une SAÉ (et sa traduction)

Dans `index.html`, tableau `SAE_DATA` (section A du script) :

```js
{ id: "3.1", sem: "S3", img: "images/sae31.webp", pdf: "documents/sae31.pdf",
  title: "Titre en français",
  contexte: "Semestre 3 · Contexte court",
  org: "Groupe de 3 étudiants", solo: false, graded: true, note: "15/20",
  desc: "Description en français.",
  en: { title: "English title", contexte: "Semester 3 · Short context",
        org: "Group of 3 students", desc: "English description." } },
```

- `pdf: null` si le compte rendu n'est pas disponible : le bloc « Compte rendu (PDF) » n'est alors pas affiché.
- `feature: true` pour une carte « Projet phare » en pleine largeur.
- Images : WebP, 900 px de large (1600 px pour une carte phare), format 16:9 conseillé.
- Une SAÉ ajoutée à `v1/index.html` n'est pas nécessaire (archive).

## Réactiver les SAÉ du semestre 3

Les SAÉ 3.1, 3.2 et 3.3 sont dans `SAE_DATA` avec `upcoming: true, hidden: true`.
- Supprimer `hidden: true` pour réafficher la carte (avec la mention « à venir »).
- Une fois la SAÉ terminée : remplacer `title`, `contexte`, `org`, `desc` (et leur version `en`), supprimer `upcoming`, mettre `graded: true`, `note`, `img` et `pdf`.
- L'en-tête « Semestre 3 » réapparaît automatiquement dès qu'une carte du S3 est visible.

## Documents encore à fournir

- `documents/sae12.pdf` — SAÉ 1.2 (borne de recharge)
- `documents/sae22.pdf` — SAÉ 2.2 (cellule robotisée)
- `documents/sae24.pdf` — SAÉ 2.4 (chiffrage)

Après ajout, remplacer `pdf: null` par le chemin du fichier dans `SAE_DATA` (et dans `v1/index.html` si besoin).
Avant de déposer un PDF lourd, le compresser, par exemple avec Ghostscript :
`gswin64c -sDEVICE=pdfwrite -dPDFSETTINGS=/ebook -dNOPAUSE -dBATCH -sOutputFile=sortie.pdf entree.pdf`
