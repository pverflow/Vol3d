# Third-party license audit

Last checked: 2026-04-09

This file is a practical license snapshot for the dependencies currently used by this repository.

> This is a repository-level engineering summary, not legal advice.

---

## Overall result

### Good news
The dependency set is **mostly permissive FOSS**.

The direct dependencies currently used by the project are declared under:
- **MIT**
- **Apache-2.0**
- **MIT OR Apache-2.0**
- **Apache-2.0 OR MIT**

No direct dependency was found to be GPL-only or AGPL.

### Important nuance
The desktop/Tauri dependency tree includes some **transitive** crates under:
- **MPL-2.0**
- **Unicode-3.0**
- several multi-license expressions that still include permissive options

That does **not** automatically block commercial or permissively licensed distribution, but it does mean you should treat third-party notices and source-attribution obligations seriously when shipping binaries.

---

## Direct JavaScript / npm dependencies

| Package | Version | Declared license |
|---|---:|---|
| `@tauri-apps/plugin-dialog` | `2.7.0` | `MIT OR Apache-2.0` |
| `@tauri-apps/plugin-fs` | `2.5.0` | `MIT OR Apache-2.0` |
| `fflate` | `0.8.2` | `MIT` |
| `@tauri-apps/cli` | `2.10.1` | `Apache-2.0 OR MIT` |
| `typescript` | `5.9.3` | `Apache-2.0` |
| `vite` | `6.4.2` | `MIT` |

### Notes
- `fflate` is the only direct runtime web dependency outside the Tauri plugin pair.
- `typescript`, `vite`, and `@tauri-apps/cli` are tooling / build-time dependencies.
- The Tauri plugin packages are dual-licensed in a standard permissive way.

---

## Direct Rust / Cargo dependencies

| Crate | Version | Declared license |
|---|---:|---|
| `tauri` | `2.10.3` | `Apache-2.0 OR MIT` |
| `tauri-build` | `2.5.6` | `Apache-2.0 OR MIT` |
| `tauri-plugin-dialog` | `2.7.0` | `Apache-2.0 OR MIT` |
| `tauri-plugin-fs` | `2.5.0` | `Apache-2.0 OR MIT` |

### Project itself
The application crate currently declares:
- `vol3d` → `MIT`

That is compatible with using permissive third-party dependencies, provided you comply with each dependency’s notice / attribution requirements.

---

## npm transitive license summary

From the current `package-lock.json` / installed package metadata:

| License | Count |
|---|---:|
| `MIT` | `62` |
| `Apache-2.0 OR MIT` | `13` |
| `MIT OR Apache-2.0` | `2` |
| `Apache-2.0` | `1` |
| `BSD-3-Clause` | `1` |
| `ISC` | `1` |

This is a very permissive npm tree overall.

---

## Cargo transitive license summary

From current Cargo metadata / `src-tauri/Cargo.lock`:

Largest groups:
- `MIT OR Apache-2.0` → `227`
- `MIT` → `117`
- `Apache-2.0 OR MIT` → `30`
- `MIT/Apache-2.0` → `24`
- `Unicode-3.0` → `18`
- `Apache-2.0 WITH LLVM-exception OR Apache-2.0 OR MIT` → `13`
- `Zlib OR Apache-2.0 OR MIT` → `10`
- `MPL-2.0` → `7`
- `Unlicense OR MIT` / `Unlicense/MIT` → `6` combined
- `BSD-3-Clause` and BSD/MIT/Apache combinations → small count
- `ISC` → `1`

The `MIT` count includes the app itself plus much of the dependency tree.

No GPL-only or AGPL package was found in the Cargo dependency metadata that was inspected.

---

## Notable transitive licenses by name

### MPL-2.0 crates
These are the ones worth explicitly noticing in the current Cargo tree:

- `cssparser`
- `cssparser-macros`
- `dtoa-short`
- `option-ext`
- `selectors`

### Unicode-3.0 crates
These mostly come from ICU / Unicode data handling:

- `icu_collections`
- `icu_locale_core`
- `icu_normalizer`
- `icu_normalizer_data`
- `icu_properties`
- `icu_properties_data`
- `icu_provider`
- `litemap`
- `potential_utf`
- `tinystr`
- `writeable`
- `yoke`
- `zerofrom`
- `zerotrie`
- `zerovec`

### Multi-license crate including LGPL option
These were found as:
- `r-efi` → `MIT OR Apache-2.0 OR LGPL-2.1-or-later`

Because that crate offers permissive options too, the LGPL path is not the only available one.

---

## Practical interpretation

### For your current setup
Using mostly permissive FOSS libraries is generally fine with an MIT-licensed project, **as long as you honor their license terms**.

### The main practical obligations you should expect
- keep copyright / license notices intact where required
- include third-party license notices with shipped binaries when appropriate
- if you modify MPL-covered code, review MPL file-level obligations carefully
- keep a reproducible dependency/license record for releases

### What I would recommend before public distribution
1. Keep this audit file in the repo.
2. Add a packaged `THIRD_PARTY_NOTICES` file to desktop release artifacts.
3. Keep the current dependency audit updated when dependencies change.
4. If you want a stronger compliance workflow, automate license report generation in CI.

---

## Bottom line

### Safe summary
- **Direct dependencies:** all permissive
- **npm transitive dependencies:** all permissive in the current audit
- **Cargo transitive dependencies:** mostly permissive, with some **MPL-2.0** and **Unicode-3.0** entries
- **No obvious GPL / AGPL blocker found** in the inspected dependency metadata

If you want, the next useful step is to generate a proper **`THIRD_PARTY_NOTICES.md`** or release-bundled notice file from this audit and wire it into the Windows packaging flow.



