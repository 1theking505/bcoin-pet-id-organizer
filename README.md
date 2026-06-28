# Bconomy Tool v37 — README

A single-file browser-based companion tool for the Bconomy game. Open the `.html` file in any modern browser — no installation required.

---

## Getting Started

1. Open `bconomy_tool_v37.html` in a browser.
2. Enter your **Player ID** in the top bar.
3. Enter your **API Key** (optionally toggle visibility with the 👁 button).
   > **Tip:** If a shared API key is already filled in and working, you don't need to enter your own — just add your Player ID and fetch. The API Key field only needs to be changed if the shared one stops working or you want to use your personal key.
4. Check **Save credentials** to persist them across sessions so you don't have to re-enter anything next time.
5. Click **Fetch All** to load your full account data, or **⚡ Quick Fetch** for pets + inventory only.

> **Fetch All** pulls: profile, stats, trophies, farm, relay, quests, inventory, and pets.  
> **Quick Fetch** is faster and only refreshes pets and inventory (useful when feeding cravings).

---

## Interface Layout

| Area | Description |
|---|---|
| **Sidebar** | Navigation between all tabs |
| **Global Top Bar** | Player ID, API Key, Fetch All, Quick Fetch, and status messages |
| **Main Panel** | Tab-specific content |

A **Light Mode** toggle is available in the Settings tab to flip the dark theme.

---

## Tabs & Features

### 👤 Profile
Displays a full overview of your player account after fetching.

- **Identity card** — username, avatar, player ID, and rank
- **Basic stats grid** — key numbers (BC balance, rank, level, etc.)
- **Cooldowns** — shows all action cooldowns and whether they are Ready or Active
- **Active Effects** — lists all current buffs/effects with names, values, and expiry (color-coded: soon = red, ok = green)
- **Buddy List** — shows buddies with their last action and player ID
- **Perks** — full perk card grid showing icon, name, description, current level, benefit, and whether maxed
- **Statistics** — full stat breakdown from your profile
- **Trophies** — all earned trophies with count and date

---

### 🐾 Pet Manager
The most feature-rich tab — a full pet management dashboard.

#### Loading Pets
- **Fetch via API** — use the global Fetch All or Quick Fetch button
- **Drop a JSON file** — drag and drop a `pets.json` export onto the drop zone, or click to browse

#### Pet Table
Displays all pets in a sortable, filterable, paginated table with columns for: ID, name, species, skin, aura, tier, adventure type, XP, energy, items found, times bred, and adventure status.

**Filters:**
- Free-text search (name, species, skin, aura)
- Dropdown filters for Species, Skin, and Aura
- Results update live as you type

**Pagination:**
- Configurable rows per page (5–2000)
- First / Prev / Next / Last navigation
- Shown at both top and bottom of the table

#### Pinning
- Click the 📌 pin button on any pet row to pin it to the top of the table
- Buddy pets (from your buddy list) are auto-pinned in blue
- Copy in-game pin IDs or generate a `/pets/setpins` command to clipboard

#### Magic ID Ordering
Paste a list of pet IDs (JSON array or space/comma/newline separated) to reorder or filter the table:
- **Listed Only** — show only pets matching the IDs, in that order
- **Listed First** — show matched pets first, then all others

#### Lock & Nuclear Sort
1. Enable **Lock Order** to freeze the current table order for sorting
2. Apply one of four Nuclear Sort presets:
   - **Nuclear 1** — Species → Skin → Aura (Skin order: None → Alpha…Eta → Specials)
   - **Nuclear 2** — Species → Skin → Aura (Skin order: Eta…Alpha → None → Specials)
   - **Nuclear 3** — Skin → Species → Aura (Eta…Alpha → Specials → None last)
   - **Nuclear 4** — Tier↓ → Adventure Type → Species → Skin↓ → Aura
3. Click **Copy IDs** to copy the sorted ID list
4. Click **Copy /setpins** to generate a ready-to-paste game command

#### Craving Commands
Automatically detects adventuring pets with active cravings and generates feed commands.

- **Eligible pets** = adventuring + XP below threshold + has an active craving
- Groups cravings by item, shows total amount needed per item
- Displays per-pet breakdown with XP info
- Checks your current inventory and highlights if you're short
- Shows crafting requirements if the craving item is craftable
- Configurable **multiplier** (multiply all amounts before generating commands)
- **Compact toggle** and **column count** controls for layout
- **Auto-refresh** — enable to automatically re-fetch pets + inventory on a timer (configurable interval in seconds, with a live countdown)

#### Pet Analytics Dashboard
A collapsible summary panel showing:
- Adventure type assignment breakdown (how many pets on Fish / Hunt / Explore / Mine)
- Adventure status (on adventure vs idle)
- Tier breakdown
- Skin breakdown
- Aura breakdown
- Species breakdown
- Breeding stats (total breeds, ever bred, never bred, most-bred pet)
- Top 5 item finders (lifetime items found per pet)

---

### 🌾 Farm
Displays your farm state after fetching.

- **Crop Analytics** — groups plots by crop type, shows count per boost multiplier, and expiry buckets (color-coded: ≤10d, ≤20d, ≤30d, more/no expiry)
- **Farm Plots grid** — each plot card shows: plot number, level, whether it's an extra plot, what's planted, and active boost info (multiplier + time remaining)
- Empty plots are shown with a grey border; planted plots with a green border

