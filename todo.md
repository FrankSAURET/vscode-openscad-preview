# À faire

1. ⬜ Tester l'aperçu en français sur un vrai fichier `.scad` (bulles, bouton Prévisualiser clic / Ctrl+clic, préréglage fixe).

# v2026.10.0.3

1. ✅ Premier calcul forcé à l'ouverture de l'aperçu, même hors mode automatique (`ScadSession.hasRendered`).

# v2026.10.0.2

1. ✅ Onglet Paramètres : préréglage hors zone de défilement (`.preset` fixe, `.groups` défile, boutons Imprimer/Exporter fixes en bas).
2. ✅ Bouton Prévisualiser : aperçu automatique coupé par défaut ; clic = `renderNow` (nouveau message), Ctrl/Cmd+clic = verrouillage (`setAutoRender`), état `latched` gris dans `IconButton`.
3. ✅ Bandeaux d'aperçu : `preview.idle` (rien calculé), `preview.pending` (modifications en attente) ; clés `preview.paused*` retirées.

# v2026.10.0.1

1. ✅ Fork de thijsdaniels/vscode-openscad-preview vers FrankSAURET/vscode-openscad-preview.
2. ✅ Internationalisation côté extension : `l10n.t()`, `l10n/bundle.l10n.fr.json`, `package.nls.json` / `package.nls.fr.json`.
3. ✅ Internationalisation de la vue web : dictionnaire `src/webview/i18n/` (`en.ts`, `fr.ts`, `t.ts`), langue lue dans `<html lang>`.
4. ✅ Bulle d'aide (`title`) sur chaque contrôle : barre d'outils, options, onglets, paramètres, arbre de scène, propriétés, environnement, sortie.
5. ✅ Bouton « Aperçu automatique » (pause/reprise du rendu) : `ScadSession.setAutoRender`, messages `setAutoRender` / `autoRender`, bandeau en pause.
6. ✅ Manifeste : identifiant `electropol-fr.openscad-preview-fr`, version `2026.10.0`, `buildNumber` 1.
7. ⏳ Autres langues (ES, ZH…) : à faire juste avant une publication, sur demande.
