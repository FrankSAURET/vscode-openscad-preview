# À faire

# v2026.10.0.16

1. ✅ Réglage `openscad.enableLazyUnion` supprimé (package.json, nls EN/FR). Remplacé par un bouton bascule « Éclater » dans l'en-tête de l'arbre Scène (icône `explode` : trois cubes orange écartés).
2. ✅ État porté par `ScadSession` (`explode`, `setExplode` → `renderNow`, recalcul même aperçu libéré), mémorisé par fichier dans `workspaceState` (`openscad.explode.<uri>`, lu avant le premier rendu). Passé à `ScadClient.render` (`--enable lazy-union`), export et trancheur compris.
3. ✅ Messages `setExplode` / `explode`, `ModelContext.explode` + `toggleExplode`. Libellé et bulle FR/EN.

# v2026.10.0.15

1. ✅ Mesure : extrémités en flèches de cote. Widget `widgets/MeasureArrow.ts` (CSS2D, SVG tourné dans `onBeforeRender` d'après la projection des deux points, rapport d'aspect tiré de la caméra), partagé par `MeasurementRig` et l'aperçu de `MeasureTool`. Anneau creux pour le point survolé.
2. ✅ Accroche réelle : plus de seuil de 20 px, le point colle toujours au sommet / à l'arête le plus proche. Candidats = arêtes vives (`tools/MeshFeatures.ts`, `EdgesGeometry` à 0,5°, cache par géométrie) : diagonales des faces planes exclues. Recherche en espace local du maillage.
3. ✅ Lancer de rayon de la mesure : ignore les pièces masquées et les zones coupées (`isClippedAway` sorti de `Stage` dans `preview/isClippedAway.ts`, partagé).
4. ✅ Échap (hors champ de saisie) : retour à l'outil Sélection, quel que soit l'outil actif (`App.handleKeyDown`). Bulle Mesurer complétée FR/EN.
5. ✅ Test hors navigateur : cube → 12 arêtes, 8 sommets ; cylindre $fn=100 → 300 arêtes.

# v2026.10.0.14

1. ✅ Icône Mesurer redessinée (`drawnIcons.ts`, constante `ruler`) : règle orange, contour et graduations noirs, une graduation sur deux plus longue. Partagée par `tool-measure` et `measurement` ; retirées de la table `filled` du générateur.
2. ✅ Bouton engrenage en tête de la barre d'outils verticale (groupe à part, les autres descendent) : message `openSettings` → `Bridge.openSettings()` → `ModelContext.openSettings` → `workbench.action.openSettings` filtré sur `@ext:electropol-fr.openscad-preview-fr`. Libellé et bulle FR/EN.

# v2026.10.0.13

