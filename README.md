# Bconomy Pet Manager – User Guide

## What is this?

A single static HTML file that lets you load your Bconomy pet data, view and filter it in a table, reorder pets using custom ID lists or drag-and-drop, pin specific rows to the top, and apply automated sorting logic (Nuclear Orders) — then export the final ordered list of pet IDs to your clipboard.

No installation, no server, no account. Open the file in any browser and it works.

---

## Loading Your Data

You have three ways to get your pet JSON into the tool:

**Drag & drop** — drag a `.json` file from your file system directly onto the dashed drop zone at the top of the page.

**File picker** — click "📂 Choose JSON file" inside the drop zone to browse for your file.

**Paste** — paste your raw JSON text into the textarea below the drop zone, then click "🔍 Parse & Load".

The tool expects the JSON to have a `pets` array (and optionally an `eggs` array). Once loaded, the stats bar will show how many pets and eggs were found.

> Loading new data resets everything — all pins, lock state, and magic mode are cleared.

---

## The Table

Each row is one pet. Columns shown:

| Column | What it is |
|---|---|
| 📌 | Pin button |
| ID | Pet's unique numeric ID |
| 🐾 | Species emoji |
| Name | Pet name |
| Species | Species text |
| Tier | Pet tier |
| Gen | Generation |
| Skin | Skin name (blue badge) |
| Aura | Aura name (purple badge) |
| Adventure | Adventure type |
| Items Found | Lifetime items found |
| Times Bred | Breed count |
| Last Bred | Date of last breed |

By default pets are sorted by ID ascending.

---

## Filters & Search

The search bar and three dropdowns (Species, Skin, Aura) let you narrow down what's visible in the table. They work together — all active filters apply at the same time.

- **Search** matches against name, species, skin, and aura simultaneously.
- **Dropdowns** filter to an exact value.

Filters are disabled once Lock Order is on.

---

## ✨ Magic Mode

Magic Mode lets you impose a specific order on the table using a list of pet IDs you supply.

**How to use:**

1. Check "✨ Magic Mode" — an input area appears.
2. Paste your ID list in array format, e.g. `[59299, 5089, 27013]`.
3. Click one of the two apply buttons:

**🪄 Apply ID Order (Listed Only)** — shows only the pets whose IDs are in your list, in exactly the order you listed them. Pets not in the list are hidden.

**🪄➕ Apply ID Order (Listed First, Then All)** — shows the listed pets first in your specified order, then appends all remaining pets in their default (ID ascending) order.

The stats bar will show how many of your listed IDs matched actual pets in the loaded data.

> Magic Mode must be on to access Lock Order.

---

## 🔒 Lock Order

Lock Order freezes the current table state so you can run Nuclear Orders and export the result. It appears only when Magic Mode is active.

**Enabling lock:**
- The table order is snapshotted exactly as it appears on screen — no rows jump or reorder when you check the box.
- Filters, search, and magic ID inputs are all disabled.
- Pin buttons and drag-and-drop are disabled.
- The Nuclear Order buttons and Copy IDs button become available.

**Disabling lock:**
- Everything returns to how it was before locking — same order, same pins, filters re-enabled.
- No visible change to the table when you uncheck the box.

> **Workflow:** set up your order (magic mode + filters + pins + drag) → lock → run a Nuclear Order → copy IDs.

---

## 📌 Pinning

Pinning a row fixes it permanently at the top of the table, above all unpinned rows.

- Click the 📌 button on any row to pin it. The button turns orange and the row gets an orange highlight with a "PINNED" label.
- Click again to unpin. The row returns to its natural position in the base order (by ID or magic order) — it does not stay where it was visually, it goes back to where it belongs in the sorted list.
- Multiple rows can be pinned. Pinned rows appear in the order they were pinned.
- Pinning is available **before locking only**. Once Lock Order is on, pin buttons are grayed out and non-interactive.

---

## 🖱️ Drag & Drop

While Lock Order is off, you can drag any row to manually reorder the table.

- Click and hold a row, drag it to the desired position, release.
- A ghost/shadow shows where the row will land.
- The manual order you set becomes the new base order — pinning and unpinning will respect the positions you dragged things to.
- Drag is disabled once Lock Order is on.

---

## ⚛️ Nuclear Orders

Nuclear Orders are automated sorts that run on the locked table. They only affect **unpinned rows** — pinned rows always stay at the top, untouched.

All three Nuclear Orders are available after enabling Lock Order.

---

### Nuclear Order 1

**Sort key: Species → Skin → Aura**

Groups all pets of the same species together. Within each species, pets are sorted by skin then aura.

Skin order: `None → Alpha → Beta → Gamma → Delta → Epsilon → Zeta → Eta → Sunkissed → Grayscale → Whiteout → Overclocked → Signal → Static`

---

### Nuclear Order 2

**Sort key: Species → Skin → Aura**

Same structure as Nuclear 1, but the tier skin order is reversed (highest tier first), and None comes after the tier skins but before the special skins.

Skin order: `Eta → Zeta → Epsilon → Delta → Gamma → Beta → Alpha → None → Sunkissed → Grayscale → Whiteout → Overclocked → Signal → Static`

---

### Nuclear Order 3

**Sort key: Skin → Aura → Species**

Completely different grouping — skin is the primary key, not species. All Eta pets come first regardless of species, then all Zeta pets, and so on. Within each skin group, pets are sub-sorted by aura, then by species order within each aura.

Skin order: `Eta → Zeta → Epsilon → Delta → Gamma → Beta → Alpha → Sunkissed → Grayscale → Whiteout → Overclocked → Signal → Static → None`

None-skin pets always appear last in Nuclear 3.

---

## 📋 Copy IDs Order

Once you're happy with the order (after pinning, dragging, and/or running a Nuclear Order), click "📋 Copy IDs Order" to copy the full ordered list of pet IDs to your clipboard as a JSON array, e.g.:

```
[59299, 5089, 27013, 44201, ...]
```

The copied order reflects exactly what you see on screen — pinned rows first, then the rest in their current order.

---

## Typical Workflows

**Just view and filter your pets:**
Load JSON → use search/filters → done.

**Reorder by a specific ID list:**
Load JSON → enable Magic Mode → paste IDs → click Apply → view result.

**Sort everything by species and skin:**
Load JSON → enable Magic Mode → apply your ID list → enable Lock Order → click Nuclear Order 1 or 2 → Copy IDs.

**Keep specific pets at the top, sort the rest:**
Load JSON → enable Magic Mode → apply ID list → pin the rows you want fixed → enable Lock Order → run Nuclear Order → Copy IDs.

**Group everything by skin tier across all species (Nuclear 3):**
Load JSON → enable Magic Mode → apply ID list → enable Lock Order → click Nuclear Order 3 → Copy IDs.

---

## Notes

- The species sort order used in all Nuclear Orders follows a fixed internal list (poodle → dog → bat → mustang → pig → eagle → otter → tiger → … → snowman). Species not in this list sort to the end.
- Aura sort order: `None → Green → Purple → Orange → Cyan → Red → Pink → Blue → Yellow → Black → Deepskyblue → Magenta → White`.
- The tool never sends your data anywhere. Everything runs locally in your browser.
- Refreshing the page clears everything. There is no save state.
