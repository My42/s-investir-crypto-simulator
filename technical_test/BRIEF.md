# Test Technique — S'investir — Développeur IA

**Deadline : mercredi 1er juillet 2026 à 23h59**
**Rendu via :** https://tally.so/r/81E2lA

---

## Contexte

S'investir recrute un développeur IA pour une collaboration full remote longue durée.
Les missions réelles porteront sur des **outils internes, agents IA et automatisations**
(HubSpot, WooCommerce, Google Sheets, n8n…). Le simulateur est un exercice autonome
pour évaluer le niveau — pas un reflet des vraies missions.

---

## Mission

> Transposer le simulateur crypto de S'investir dans le design et les standards
> de leur suite d'outils, et livrer une démo fonctionnelle.

- **Source fonctionnelle (logique à reproduire) :** https://sinvestir.fr/simulateur-crypto-monnaie/
- **Design & standards cibles :** https://simulateurs.sinvestir.fr/

On reprend la **logique métier** du simulateur crypto et on l'habille aux couleurs
de `simulateurs.sinvestir.fr`, comme s'il intégrait nativement la suite.

---

## Livrables attendus

| # | Livrable | Priorité |
|---|----------|----------|
| 1 | **Démo en ligne fonctionnelle** (Vercel de préférence) | Obligatoire |
| 2 | **Fidélité visuelle** — couleurs, typo, composants de simulateurs.sinvestir.fr | Obligatoire |
| 3 | **Composant autonome et intégrable** — peu de dépendances, embarquable proprement | Obligatoire |
| 4 | **Responsive** — desktop et mobile | Obligatoire |
| 5 | **Code propre** + README minimal (lancer le projet, partis pris) | Obligatoire |
| 6 | Embeddable depuis sinvestir.fr (iframe/web component) | Bonus |
| 7 | Vidéo Loom ≤ 5 min de présentation | Bonus |

---

## Stack

**Libre** pour ce test. Stack interne S'investir :

- **Next.js** — front
- **Supabase** — BDD
- **Vercel** — déploiement
- **n8n** — automatisations
- **Claude Code** — IA
- Outils : HubSpot, WooCommerce, Google Sheets

Le rendu doit pouvoir s'intégrer dans cette infra — ou justifier brièvement un autre choix dans le README.

---

## Critères d'évaluation

1. Démo fonctionnelle (résultat concret et manipulable)
2. Fidélité au design de simulateurs.sinvestir.fr
3. Qualité & intégrabilité du code (compatibilité stack ou choix justifié)
4. Pertinence des suggestions d'amélioration

---

## Format de rendu (formulaire Tally)

- Lien démo en ligne (Vercel/Netlify — cliquable et fonctionnel)
- Lien repo Git (public ou accès lecture)
- Partis pris techniques + suggestions d'amélioration
- (Bonus) Vidéo Loom ≤ 5 min

---

## Plan d'attaque

### Phase 1 — Analyse (1h)

- [ ] Analyser le simulateur source : https://sinvestir.fr/simulateur-crypto-monnaie/
  - Inputs (montant, crypto, durée, fréquence, rendement…)
  - Logique de calcul (formules, scénarios)
  - Outputs affichés (graphique, tableau, résumé)
- [ ] Analyser le design cible : https://simulateurs.sinvestir.fr/
  - Palette de couleurs (CSS variables / tokens)
  - Typographie
  - Composants UI (inputs, sliders, cards, boutons, graphiques)
  - Layout général

### Phase 2 — Setup projet (30 min)

- [ ] Créer un projet Next.js (App Router) dans ce dossier
- [ ] Configurer Tailwind CSS avec les couleurs S'investir
- [ ] Configurer le déploiement Vercel

### Phase 3 — Développement (2-3h)

- [ ] Recoder la logique de calcul du simulateur crypto (TypeScript pur, testable)
- [ ] Construire le composant `<CryptoSimulator />` :
  - Formulaire avec les inputs du simulateur source
  - Graphique de projection (Recharts ou Chart.js)
  - Tableau/résumé des résultats
- [ ] Appliquer le design S'investir fidèlement
- [ ] Rendre le composant responsive

### Phase 4 — Intégrabilité (30 min)

- [ ] S'assurer que le composant est isolé (props only, pas de state global)
- [ ] Préparer une démo d'embedding simple (ex: `<script>` tag ou iframe fallback)
- [ ] (Bonus) Export web component

### Phase 5 — Finition & rendu (30 min)

- [ ] Écrire le README (lancer le projet, partis pris, justification stack)
- [ ] Déployer sur Vercel
- [ ] Préparer les suggestions d'amélioration pour le formulaire Tally
- [ ] (Bonus) Enregistrer la vidéo Loom
- [ ] Soumettre via https://tally.so/r/81E2lA

---

## Suggestions d'amélioration à préparer

À rédiger après avoir exploré simulateurs.sinvestir.fr — quelques idées à challenger :
- Comparateur multi-cryptos côte à côte
- Mode "objectif inversé" (combien investir pour atteindre X€ ?)
- Export PDF / partage de simulation
- Intégration des prix live via API CoinGecko
- Simulation avec DCA (Dollar Cost Averaging) personnalisable
