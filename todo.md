# À faire

1. ✅ Tester l'aperçu en français sur un vrai fichier `.scad` (bulles, bouton Prévisualiser clic / Ctrl+clic, préréglage fixe).

# v2026.10.0.8

1. ✅ Icône Enregistrer : retour au dessin codicon `save`, peint en dégradé bleu + reflet (table `codicons` du générateur, source `@vscode/codicons/src/icons`).
2. ✅ Outil Déplacer : retour à l'ancienne quadruple flèche, en vert à reflet (`glossyPath` dans `drawnIcons.ts`).
3. ℹ️ Les fichiers de ces deux icônes sont partis dans l'enregistrement `dd5d97f` d'une session parallèle.

# v2026.10.0.7

1. ✅ Moteur de calcul : réglage `openscad.renderBackend` (`auto` | `manifold` | `cgal`). `auto` sonde `openscad --help` une fois par exécutable (`--backend` présent → Manifold), sinon CGAL + message dans la sortie.
2. ✅ Détection Windows : `OpenSCAD (Nightly)` passe avant `OpenSCAD` (les deux peuvent coexister).
3. ℹ️ OpenSCAD installé sur le poste : 2021.01 (CGAL seul). Gain réel seulement après installation d'une nightly.

# v2026.10.0.6

1. ✅ Icônes couleur à relief : `atoms/icons/` (`iconPalette.ts`, `drawnIcons.ts` isométriques, `fluentIcons.generated.ts`), `Icon.ts` les rend via `unsafeSVG` + ombre portée.
2. ✅ Générateur `scripts/generate-icons.ts` (`npm run icons`) : Fluent « color » tel quel, Fluent « filled » + dégradé de palette + reflet ; écrit aussi `media/preview.svg` (bouton du titre d'éditeur). Dépendance de développement `@fluentui/svg-icons` (MIT).
3. ✅ Plus aucun codicon dans la vue web : `vscode-toolbar-button` / `vscode-icon` remplacés par `scad-icon-button` + `scad-icon` ; `IconButton` gagne `disabled` et désature l'icône en état verrouillé.
4. ✅ Lumières : teinte par variable CSS `--icon-tint` (jaune par défaut, couleur de la lumière dans la vue 3D, `LightRig`).
5. ✅ Œil barré (`eye-off`) pour un objet masqué.
6. ✅ Planche de contrôle : `npx tsx scripts/icon-sheet.ts <sortie.html>`.

# v2026.10.0.5

1. ✅ `ScadParser` : description = ligne `// texte` juste au-dessus de la déclaration (prioritaire sur le commentaire de fin de ligne) ; remise à zéro sur ligne vide, groupe ou autre instruction.
2. ✅ Groupes masqués : table `HIDDEN_GROUPS` (`hidden`, `masqué`, `masque`).
3. ✅ Tests `ScadParser.test.ts` mis à jour + nouveau cas ; vérifié sur `Ratelier fil.scad` (31 paramètres, tous avec description).

# v2026.10.0.4

1. ✅ Réglage `openscad.parameterLabel` (`name` | `description`), type partagé `ParameterLabelMode`, messages `parameterLabel` / `setParameterLabel`.
2. ✅ Bouton bascule dans la zone Préréglage ; écrit le réglage global, l'écouteur de configuration renvoie l'état à la vue web.
3. ✅ Mode `description` : libellé = commentaire au-dessus de la variable, sinon nom mis en forme ; bulle inchangée (description + nom de variable).

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
