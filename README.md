# Algeria — Wilayas, Daïras & Communes

A clean, ready-to-use dataset of **Algeria's administrative divisions** — every **commune** (municipality / بلدية) mapped to its **daïra** (district / دائرة) and **wilaya** (province / ولاية), in both Latin (ASCII/French) and Arabic.

The data is provided in **two structures**, because Algeria's territorial organization changed:

| File | Wilayas | Communes | Reflects |
|------|:-------:|:--------:|----------|
| [`algeria-communes-58-wilayas.json`](algeria-communes-58-wilayas.json) | **58** | 1,541 | Organization after the **2019** reform (Loi n° 19-12) |
| [`algeria-communes-69-wilayas.json`](algeria-communes-69-wilayas.json) | **69** | 1,541 | Current official organization after the **2026** reform (Loi n° 26-06) |

> The number of communes (1,541) is identical in both files. The 2026 reform did **not** change communes — it only regrouped existing communes by promoting 11 districts into full wilayas (codes 59–69). Pick the file that matches the administrative structure your project needs.

If you're unsure which to use: **use the 69-wilaya file** — it is the current official structure as of April 2026.

---

## Data format

Each file is a JSON array of commune objects. One object per commune:

```json
{
    "id": 22,
    "commune_name_ascii": "Timekten",
    "commune_name": "تيمقتن",
    "daira_name_ascii": "Aoulef",
    "daira_name": "أولف",
    "wilaya_code": "01",
    "wilaya_name_ascii": "Adrar",
    "wilaya_name": "أدرار"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `id` | number | Internal commune identifier |
| `commune_name_ascii` | string | Commune name in Latin/French script |
| `commune_name` | string | Commune name in Arabic |
| `daira_name_ascii` | string | Parent daïra (district) name in Latin/French |
| `daira_name` | string | Parent daïra name in Arabic |
| `wilaya_code` | string | Zero-padded wilaya code, e.g. `"01"`–`"58"` (or `"69"`) |
| `wilaya_name_ascii` | string | Wilaya (province) name in Latin/French |
| `wilaya_name` | string | Wilaya name in Arabic |

Notes:
- `wilaya_code` is a **string** with a leading zero for codes below 10 (`"01"`, not `1`).
- Files are UTF-8, pretty-printed with 4-space indentation.

### Hierarchy

```
Wilaya (province)  →  Daïra (district)  →  Commune (municipality)
```

A wilaya contains several daïras; a daïra contains several communes. The 58-wilaya file spans 548 daïras.

---

## What changed between the two files

The 2026 reform (Loi n° 26-06, published 4 April 2026) created **11 new wilayas** by promoting existing districts. Every commune they contain was previously part of a "parent" wilaya:

| New wilaya | Code | Split from |
|------------|:----:|------------|
| Aflou | 59 | Laghouat |
| Barika | 60 | Batna |
| El Kantara | 61 | Biskra |
| Bir El Ater | 62 | Tébessa |
| El Aricha | 63 | Tlemcen |
| Ksar Chellala | 64 | Tiaret |
| Aïn Oussera | 65 | Djelfa |
| Messaad | 66 | Djelfa |
| Ksar El Boukhari | 67 | Médéa |
| Boussaâda | 68 | M'Sila |
| El Abiodh Sidi Cheikh | 69 | El Bayadh |

In the 69-wilaya file, the 92 communes belonging to these new wilayas carry codes 59–69; in the 58-wilaya file the same communes carry their parent wilaya's code. **All other records are identical between the two files.**

> Codes `1`–`58` are unchanged between the two structures (the 2019 reform's 10 new wilayas, codes 49–58, are already present in both files).

---

## Usage examples

**JavaScript / Node**
```js
const communes = require("./algeria-communes-69-wilayas.json");

// All communes of a wilaya (e.g. Béni Abbès, code 52)
const beniAbbes = communes.filter(c => c.wilaya_code === "52");

// Group communes by wilaya
const byWilaya = communes.reduce((acc, c) => {
  (acc[c.wilaya_name_ascii] ??= []).push(c.commune_name_ascii);
  return acc;
}, {});
```

**Python**
```python
import json

with open("algeria-communes-69-wilayas.json", encoding="utf-8") as f:
    communes = json.load(f)

# Communes of Oran (code 31)
oran = [c for c in communes if c["wilaya_code"] == "31"]
```

---

## Data quality & sources

This dataset was fact-checked commune-by-commune against an up-to-date 2026 reference and official decrees, and corrected where needed.

- Administrative reforms verified against the Algerian *Journal Officiel*: **Loi n° 19-12** (2019, 48 → 58 wilayas) and **Loi n° 26-06** (2026, 58 → 69 wilayas).
- Notable correction applied: **Tabelbala** is assigned to **Béni Abbès** (wilaya 52), not Béchar — it was transferred to Béni Abbès by the 2019 reform, a change many datasets still omit.

If you spot an error, please open an issue or a pull request with a source.

## License

Released under the [MIT License](LICENSE).
