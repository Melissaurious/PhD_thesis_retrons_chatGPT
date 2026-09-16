# Figure and table manifest — database-characterization Results

Status key: **READY** = PNG/TSV exists in the workbench · **BUILD** = specified, not yet generated ·
**GEN** = table exists as TSV, needs LaTeX formatting.

Figures live in `ARIS_OUTPUT/dbchar_workbench/figures/`, source tables in `../tables/`.

---

## Tables

| # | LaTeX label | Title | Unit / denominator | Source | Status |
|---|---|---|---|---|---|
| T1 | `tab:populations` | Anchor populations of the corpus | record; all 3,358,182 corpus records | `dbchar_g1/tables/s02_populations.tsv` | **READY** (in .tex) |
| T2 | `tab:units` | Analytical units | one row per unit; each its own denominator | `dbchar_g2/tables/g2_unit_ladder.tsv` | **READY** (in .tex) |
| T3 | `tab:recovery` | Records lacking an RT CDS | record; the 31,504 RT-CDS-less population | `dbchar_g2b/tables/g2b_summary.tsv` | **READY** (in .tex) |
| T4 | `tab:geometry` | Canonical placement geometry | placement; 344,154 canonical | `dbchar_g3/tables/g3_direction.tsv`, `g3_same_strand.tsv`, `g3_cds_between_explicit.tsv` | **READY** (in .tex) |
| T5 | `tab:atypical` | Atypical placements retained | placement; 345,313 **eligible** (not canonical) | `dbchar_g3/tables/g3_atypical_catalogue.tsv` | **READY** (in .tex) |
| T6 | `tab:redundancy` | Redundancy correction on taxonomy | record vs distinct protein, per taxonomy system | `dbchar_g5/tables/g5_redundancy_correction.tsv` | **READY** (in .tex) |
| T7 | `tab:cascade` | Dataset construction cascade | cumulative; canonical placements → pairs | `tables/L7_dataset_rule_cascade.tsv` | **READY** (in .tex) |
| T8 | `tab:inventory` | Dataset inventory | one row per dataset | `tables/K1_dataset_inventory.tsv` | **GEN** — 11 rows exist; needs LaTeX formatting (placeholder in .tex) |

### Supplementary tables worth adding

| # | Title | Unit / denominator | Source | Status |
|---|---|---|---|---|
| S1 | Per-file corpus identity (SHA-256, bytes, records) | file; 43 files | `dbchar_g1/tables/s01_file_identity.tsv` | **GEN** |
| S2 | Full per-family composition, all 41 families | distinct single-family protein | `tables/B1_family_composition.tsv` | **GEN** |
| S3 | Per-family RT length quantiles and Tukey fences | distinct single-family protein | `dbchar_g4/tables/g4_rt_length_by_family.tsv` | **GEN** |
| S4 | Per-model ncRNA statistics (calls, sequences, score, length) | call / distinct RNA | `tables/C3_model_composition.tsv` | **GEN** |
| S5 | The 12 cross-label proteins | distinct protein; all 12 | `tables/L2_cross_label_proteins.tsv` | **GEN** |
| S6 | Sequence-only records by collection and class | record; 16,688 | `tables/L1_sequence_only_by_database.tsv` | **GEN** |
| S7 | Prodigal partial-flag distribution with interpretation | distinct record | `tables/L3_prodigal_partial_flags.tsv` | **GEN** |
| S8 | Pair recurrence classes | exact pair; 30,924 | `tables/F3_recurrence_classes.tsv` | **GEN** |
| S9 | Taxonomy rank coverage and quality-field availability by collection | genome | `dbchar_g5/tables/g5_rank_coverage_by_system.tsv`, `g5_quality_availability.tsv` | **GEN** |
| S10 | Reproducibility controls per gate (recounts, positive controls) | quantity / control | `*/tables/*_second_counts.tsv`, `c0*_positive_controls.tsv` | **GEN** |

---

## Figures

