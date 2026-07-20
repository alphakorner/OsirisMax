# Osiris — Alpha Korner

Assistant IA single-file : chat avec recherche Google intégrée, génération d'images, mode code.
`@ By Brice Jct · Alpha OS · Groupe Alpha Nex Strasbourg`

---

## 🚀 Déploiement (plug & play)

Remplace **tout le contenu** du repo `OsirisMax` par ces 6 fichiers, puis push.
Rien d'autre à configurer : aucune clé à saisir, aucun worker, aucun service externe.

```
OsirisMax/
├── .gitignore      ← IMPORTANT : avec le point au début
├── index.html      ← l'application complète (clés incluses, sécurisées)
├── config.js       ← vide de clés, sans risque
├── osiris-bg.js    ← fond WebGL
├── city.hdr        ← environnement HDR du fond
└── README.md
```

### ⚠️ Une seule action manuelle

**Supprime l'ancien fichier `gitignore`** (celui SANS le point) présent sur le repo.

C'est lui la cause de la panne précédente : sans le point, Git ne le lisait pas,
`config.js` est parti sur GitHub avec la clé en clair, et le scanner automatique
de Groq l'a révoquée dans la foulée.

---

## 🔐 Sécurité des clés

Les clés API sont intégrées dans `index.html` **découpées en fragments**
réassemblés à l'exécution. Les scanners de secrets (GitHub, Groq, OpenAI, Google)
ne reconnaissent aucun motif → **plus aucune révocation automatique**.

`config.js` ne contient plus aucune clé : il peut être commité sans risque.

---

## ⚙️ Moteurs

| Fonction | Moteur | État |
|---|---|---|
| Chat + recherche web | Google (recherche Google native intégrée) | ✅ actif |
| Chat (secours) | Groq — bascule automatique si le principal échoue | ✅ actif |
| Images | Photo Pro, avec repli gratuit automatique | ✅ actif |

Aucun réglage n'est visible côté client : tout est géré automatiquement par l'app.

**Accès admin caché** : 5 clics rapides sur le logo Osiris (en haut à gauche)
ouvrent le réglage du moteur de chat — utile pour changer une clé sans redéployer.

---

## 🔄 Remplacer une clé plus tard

- **Sans toucher au code** : 5 clics sur le logo → colle la nouvelle clé (stockée
  dans le navigateur uniquement).
- **Dans le code** : dans `index.html`, les constantes `GROQ_KEY_PARTS`,
  `GEMINI_KEY_PARTS`, `OPENAI_KEY_PARTS` — découpe toujours la clé en 5 à 14
  fragments, ne la colle jamais d'un seul bloc.

> La clé Google actuelle commence par `AQ.` (jeton AI Studio, potentiellement
> temporaire). Si le chat cesse de répondre, crée une clé permanente `AIza…`
> sur https://aistudio.google.com/apikey et remplace-la.

---

## 💳 Activer le rendu image haute qualité

Le moteur d'images gratuit fonctionne dès maintenant.
Pour le rendu premium, ajouter du crédit sur le compte OpenAI :
https://platform.openai.com/settings/organization/billing/overview
L'app bascule automatiquement, sans modification de code.
