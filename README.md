# Compagnon de wargame · Wargame Companion

**[English](#english) · [Français](#français)**

A Stream Deck plugin that runs the bookkeeping of a wargame played on a real table.
Un plugin Stream Deck qui tient la mécanique d'un wargame joué sur une vraie table.

---

## English

Wargame Companion turns a Stream Deck into a game assistant for physical wargames and board games. It tracks the turn sequence and scheduled events, rolls on combat tables, resolves dice-pool battles with automatic losses and retreat, keeps counters and a per-player clock, draws from random tables, undoes mistakes, and writes a timestamped game log that ends with a summary. Each game is a JSON file, edited in a visual editor or by hand.

The plugin follows the Stream Deck app's language: French for French, English for every other language.

### Requirements

- Stream Deck app 7.1 or later, on macOS 12+ or Windows 10+
- Any Stream Deck model; dials and touch strips are supported on Stream Deck + and + XL

### Quick start

1. Ready-made profiles are offered for each Stream Deck model; the actions are under **Wargame Companion**.
2. Open the settings of any key and pick *Classic wargame (example)*: it uses every feature.
3. Press **Turn sequence** to move through the phases, roll a **Battle** for each side, then press **Game** to open the log.
4. To create your own game: **Game** key settings → **Open the game editor**.

On first launch the plugin creates `Documents/Compagnon de wargame/` (the folder name is the same in every language):

| Folder | Contents |
|---|---|
| `jeux/` | Your games, the templates `_model.en.json` / `_modele.json`, and the format guides `_README.en.md` / `_LISEZMOI.md` |
| `journaux/` | One Markdown log per game |

### Actions

| Action | Press | Long press | Dial (Stream Deck +) |
|---|---|---|---|
| **Game** | Open the log | New game, with summary (hold 1.5 s) | |
| **Turn sequence** | Next phase | Previous phase | Scroll through phases |
| **Phase reminders** | Next reminder | Back to the first | |
| **Undo** | Undo the last action | | |
| **Player clock** | Pause / resume | Reset (hold 1.5 s) | Push: pause / resume |
| **Combat table** | Roll | Next odds column | Column; pushed: modifier |
| **Battle** | Roll the pool | New battle | Unit count; pushed: target or group |
| **Adjust (+/−)** | Apply +1 or −1 | Back to default | |
| **Random table** | Draw | Clear | Switch table |
| **Dice** | Roll | Clear | |
| **Counter** | +1 (or −1) | Opposite direction | ±1; pushed: ±10 |

**Adjust** gives keys-only Stream Decks what a dial does: one key per setting and direction (column, modifier, unit count, target or group).

### What the plugin does for you

- **Battles to the end.** With losses enabled in the game file, each round ends once both sides have rolled: hits are applied to both armies at once, weakest units first by default, then retreat or destruction is checked. The outcome and losses are logged.
- **Mixed armies.** A side can field several groups (dwarves at 4+, elves at 3+…); one press rolls them all, each at its own target, with dice tinted per group.
- **Scheduled events.** Reinforcements or rule changes planned for turn 5 show as a badge on the Sequence key and first on the Reminders key, and are logged once.
- **Rolling dice.** On Dice, Combat table, Battle and Random table keys, the chosen die (d4, d6, d8, d10, d12, d20, d100) spins for about half a second before the result shows; it can be switched off per key.
- **Undo.** Rolls, draws, phases, counters and battles can be undone; a quick burst on a dial undoes in one go. The undo is logged.
- **Player clock.** Follows whose phase it is, logs each turn's times and turns red past the game's limit.
- **Summary.** A new game first closes the old log with a summary: duration, dice luck per side (hits against expected hits), battles won, combat results, playing time, final counter values.
- **Tidy log.** A phase is logged only once it has stayed put for 2 seconds; a burst of counter presses makes one line.
- **Live files.** Saved changes to a game file reload immediately; a broken file is reported in the key settings with the exact cause. The game state is saved continuously.

### Game editor

The editor opens in your browser from the **Game** key settings. It edits every part of a game (sides, sequence, odds grid, battles with profiles and losses, random tables, counters, schedule, clock) and saves straight to your `jeux/` folder, with field names in English or French. It runs only on your computer (127.0.0.1) and every request carries a random token, so no website can read or write your files. `editeur/index.html` also works on its own, opened as a file: import and export instead of saving.

### Premium edition

**Wargame Companion Premium** is a separate plugin (`com.paul.compagnon-wargame-premium`) that contains everything above, plus:

| Feature | What it does |
|---|---|
| **Game screen** | A live page for a TV or tablet on the same network: turn, phase and active side, scheduled events, battles with drawn dice, combat results, counters, clock, cards, solo opponent, log. Scan the QR code on the **Game screen** key. Read-only; every request carries a random token. |
| **Odds calculation** | A combat table with `"odds"` computes the column from attack and defence strength (ratio or difference, rounding for the defender, the attacker or nearest, column shifts). Dial: attack, pushed: defence; Adjust keys in steps of 1 or 5. |
| **Solo opponent** | The automaton plays one or more sides: a posture drawn each turn and a priority list for each phase. The **Solo opponent** key shows the current priority; press if it is not possible, long press when the automaton does it. |
| **Card decks** | Draw without replacement, discard pile, automatic or manual reshuffle, reshuffle cards, hands per side (the game screen only shows how many cards each hand holds). |
| **Campaigns** | Named armies bound to a Battle key keep their losses and reinforcements from one battle, game and session to the next (`Documents/Compagnon de wargame/campagnes/`). |
| **Discord sharing** | Results, scheduled events and the summary posted to a Discord channel through a webhook, batched every few seconds, with mentions disabled. |
| **Illustrated report** | An HTML page with charts (dice luck per turn, battle losses, combat results, playing time, counters), written next to the log at every new game and printable to PDF. |
| **Sounds** | Dice, critical hit, victory, defeat, card, new turn, scheduled event; on the computer, on the game screen, or both. |
| **Key themes** | Night map room, Parchment, Military, Science fiction; chosen per game (`"theme"`) or forced in the Game key settings. |
| **Spreadsheet import** | In the game editor, paste cells from Excel, Numbers or Google Sheets (or open a CSV) to create an odds table or a random table; export any table to CSV. |

Three actions are added: **Card deck** (a deck, or one side's hand), **Solo opponent** and **Game screen**. Sounds, theme, Discord and the report are set in the **Game** key settings. To share on Discord, create a webhook in the channel settings (Integrations → Webhooks) and paste its address there; it is stored only in the plugin settings and never shown again. The game screen listens on port 8484 by default; it can be limited to this computer, and **New address** invalidates every link already shared.

Premium fields are documented in `jeux/_PREMIUM.en.md` / `jeux/_PREMIUM.md`; the full example is `example-premium.json` / `exemple-premium.json`. The free edition reads the same files and simply ignores Premium fields.

### Security

Game files are shared between players, so the plugin treats them, key settings and its own saved state as untrusted:

- **Game files** are limited in size (1 MB), depth, number of items and text length; every field is type-checked, dice and unit counts are capped, and colours must be `#rgb` or `#rrggbb` before they reach a key image.
- **Nothing outside its folders** is ever written: guides are never copied through a symbolic link, the log path from a saved game must sit in the logs folder, and files open without a shell.
- **The game editor** listens on 127.0.0.1 only, checks the Host header and a 128-bit token sent in a header; the token leaves the address bar once the page has loaded.
- **The game screen** (Premium) is read-only, checks the Host header against this computer's addresses (no DNS rebinding), requires a random token on every data request, and limits live connections per device.
- **Discord** (Premium): only Discord webhook addresses are accepted, redirects are refused, mentions and link previews are disabled, masked links and headings coming from game files are neutralised, and messages for an old address are dropped as soon as it changes.
- **An unexpected error is logged, never fatal**: one bad file or message can no longer stop every key.

### Game file format

See `jeux/_README.en.md` (English field names) or `jeux/_LISEZMOI.md` (French field names). Both spellings are accepted, even mixed.

```json
{
  "id": "my-game",
  "name": "My Game",
  "sides": ["Blue", "Red"],
  "sequence": { "start": ["Weather"], "perSide": ["Movement", "Combat"], "end": ["End of turn"] },
  "tables": {
    "melee": {
      "type": "pool", "name": "Melee", "target": 4, "sides": ["Attacker", "Defender"],
      "profiles": [{ "name": "Veterans", "target": 3, "dice": 2 }, { "name": "Militia", "target": 5, "dice": 4 }],
      "losses": { "perHit": 1, "order": "weakest", "retreat": { "losses": 50 } }
    }
  },
  "counters": { "vp": { "name": "Victory points", "perSide": true } },
  "schedule": [{ "turn": 5, "text": "The bridge is repaired" }]
}
```

### Development

```bash
npm install
npm run build         # compile both editions, then assemble the Premium plugin folder
npm test              # logic tests: dice, tables, battles, counters, undo, clock, summary, editor server
npm run test:premium  # odds, decks, solo, campaigns, game screen server, sounds, Discord, game screen page
npm run test:editeur  # game editor, in a real browser
npm run test:reglages # settings page of every action, both editions
npm run integration   # run both compiled plugins against a simulated Stream Deck app, in French then English, then the attack scenario
npm run apercu        # render key faces to PNG in apercu/
npm run pack          # validate and build both .streamDeckPlugin files in dist/
```

`EDITION=gratuit` or `EDITION=premium` in front of `rollup -c` builds one edition only. The free bundle contains no Premium code.

| Path | Role |
|---|---|
| `src/core/etat.ts` | Game state and every rule: sequence, battles, losses, counters, undo, clock, summary. No SDK dependency |
| `src/core/jeux.ts`, `alias.ts` | Game file format, validation with readable errors, English ↔ French field names |
| `src/core/rendu.ts` | SVG key faces (144 px) and touch-strip panels (200 × 100) |
| `src/core/langue.ts` | French / English texts |
| `src/editeur.ts` | Local server for the game editor |
| `src/actions/` | The eleven actions |
| `src/premium/` | Premium edition: odds, decks, solo opponent and campaigns (`partie.ts`), game screen server (`ecran.ts`), sounds, Discord, three extra actions |
| `premium/` | Premium files: game screen page, report template, sounds, profiles, example game, settings additions, data contract (`CONTRAT.md`) |
| `scripts/manifestes.mjs`, `premium.mjs` | Manifests of both editions; assembly of the Premium plugin folder |
| `com.paul.compagnon-wargame.sdPlugin/` | Manifest, `en.json` / `fr.json`, settings page, editor, profiles, bundled games |

Built with TypeScript, the official Elgato SDK (`@elgato/streamdeck` 3.x) and Rollup.

### Known limitations

- Tested with the official SDK and a simulated Stream Deck app, not yet on physical hardware. The bundled profiles in particular need checking in the real app.
- Above about fifteen dice, a pool is shown as a count per face.
- Updating the plugin never overwrites a game you already have in `jeux/`; delete your copy of a bundled game to get its new version.
- Premium: on Windows each sound starts a PowerShell process, so it can arrive a fraction of a second after the key; the generated sounds have not been listened to on real speakers yet. The game screen needs both devices on the same network, and the Windows firewall may ask to allow it on first start.

---

## Français

Compagnon de wargame transforme un Stream Deck en assistant de partie pour les wargames et jeux de plateau physiques. Il suit la séquence de tour et les événements programmés, lance sur les tables de combat, résout les batailles à poignées de dés avec pertes et retraite automatiques, tient des compteurs et un chrono par joueur, tire dans les tables aléatoires, annule les erreurs et écrit un journal horodaté qui se termine par un bilan. Chaque jeu est un fichier JSON, modifiable dans un éditeur visuel ou à la main.

Le plugin suit la langue de l'application Stream Deck : français pour le français, anglais pour toutes les autres langues.

### Prérequis

- Application Stream Deck 7.1 ou plus récente, sur macOS 12+ ou Windows 10+
- Tous les modèles ; molettes et écrans tactiles pris en charge sur Stream Deck + et + XL

### Démarrage rapide

1. Des profils prêts à l'emploi sont proposés pour chaque modèle ; les actions sont dans la catégorie **Compagnon de wargame**.
2. Ouvrez les réglages d'une touche et choisissez *Wargame classique (exemple)* : il utilise toutes les fonctions.
3. Appuyez sur **Séquence de tour** pour avancer, lancez une **Bataille** pour chaque camp, puis appuyez sur **Partie** pour ouvrir le journal.
4. Pour créer votre jeu : réglages de la touche **Partie** → **Ouvrir l'éditeur de jeu**.

Au premier lancement, le plugin crée `Documents/Compagnon de wargame/` :

| Dossier | Contenu |
|---|---|
| `jeux/` | Vos jeux, les modèles `_modele.json` / `_model.en.json` et les guides du format `_LISEZMOI.md` / `_README.en.md` |
| `journaux/` | Un journal Markdown par partie |

### Les actions

| Action | Appui | Appui long | Molette (Stream Deck +) |
|---|---|---|---|
| **Partie** | Ouvrir le journal | Nouvelle partie, avec bilan (1,5 s) | |
| **Séquence de tour** | Phase suivante | Phase précédente | Défiler les phases |
| **Rappels de phase** | Rappel suivant | Revenir au premier | |
| **Annuler** | Annuler la dernière action | | |
| **Chrono** | Pause / reprise | Remise à zéro (1,5 s) | Appui : pause / reprise |
| **Table de combat** | Lancer | Colonne suivante | Colonne ; enfoncée : modificateur |
| **Bataille** | Lancer la poignée | Nouvelle bataille | Effectif ; enfoncée : seuil ou groupe |
| **Ajuster (+/−)** | Appliquer +1 ou −1 | Valeur par défaut | |
| **Table aléatoire** | Tirer | Effacer | Changer de table |
| **Dés** | Lancer | Effacer | |
| **Compteur** | +1 (ou −1) | Sens inverse | ±1 ; enfoncée : ±10 |

**Ajuster** donne aux Stream Deck sans molette ce que fait une molette : une touche par réglage et par sens (colonne, modificateur, effectif, seuil ou groupe).

### Ce que le plugin fait pour vous

- **Batailles jusqu'au bout.** Si le fichier de jeu prévoit des pertes, chaque round se termine quand les deux camps ont lancé : les touches sont appliquées aux deux armées à la fois, des unités les plus faibles aux plus fortes par défaut, puis la retraite ou la destruction est vérifiée. L'issue et les pertes vont au journal.
- **Armées mixtes.** Un camp peut aligner plusieurs groupes (nains à 4+, elfes à 3+…) ; un seul appui les lance tous, chacun à son seuil, avec des dés teintés par groupe.
- **Événements programmés.** Renforts ou changements de règle prévus au tour 5 : pastille sur la touche Séquence, affichage en tête des rappels, une ligne au journal.
- **Dés qui tournent.** Sur les touches Dés, Table de combat, Bataille et Table aléatoire, le dé choisi (d4, d6, d8, d10, d12, d20, d100) tourne environ une demi-seconde avant d'afficher le résultat ; on peut le couper touche par touche.
- **Annulation.** Jets, tirages, phases, compteurs et batailles s'annulent ; une rafale à la molette s'annule d'un coup. L'annulation est notée au journal.
- **Chrono par joueur.** Il suit le joueur dont c'est la phase, note les temps de chaque tour et passe au rouge au-delà de la limite du jeu.
- **Bilan.** Une nouvelle partie clôt l'ancien journal par un bilan : durée, chance aux dés par camp (touches obtenues contre touches attendues), batailles gagnées, résultats de combat, temps de jeu, valeurs finales des compteurs.
- **Journal propre.** Une phase n'est notée qu'après 2 secondes sans changement ; une rafale de clics sur un compteur fait une seule ligne.
- **Fichiers vivants.** Un fichier de jeu enregistré est relu aussitôt ; un fichier en erreur est signalé dans les réglages avec sa cause exacte. L'état de la partie est sauvegardé en continu.

### Éditeur de jeu

L'éditeur s'ouvre dans votre navigateur depuis les réglages de la touche **Partie**. Il modifie toutes les parties d'un jeu (camps, séquence, grille de table, batailles avec profils et pertes, tables aléatoires, compteurs, programme, chrono) et enregistre directement dans le dossier `jeux/`, avec des noms de champs en français ou en anglais. Il ne tourne que sur votre ordinateur (127.0.0.1) et chaque requête porte un jeton aléatoire : aucun site web ne peut lire ni écrire vos fichiers. `editeur/index.html` fonctionne aussi seul, ouvert comme fichier : import et export au lieu de l'enregistrement.

### Édition Premium

**Compagnon de wargame Premium** est un plugin séparé (`com.paul.compagnon-wargame-premium`) qui contient tout ce qui précède, plus :

| Fonction | Ce qu'elle fait |
|---|---|
| **Écran de partie** | Une page en direct pour une télé ou une tablette du même réseau : tour, phase et camp actif, événements prévus, batailles avec les dés dessinés, résultats de combat, compteurs, chrono, cartes, adversaire solo, journal. On scanne le QR code de la touche **Écran de partie**. Lecture seule ; chaque requête porte un jeton aléatoire. |
| **Rapport de forces** | Une table de combat avec `"rapport"` calcule la colonne à partir de l'attaque et de la défense (rapport ou différence, arrondi en faveur du défenseur, de l'attaquant ou au plus proche, décalages de colonnes). Molette : attaque, enfoncée : défense ; touches Ajuster par pas de 1 ou de 5. |
| **Adversaire solo** | L'automate joue un ou plusieurs camps : posture tirée à chaque tour et liste de priorités pour chaque phase. La touche **Adversaire solo** affiche la priorité en cours ; appui si elle est impossible, appui long quand l'automate l'exécute. |
| **Pioches de cartes** | Tirage sans remise, défausse, remélange automatique ou manuel, cartes de remélange, mains par camp (l'écran de partie ne montre que le nombre de cartes en main). |
| **Campagnes** | Des armées nommées, liées à une touche Bataille, gardent leurs pertes et leurs renforts d'une bataille, d'une partie et d'une séance à l'autre (`Documents/Compagnon de wargame/campagnes/`). |
| **Partage Discord** | Résultats, événements programmés et bilan publiés dans un salon Discord par un webhook, groupés toutes les quelques secondes, mentions désactivées. |
| **Rapport illustré** | Une page HTML avec graphiques (chance aux dés par tour, pertes des batailles, résultats de combat, temps de jeu, compteurs), écrite à côté du journal à chaque nouvelle partie et imprimable en PDF. |
| **Sons** | Dés, coup critique, victoire, défaite, carte, nouveau tour, événement prévu ; sur l'ordinateur, sur l'écran de partie, ou les deux. |
| **Thèmes de touches** | Nuit d'état-major, Parchemin, Militaire, Science-fiction ; choisi par jeu (`"theme"`) ou imposé dans les réglages de la touche Partie. |
| **Import tableur** | Dans l'éditeur de jeu, collez des cellules d'Excel, Numbers ou Google Sheets (ou ouvrez un CSV) pour créer une table à colonnes ou une table aléatoire ; exportez n'importe quelle table en CSV. |

Trois actions s'ajoutent : **Pioche** (une pioche, ou la main d'un camp), **Adversaire solo** et **Écran de partie**. Sons, thème, Discord et rapport se règlent dans les réglages de la touche **Partie**. Pour partager sur Discord, créez un webhook dans les paramètres du salon (Intégrations → Webhooks) et collez son adresse à cet endroit ; elle n'est gardée que dans les réglages du plugin et n'est plus jamais réaffichée. L'écran de partie écoute par défaut sur le port 8484 ; on peut le limiter à cet ordinateur, et **Nouvelle adresse** rend caducs tous les liens déjà partagés.

Les champs Premium sont décrits dans `jeux/_PREMIUM.md` / `jeux/_PREMIUM.en.md` ; l'exemple complet est `exemple-premium.json` / `example-premium.json`. La version gratuite lit les mêmes fichiers et ignore simplement les champs Premium.

### Sécurité

Les fichiers de jeu circulent entre joueurs : le plugin les traite donc comme non fiables, tout comme les réglages des touches et sa propre sauvegarde.

- **Fichiers de jeu** : taille (1 Mo), profondeur, nombre d'éléments et longueur des textes bornés ; chaque champ est vérifié, les dés et les effectifs sont plafonnés, et une couleur doit être `#rgb` ou `#rrggbb` avant d'arriver dans l'image d'une touche.
- **Rien n'est écrit hors de ses dossiers** : un guide n'est jamais copié à travers un lien symbolique, le journal d'une sauvegarde doit être dans le dossier des journaux, et les fichiers s'ouvrent sans passer par un shell.
- **L'éditeur de jeu** n'écoute que sur 127.0.0.1, vérifie l'en-tête Host et un jeton de 128 bits envoyé en en-tête ; le jeton quitte la barre d'adresse dès que la page est chargée.
- **L'écran de partie** (Premium) est en lecture seule, n'accepte que les adresses de cet ordinateur dans l'en-tête Host (pas de rebinding DNS), exige un jeton aléatoire sur chaque requête de données et limite les connexions en direct par appareil.
- **Discord** (Premium) : seules les adresses de webhook Discord sont acceptées, les redirections sont refusées, les mentions et les aperçus de liens sont désactivés, les liens masqués et les titres venant des fichiers de jeu sont neutralisés, et les messages destinés à une ancienne adresse sont abandonnés dès qu'elle change.
- **Une erreur imprévue est journalisée, jamais fatale** : un fichier ou un message défectueux ne peut plus arrêter toutes les touches.

### Format des fichiers de jeu

Voir `jeux/_LISEZMOI.md` (noms de champs français) ou `jeux/_README.en.md` (noms anglais). Les deux écritures sont acceptées, même mélangées.

```json
{
  "id": "mon-jeu",
  "nom": "Mon jeu",
  "camps": ["Bleu", "Rouge"],
  "sequence": { "debut": ["Météo"], "parCamp": ["Mouvement", "Combat"], "fin": ["Fin de tour"] },
  "tables": {
    "melee": {
      "type": "poignee", "nom": "Mêlée", "seuil": 4, "camps": ["Attaquant", "Défenseur"],
      "profils": [{ "nom": "Vétérans", "seuil": 3, "des": 2 }, { "nom": "Milice", "seuil": 5, "des": 4 }],
      "pertes": { "parTouche": 1, "ordre": "faibles", "retraite": { "pertes": 50 } }
    }
  },
  "compteurs": { "pv": { "nom": "Points de victoire", "parCamp": true } },
  "programme": [{ "tour": 5, "texte": "Le pont est réparé" }]
}
```

### Développement

```bash
npm install
npm run build         # compile les deux éditions, puis assemble le dossier du plugin Premium
npm test              # tests de logique : dés, tables, batailles, compteurs, annulation, chrono, bilan, serveur de l'éditeur
npm run test:premium  # rapport de forces, pioches, solo, campagnes, serveur de l'écran, sons, Discord, page de l'écran
npm run test:editeur  # éditeur de jeu, dans un vrai navigateur
npm run test:reglages # page de réglages de chaque action, dans les deux éditions
npm run integration   # lance les deux plugins compilés face à un logiciel Stream Deck simulé, en français puis en anglais, puis le scénario d'attaques
npm run apercu        # rend les faces de touches en PNG dans apercu/
npm run pack          # valide et produit les deux fichiers .streamDeckPlugin dans dist/
```

`EDITION=gratuit` ou `EDITION=premium` devant `rollup -c` ne construit qu'une édition. Le paquet gratuit ne contient aucun code Premium.

| Chemin | Rôle |
|---|---|
| `src/core/etat.ts` | État de la partie et toutes les règles : séquence, batailles, pertes, compteurs, annulation, chrono, bilan. Sans dépendance au SDK |
| `src/core/jeux.ts`, `alias.ts` | Format des fichiers, validation avec messages lisibles, noms de champs anglais ↔ français |
| `src/core/rendu.ts` | Faces SVG des touches (144 px) et des écrans tactiles (200 × 100) |
| `src/core/langue.ts` | Textes français / anglais |
| `src/editeur.ts` | Serveur local de l'éditeur de jeu |
| `src/actions/` | Les onze actions |
| `src/premium/` | Édition Premium : rapport de forces, pioches, adversaire solo et campagnes (`partie.ts`), serveur de l'écran (`ecran.ts`), sons, Discord, les trois actions en plus |
| `premium/` | Fichiers Premium : page de l'écran de partie, modèle du rapport, sons, profils, jeu d'exemple, compléments des réglages, contrat de données (`CONTRAT.md`) |
| `scripts/manifestes.mjs`, `premium.mjs` | Manifests des deux éditions ; assemblage du dossier du plugin Premium |
| `com.paul.compagnon-wargame.sdPlugin/` | Manifest, `en.json` / `fr.json`, page de réglages, éditeur, profils, jeux fournis |

Réalisé en TypeScript avec le SDK officiel d'Elgato (`@elgato/streamdeck` 3.x) et Rollup.

### Limites connues

- Testé avec le SDK officiel et un logiciel Stream Deck simulé, pas encore sur un appareil réel. Les profils fournis, en particulier, sont à vérifier dans la vraie application.
- Au-delà d'une quinzaine de dés, une poignée s'affiche en résumé par face.
- Une mise à jour du plugin n'écrase jamais un jeu déjà présent dans `jeux/` : supprimez votre copie d'un jeu fourni pour obtenir sa nouvelle version.
- Premium : sous Windows, chaque son lance un processus PowerShell et peut donc arriver une fraction de seconde après l'appui ; les sons générés n'ont pas encore été écoutés sur de vrais haut-parleurs. L'écran de partie demande que les deux appareils soient sur le même réseau, et le pare-feu de Windows peut demander l'autorisation au premier démarrage.