1. ✅ Pièces du modèle sélectionnables : nouveau rig `ModelPartRig` (contrat `Rig`), un par enfant du groupe 3MF (élément de construction) ou le maillage STL. Pivot au centre de la boîte englobante (gizmo Déplacer/Pivoter autour du centre), matériaux clonés par pièce (le chargeur 3MF les partage entre objets de même couleur).
2. ✅ `Stage` : `registerModelParts` / `clearModelParts` à chaque `loadModelData`. Id `model-part:<nom 3MF>` (`#n` si doublon) → sélection reprise si le nom existe encore, sinon effacée. Pose d'inspection gardée tant que les données sont identiques (rechargement sur changement d'option d'affichage), perdue au rendu suivant.
3. ✅ Clic : lancer de rayon commun scène + pièces, le plus proche gagne ; un point retiré par un plan de coupe (`clippingPlanes` du matériau) n'est pas un impact.
4. ✅ Mise en évidence : teinte émissive (accent × 0,35) + contour `EdgesGeometry` (30°) hors du groupe modèle (`outline`, ajouté à la scène), donc invisible pour la passe rayons X et les stencils ; découpé par les plans de coupe actifs.
5. ✅ `Rig.update()` appelé à chaque image pour tous les rigs (remplace l'appel réservé à `CrossSectionRig`). `CrossSectionRig` : les maillages de stencil suivent la matrice et la visibilité de leur maillage source (pièce masquée ou déplacée).
6. ✅ `sceneObjectMeta` : champs `fromModel` (pas de suppression, pas de sauvegarde dans la scène persistée) et `visibleTip`. `App.syncModelParts` place les pièces en tête de l'arbre et réapplique leur masquage.
7. ✅ Propriétés : section Pièce (nom, couleurs, triangles) via nouvel atome `ValueBox`, Dimensions, Inspection (position du centre, rotation). Icône `model-part` (cube orange isométrique).
8. ✅ Test hors navigateur du rig (pivot, dimensions, triangles, couleur, teinte isolée, contour, masquage, rotation) : OK.
9. ⏳ README (anglais) : documenter la sélection des pièces avant publication.

# v2026.10.0.12

1. ✅ Aperçu automatique figé par défaut (`ScadSession._autoRender = true`, état initial de la vue web aligné) ; bulle du bouton Prévisualiser complétée.
2. ℹ️ Pas mémorisé : chaque ouverture d'aperçu repart figé.

# v2026.10.0.11

1. ✅ Boutons Accordéon / Tout déplier / Tout replier déplacés dans l'en-tête « Paramètres » du panneau latéral (au-dessus du préréglage), avant les onglets, séparateur à droite.
2. ✅ État remonté dans `SidePanel` (survit au changement d'onglet), logique pure dans `services/GroupLayout.ts` (`free` = ouverture par défaut + groupes inversés, `accordion`). `Parameters` reçoit `.groupLayout` et émet `GroupLayoutChangeEvent`.

# v2026.10.0.10

1. ✅ Onglet Paramètres : boutons Accordéon (bascule), Tout déplier, Tout replier dans la barre du préréglage, après un séparateur. Barre qui passe à la ligne quand le panneau est étroit.
2. ✅ État `groupLayout` dans `Parameters` : `free` (ensemble des groupes repliés) ou `accordion` (groupe ouvert unique). Quitter l'accordéon garde le groupe ouvert.
3. ✅ `Collapsible` émet `CollapsibleToggleEvent` au clic sur l'en-tête ; les groupes sont pilotés par `.open`.
4. ✅ Icônes `accordion`, `expand-all`, `collapse-all` (Fluent filled).
5. ℹ️ Mode et état non mémorisés : la vue web recréée repart tout déplié.

# v2026.10.0.9

1. ✅ Réglage `openscad.defaultColor` (`format: color-hex`, défaut `#EDEAE0`, vide = `--vscode-editor-foreground`). Message `defaultColor` → variable CSS `--scad-default-color` sur `body` ; `Preview` observe aussi l'attribut `style` et recalcule le thème (`additive`).
2. ✅ Éditeurs de paramètres texte : type partagé `StringEditor` (`color` | `file` | `folder` | `font`), champs `editor` / `extensions` sur `StringParameter`.
3. ✅ Détection par table `StringEditorRules.ts` : indice `// [color]`, `// [file:svg,dxf]`… (FR accepté), sinon valeur (`#hex`, extension importable), sinon nom de variable. Liste de choix prioritaire. Test `ScadParser` ajouté (5/5).
4. ✅ Vue web : atomes `ColorField` (pastille `<input type=color>` + texte, noms CSS convertis en hex pour la pastille) et `PickField` (texte + bouton). Table `PICK_BUTTONS` dans `Parameters`.
5. ✅ Extension : message `pickParameterValue`, table `PARAMETER_PICKERS` (`ParameterPickers.ts`) : `showOpenDialog` fichier/dossier (chemin relatif au .scad, `/`), police en deux `showQuickPick` (famille puis style, syntaxe `Famille:style=Bold`). Familles via `SystemFonts.ts` (PowerShell `InstalledFontCollection` sous Windows, `fc-list` ailleurs, cache).
6. ✅ Icônes `file`, `folder`, `font` ajoutées au générateur.
7. ⏳ README (anglais) : documenter les indices `// [color]`… avant publication.

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
