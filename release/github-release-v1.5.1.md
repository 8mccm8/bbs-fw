# bbs-fw v1.5.1

> 🇬🇧 English below — 🇫🇷 Version française plus bas

---

## 🇬🇧 English

Maintenance release based on stable v1.5.0, focused on **860C display**
compatibility and bundling two upstream fixes.

### 🐛 Fixes

- **Standard/Sport mode toggle with 860C display** — The 860C continuously sends
  the `WRITE_MODE => STANDARD` frame (~every 600 ms), which overrode any
  Sport-mode switch triggered locally (PAS + light combo). Now, when
  **"Operation mode Toggle"** (`assist_mode_select`) is set to anything other
  than `OFF`, the firmware ignores the display's `WRITE_MODE` frames and stays
  the sole owner of the operation mode. Behaviour is unchanged when the option is
  `OFF` (the display drives the mode as before).

- **Inverted "moving" status** (#164, upstream) — The response to the display's
  `READ_MOVING` request returned the opposite state (stopped ↔ moving). Values
  corrected (`0x31` = moving, `0x30` = stopped).

### 🔧 Improvements

- **Default throttle curve** (upstream) — Minor tweak to the lower end of the
  custom throttle map for a slightly more responsive feel at the start of travel.

### ✅ Tested

- Tested on BBSHD with an 860C display: Standard/Sport toggle works, **no spurious
  motor engagement at startup**.
- BBS02: compiled, not tested on hardware.

### ⚠️ Compatibility note

The **"Startup Assist Level"** option has no effect with a Bafang display
(850C/860C): the display imposes its own PAS level (always 1) at startup via the
`WRITE_PAS` frame, and the protocol does not let the controller force the
displayed value. This is inherent to the protocol and is not fixed.

---

## 🇫🇷 Français

Version de maintenance basée sur la v1.5.0 stable, ciblant la compatibilité
display **860C** et intégrant deux correctifs upstream.

### 🐛 Corrections

- **Bascule mode Standard/Sport avec display 860C** — Le 860C émet la trame
  `WRITE_MODE => STANDARD` en continu (~600 ms), ce qui écrasait toute bascule
  vers le mode Sport déclenchée localement (combo PAS + lumière). Désormais, quand
  **« Operation mode Toggle »** (`assist_mode_select`) est différent de `OFF`, le
  firmware ignore les trames `WRITE_MODE` du display et reste seul maître du mode.
  Comportement inchangé lorsque l'option est sur `OFF` (le display pilote le mode
  comme avant).

- **Statut « en mouvement » inversé** (#164, upstream) — La réponse à la requête
  `READ_MOVING` du display renvoyait l'état opposé (à l'arrêt ↔ en mouvement).
  Valeurs corrigées (`0x31` = mouvement, `0x30` = arrêt).

### 🔧 Améliorations

- **Courbe d'accélérateur par défaut** (upstream) — Léger ajustement du bas de
  course de la map throttle personnalisée pour une réponse un peu plus présente
  au début de la course.

### ✅ Validé

- Testé sur BBSHD avec display 860C : bascule Standard/Sport fonctionnelle,
  **aucun engagement moteur parasite au démarrage**.
- BBS02 : compilé, non testé sur matériel.

### ⚠️ Note de compatibilité

L'option **« Startup Assist Level »** reste sans effet avec un display Bafang
(850C/860C) : le display impose son propre niveau PAS (toujours 1) au démarrage
via la trame `WRITE_PAS`, et le protocole ne permet pas au controller de forcer
l'affichage. Comportement inhérent au protocole, non corrigé.

---

## ⚙️ Build / Compilation

- Toolchain: SDCC 4.5.0
- Targets / Cibles:
  - BBSHD (`-mmcs51 --model-large --xram-size 3840`)
  - BBS02 (`-mmcs51 --model-large --xram-size 1792`)

| Binary | Size | MD5 |
|---|---|---|
| `bbs-fw-v1.5.1-BBSHD.hex` | 67 481 B | `e5102e3f79e7d636b2b64814b09ab8b8` |
| `bbs-fw-v1.5.1-BBS02.hex` | 63 095 B | `1bf87762a61a928fc181b2e2d6cfae3f` |