| # | LaTeX label | File | Shows | Unit / denominator | Status |
|---|---|---|---|---|---|
| F1 | `fig:units` | `A1_unit_ladder.png` | unit-ladder funnel + loci-per-protein by collection | mixed; each panel labelled | **READY** |
| F2 | `fig:dboverlap` | `A4_database_attribution.png` | coverage vs exclusive partition; protein database span | loci (working pop.) / proteins (full corpus) | **READY** |
| F3 | `fig:families` | `B1_family_composition.png` | family composition, protein vs record level | distinct single-family protein | **READY** — *shows top 18; extend to all 41* |
| F4 | `fig:lengths` | `B2_rt_length_by_family.png` | RT length by family (box, Tukey) | distinct single-family protein, n≥30 | **READY** |
| F5 | `fig:completeness` | `B3_completeness_by_family.png` | completeness composition by family | distinct single-family protein | **READY** |
| F6 | `fig:multi` | `FIG_multi_margin.png` | MULTI best-vs-second margin vs seeded control | distinct MULTI protein; 7,593 | **BUILD** |
| F7 | `fig:ncrnalen` | `C2_ncrna_length_by_model.png` | RNA length by covariance model | distinct RNA sequence; 16,458 | **READY** |
| F8 | `fig:cmcomp` | `C3_model_composition.png` | model composition, calls vs distinct sequences | call / distinct RNA | **READY** |
| F9 | `fig:geometry` | `D2_distance_distribution.png` | signed separation, stratified by contig-start truncation | placement; 344,154 canonical | **READY** |
| F10 | `fig:joint` | `D6_joint_geometry.png` | joint geometry + placement/locus/pair weighting | placement / physical locus / exact pair | **READY** |
| F11 | `fig:strand` | `D5_strand_agreement.png` | same-strand rate by population; opposite-strand structure | placement; 344,154 canonical | **READY** |
| F12 | `fig:topology` | `F_pairing_topology.png` | partner degrees, component shapes, recurrence classes | protein / RNA / exact pair | **READY** |
| F13 | `fig:venn` | `FIG_tool_venn.png` | three-tool Venn + RNA carriage per intersection | **distinct RT protein** (see note) | **BUILD** |

### Figures to build (priority order)

1. **F13 — tool Venn (`fig:venn`).** The one genuinely missing headline figure.
   Build on **distinct RT proteins**, not records: the question ("which tools recognise this RT") is
   a property of the protein, and on records the diagram is dominated by sequencing effort. The axis
   changes the numbers materially — record-level carriage is 89.23 % (myRT+PADLOC) vs 13.50 % (myRT
   alone); the protein-level figures must be recomputed, not carried over. Add a locus-level panel as
   a supplement. Print on the figure: the three tools share model lineage, so agreement is not
   independent corroboration, and an absent tool cannot be distinguished from a tool never run.
   *Requires notebook section E, currently a scaffold.*

2. **F6 — MULTI margin (`fig:multi`).** Data exists in `multi_hmm_evidence_v1.parquet`
   (`margin_bits`) and `dbchar_g4/tables/g4_multi_hmm_margin_comparison.tsv`. Plot the margin
   distribution for MULTI against the seeded control, and add a margin-vs-length panel so the length
   confound is visible rather than only stated. *Requires notebook section G.*

3. **F3 extension — all 41 families.** Currently top 18. One-hue ranked horizontal bars, log x.

### Figures deliberately not proposed

- A taxonomic composition figure. Until section H is built it would have to pool GTDB and NCBI
  schemas, which double-counts phyla under two naming systems. Report Table S9 instead until then.
- Any "high-confidence pairs" figure. The selection rule is unset; see the .tex §dataset.

---

## Cross-reference: every figure/table to its notebook cell

| Artefact | Notebook section |
|---|---|
| T1, S1 | (landed g1 bundle — not recomputed) |
| T2, F1 | A1, A2 |
| F2 | A4 |
| T3, S6, S7 | L1, L3 (+ landed g2b) |
| T5, S2, S3, F3–F5 | B1–B3 |
| S4, F7, F8 | C2, C3 |
| T4, F9 | D1–D3 |
| F10 | D6 |
| F11 | D5, L4 |
| F12, S8 | F1–F3 |
| T6, S9 | (landed g5 bundle) |
| T7, T8 | K1, K2, L7 |
| S5 | L2 |
