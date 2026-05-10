<div align="center">

```
    ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
    ░                                              ░
    ░            G  O  Y  A                       ░
    ░                                              ░
    ░    Native ddaPASEF DDA Search Engine         ░
    ░                                              ░
    ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
    ░                                              ░
    ░   "In the darkness, structure is revealed   ░
    ░         — not hidden."                       ░
    ░                                              ░
    ░    .d file  →  per-precursor 1/K₀            ░
    ░    b/y ions  →  8-feature SGD rescoring      ░
    ░    BH-FDR  →  native 4D DDA identifications  ░
    ░                                              ░
    ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░

     Francisco de Goya i Lucientes · 1746–1828
        Fuendetodos · Aragón · Zaragoza
```

*Pinturas Negras. Structure from darkness.*

![Python](https://img.shields.io/badge/python-3.9%2B-blue?style=flat-square)
![Platform](https://img.shields.io/badge/timsTOF-ddaPASEF-22d3ee?style=flat-square)
![License](https://img.shields.io/badge/license-Academic-a855f7?style=flat-square)
![ZIGGY](https://img.shields.io/badge/engine%20in-ZIGGY-DAAA00?style=flat-square)

</div>

---

## Who

Michael Krawitzky - built within [ZIGGY](https://github.com/MKrawitzky/Ziggy), the proteomics rockstar dashboard.

---

## What

A **native ddaPASEF DDA search engine** for Bruker timsTOF. Reads `.d` raw files directly via the TimsData SDK — no mzML, no ProteoWizard. Extracts per-precursor 1/K₀ from TIMS scan boundaries rather than estimated window centres, making it the first DDA engine to treat ion mobility as a first-class scoring dimension.

**Pipeline:**

```
analysis.tdf  →  ddaPASEF MS2 frames
  │
  ├─ Per-precursor 1/K₀ from TIMS scan range boundaries
  │   (not from isolation window centre — the actual measurement)
  │
  ├─ ±10 ppm precursor mass match
  ├─ 1/K₀ CCS filter (theoretical vs measured)
  │
  ├─ b/y fragment scoring (z = 1–4; z = 1 native for HLA)
  │
  ├─ 8-feature SGD logistic rescoring
  │   (charge, cosine, n_matched, ΔCCS, ΔRT, intensity_rank,
  │    missed_cleavages, fragment_coverage)
  │
  └─ Benjamini-Hochberg FDR @ 1%
```

Designed for ddaPASEF and **HLA immunopeptidomics** — the native z=1 ion extraction without forced charge assumptions makes Goya particularly effective for MHC class I peptides.

---

## When

Developed 2024–2026 alongside GauDIA. The DDA companion to ZIGGY's DIA engine suite. Built because the same mzML problem that motivated GauDIA applies equally to DDA: when you convert ddaPASEF data to mzML, the TIMS-measured 1/K₀ per precursor is either lost or averaged to the isolation window centre — a fundamentally less accurate value.

---

## Where

Runs locally — instrument PC or analysis workstation. Python 3.9+, Bruker TimsData SDK, a ddaPASEF `.d` directory, a FASTA database. Within [ZIGGY](https://github.com/MKrawitzky/Ziggy) it populates the Searches tab automatically alongside MSFragger DDA, Comet, X!Tandem, and MSBooster.

---

## Why

**Why name a DDA engine after Goya?**

Francisco de Goya i Lucientes was born in 1746 in Fuendetodos — a village of a few hundred people in the dry Aragonese steppe, 44 km south of Zaragoza. He became court painter to King Charles IV. He survived war, illness, and deafness. In his final years, confined and isolated in the Quinta del Sordo (House of the Deaf Man), he painted directly onto the walls of his home: the series now known as the *Pinturas Negras* — the Black Paintings.

Saturn Devouring His Son. The Witches' Sabbath. A Dog. Saturno. These were not public works. They were not commissions. They were Goya painting what he actually saw — structure emerging from darkness, form from chaos, signal from noise.

That is what Goya the engine does. ddaPASEF data is messy — co-isolated precursors, TIMS ramp artifacts, chimeric fragmentation. Goya extracts per-precursor 1/K₀ from the TIMS scan boundaries, filters by shape, rescores by eight independent features, and finds the signal in the darkness.

**The province of Aragón also gave the world Héroes del Silencio** — Enrique Bunbury, Juan Valdivia, Joaquín Cardiel, Pedro Andreu. One of the greatest rock bands ever to record in Spanish. From Zaragoza, same city. Their name gave rise to [Silent Heroes](https://github.com/MKrawitzky/SilentHeroes), the method advisor in ZIGGY. Aragón, once again, to the world.

> *"In the darkness, structure is revealed — not hidden."*

---

## Part of ZIGGY

| Engine | Mode | Approach |
|--------|------|----------|
| GauDIA | DIA | Cosine + BH-FDR |
| Copperfield | DIA | 4D evidence layers |
| PHANTOM | DIA | Probabilistic tracking |
| **Goya** | DDA | Native ddaPASEF, per-precursor 1/K₀ |
| Zyna | DIA post | Chimeric deconvolution |
| Silent Heroes | Advisor | Method optimisation |

[→ MKrawitzky/Ziggy](https://github.com/MKrawitzky/Ziggy)

---

*Academic License · © 2024–2026 Michael Krawitzky & Brett S. Phinney*