---

### ⚙️ Relay
Displays your Relay Network configuration after fetching.

- **Relay Bays** — each bay (Mint 🪙, Refinery ⚗️, Cooling ❄️) shown as a card with: module count, extra count, mode, upgrades, and allocation percentages
- **Salvage Buffer** — current salvage buffer value
- **Research Unlocked** — list of all unlocked research items
- **Auto-Deposit** — auto-deposit configuration

---

### 📋 Quests
Displays active quests after fetching.

- Each quest card shows: item icon, item name, progress fraction (fulfilled / required), and a color-coded progress bar
  - Blue = < 50%, Yellow = 50–99%, Green = complete ✅

---

### 📦 Inventory
Displays your item inventory after fetching.

- **Total worth** — sum of all item values in BC
- **Search** — filter items by name or ID name
- **View Toggle** — switch between two display modes:
  - **Grouped View** — card grid sorted by category group, with pinned items at top
  - **Bconomy View** — matches the in-game Items page layout, organized by: Pinned, Boosts, Usable, Equippable, Weapons, Craftable, Relay, Crops, Fishing, Hunting, Explore, Mining, Other, Rare, and Unowned (items you don't have)
- Each item card shows: thumbnail, name, quantity, and BC worth
- Items can be pinned (📌) to the top of the list

---

### 🤤 Pet Loot Calculator
Calculate expected loot and energy economics for your pets without needing to fetch live data.

**How to use:**
1. Click **Import from Pet Manager** to pre-fill rows from your loaded pets (grouped by adventure type and tier), or add rows manually with **+ Add Row**
2. For each row, set:
   - **Adventure type** — Fish 🐟, Hunt 🦌, Explore 🧭, or Mine ⛏️
   - **Tier** (T0–T20)
   - **Boost** — None, Fragrant Dogrose (×2), Mystical Rowan (×4), Legendary Aguaje (×8), or Magic Token (×10)
   - **Count** — number of pets in this group
3. The **Gluttony perk level** is auto-read from your profile (if fetched) to adjust energy cap
4. Click **⚡ Calculate All** to see results

**Results show per-adventure block:**
- Items per minute, energy per minute, session length
- Full drop table with expected counts and BC value per session
- Energy spent, food energy ROI, net energy, total loot value (BC)

**Grand Total panel:**
- Aggregated across all adventures: total pets, energy spent, food ROI, net energy, and total loot value

**Layout controls:**
- **⊞ Wide / ⊟ Stack** — toggle between compact 4-column layout and stacked layout
- Font size slider for pet count inputs

---

### 🧪 Crafting Recipes
A searchable reference for all in-game crafting recipes.

- Displays all recipes as cards with item thumbnail, name, and ingredient list
- **Ingredient color coding:** yellow = also a craftable sub-component, grey = raw material
- **Search** — filter by output item name or ingredient name (highlights matches in yellow)
- **Show full ingredient tree** checkbox — expands sub-components recursively to show all raw materials needed
- Item count shown in the tab header

---

## Global Workflows

### Full Data Load
1. Enter Player ID + API Key → **Fetch All**
2. All tabs populate simultaneously

### Craving Feed Loop
1. **Quick Fetch** (or auto-refresh) to reload pets + inventory
2. Switch to **Pet Manager → Craving Commands**
3. Copy generated commands → paste into game

### Pet Reorder & Setpins
1. Fetch All → Pet Manager
2. Use filters / Magic IDs to narrow down pets
3. Lock Order → apply Nuclear Sort
4. Copy `/setpins` command → paste into game

### Loot Planning (offline)
1. Open Pet Loot Calculator (no fetch needed)
2. Add rows for each adventure group with tier + boost
3. Calculate to compare loot value across adventure types

### Recipe Lookup
1. Open Crafting Recipes tab (works without fetching)
2. Search for an item or ingredient
3. Enable full tree view to see total raw material requirements

---

## Settings & Preferences

| Setting | Where |
|---|---|
| Save credentials (Player ID + API Key) | Global bar checkbox |
| Light / Dark mode | Settings tab |
| Auto-refresh interval | Pet Manager → Craving section |
| Pet table rows per page | Pagination bar |
| Pet count font size | Pet Loot Calculator slider |
| Pet loot layout (compact/wide) | Pet Loot Calculator toggle |

---

## Data Sources

- All live data is fetched from the Bconomy API using your Player ID and API Key
- Item images are loaded from `assets.bconomy.net`
- Crafting recipes, item worth values, drop rates, and tier stats are hardcoded in the tool and may need updates from the developer if the game changes

---

## Notes & Limitations

- The tool runs entirely in your browser — no data is sent to any third-party server
- CORS restrictions may block direct API calls in some environments; if you see a CORS error, use the full **Fetch All** path instead of Quick Fetch
- Recipes are maintained manually in `CRAFTING_RECIPES`; if something is missing or incorrect, notify the developer
- Pet analytics and craving commands require pets to be loaded first (via Fetch All or Quick Fetch)
- The Pet Loot Calculator uses hardcoded tier/drop data (all Level 100); results are estimates based on average drop rates
