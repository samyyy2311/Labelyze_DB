<div align="center">

# Labelyze DB

**The offline product and ingredient database powering the Labelyze app.**

<p>
  <img alt="License" src="https://img.shields.io/badge/License-ODbL_v1.0-blue">
  <img alt="Platform" src="https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white">
  <img alt="Format" src="https://img.shields.io/badge/Format-SQLite-003B57?logo=sqlite&logoColor=white">
  <img alt="Mode" src="https://img.shields.io/badge/Mode-Offline--First-orange">
  <img alt="Updates" src="https://img.shields.io/badge/Updates-OTA%20via%20Releases-informational">
</p>

<p>
  <a href="https://labelyze.in"><strong>Website</strong></a> &nbsp;|&nbsp;
  <a href="https://play.google.com/store/apps/details?id=in.caffeinelabs.labelyze"><strong>Google Play</strong></a> &nbsp;|&nbsp;
  <a href="https://github.com/samyyy2311/Labelyze_DB/releases/latest"><strong>Latest Release</strong></a>
</p>

</div>

---

## What This Repository Is

This repository contains the public offline database used by the [Labelyze](https://labelyze.in) mobile application.

The app checks for a new `labelyze_india.db` on every launch by polling the GitHub Releases API. If the file size has changed, it downloads and applies the update silently in the background. No reinstall required.

---

## What Is in the Database

| Table | Contents |
|---|---|
| Products | Metadata for 590+ Indian products |
| Barcodes | EAN/UPC mappings to product records |
| Ingredients | Per-product ingredient lists |
| Nutrition | Energy, fat, carbs, sugar, protein, sodium per product |
| Normalization | Ingredient name aliases and canonical forms |
| Regulatory | Reference mappings across FSSAI, CDSCO, EU, FDA, and WHO |

---

## What Is Not in This Repository

- Application source code
- Scoring and analysis logic
- Internal moderation or curation tools
- Private infrastructure or APIs
- Proprietary brand or product assets

The app code lives in a separate private repository. Only the database is published here.

---

## How OTA Updates Work

```
App launch
  └── GET https://api.github.com/repos/samyyy2311/Labelyze_DB/releases/latest
        └── Compare asset size of labelyze_india.db to last applied size
              └── If changed: download, validate SQLite magic bytes, swap on disk
                    └── Score and results reflect new data on next scan
```

Updates are anonymous. No account, token, or device identifier is sent. The only request is a standard public GitHub API call.

---

## Release Naming

| Tag format | Purpose |
|---|---|
| `v1.8.1` | Full app release — includes both APK and updated DB |
| `db-only-YYYY-MM-DD` | Database-only update — no APK, no reinstall needed |

To push a database update without a new app version, create a release tagged `db-only-YYYY-MM-DD` and attach only `labelyze_india.db`. The app will detect and apply it automatically.

---

## Data Sources

Entries are compiled from publicly available sources including:

- Product labels and manufacturer disclosures
- FSSAI permitted lists and advisory notices
- CDSCO cosmetics regulatory guidance
- EU Cosmetics Regulation (EC 1223/2009) and food additive regulations
- FDA GRAS database and banned substance lists
- WHO dietary guidelines and hazard assessments
- IARC carcinogenicity classifications
- Barcode registry public records

---

## License

The database (`labelyze_india.db` and all CSV source files) is published under the **Open Database License (ODbL) v1.0**.

You are free to share, adapt, and build upon this data as long as you attribute the source and release any derivative databases under the same license.

Full license text: [opendatacommons.org/licenses/odbl/1-0](https://opendatacommons.org/licenses/odbl/1-0/)

---

## Legal Notice

Labelyze is an independent project. It is not affiliated with or endorsed by FSSAI, CDSCO, the FDA, WHO, the European Commission, or any product manufacturer.

Product names, trademarks, and brand assets referenced in the database belong to their respective owners and are used solely for identification purposes.

Labelyze trademarks, application logic, scoring systems, and source code are not covered by this license.
