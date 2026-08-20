# R-scape + RNAView on a single tRNA structure (1EHZ)

What I actually did here: ran R-scape directly against the 1EHZ crystal structure to see how it
annotates base pairs/contacts straight from 3D coordinates (via RNAView, which R-scape calls
internally when you pass `--pdb`), rather than from a real multi-sequence alignment.

Because the input is a **single sequence**, there's no evolutionary signal to test — covariation
needs variation across many homologs. So this run isn't really "detect covariation" (that's what
[`secondary-structure-covariation-and-annotation-with-rscape`](../secondary-structure-covariation-and-annotation-with-rscape)
does with a real Rfam alignment). This is R-scape's structure-annotation side: take the PDB, pull
contacts out of it with RNAView, and lay them onto the sequence/secondary-structure bookkeeping it
normally uses for covariation.

## Input files

- `1EHZ.pdb` — yeast tRNA-Phe crystal structure (https://www.rcsb.org/structure/1EHZ)
- `1ehz_A.sto` — chain A sequence as a (single-sequence) Stockholm file:

		# STOCKHOLM 1.0
		1ehz_A GCGGAUUUAGCUCAGUUGGGAGAGCGCCAGACUGAAGAUCUGGAGGUCCUGUGUUCGAUCCACAGAAUUCGCACCA
		//

## Command

	$ R-scape --pdbchain A --pdb 1EHZ.pdb 1ehz_A.sto

`--pdb 1EHZ.pdb --pdbchain A` tells R-scape to fetch chain A's 3D contacts from the structure
(via RNAView) and map them onto the sequence in `1ehz_A.sto`, instead of only trusting whatever
`SS_cons` line an alignment provides.

## Why is there a `.hmm` and a `.cm` here? I didn't run cmbuild/hmmbuild

Right — `1ehz.hmm` and `1ehz.cm` aren't something I invoked. R-scape builds them itself as a side
effect. Under the hood it needs a model of the input alignment to do its bookkeeping (consensus
columns, expected pair positions, etc.), so it shells out to Infernal's `cmbuild` on the Stockholm
file it was given. You can see this in the `.cm` file's own header:

	COM      [1] .../rscape_v2.6.10/bin/../lib/infernal/src/cmbuild --noss -F 1ehz.cm 1ehz_A_A.sto.sto

`cmbuild` in turn always produces a companion filter profile HMM alongside the CM (Infernal uses
it as a fast local-alignment filter before the full CM scan) — that's `1ehz.hmm`. Both are just
Infernal's standard build artifacts:

- **CM (covariance model, `1ehz.cm`)** — a full profile stochastic context-free grammar: emission
  probabilities per consensus column *and* pairwise emission probabilities for base-paired
  columns, so it can score secondary structure, not just linear sequence.
- **HMM (`1ehz.hmm`)** — the same consensus columns but flattened into a standard profile HMM with
  no pairwise/structural terms, used by Infernal as a cheap pre-filter.

With only one input sequence, `NSEQ 1` / `EFFN 1.000000` in both files — there's no real "model
building" happening (nothing is generalizing across homologs), it's essentially a pass-through of
the single sequence into Infernal's file formats so R-scape's downstream code has something to
work with.

## Output files

Everything else is named `1ehz_A_1.1EHZ.A.*` (R-scape's `<alignment>_<n>.<pdbid>.<chain>.*` naming):

- `1ehz_A_1.1EHZ.A.cmap` — the actual point of this run: pairwise contacts pulled from the PDB via
  RNAView, one line per `(i, j)` pair with its geometry, e.g.

		# ij in alignment | ij in pdbsequence | basepair type
		# 1 72 | 1 72 | WWc
		# 1 2  | 1 2  | CONTACT

  `WWc` = Watson-Crick *cis* base pair (Leontis-Westhof nomenclature, as classified by RNAView);
  `CONTACT` = a 3D proximity RNAView flagged that isn't a canonical WC pair.
- `1ehz_A_1.1EHZ.A.helixcov` — the contacts grouped into helices (`NESTED` for the canonical
  cloverleaf stems, `PK` for the pseudoknot) with `nbp`/`nbp_cov` per helix. `nbp_cov` is `0`
  everywhere here — expected, since covariation can't be measured from one sequence.
- `1ehz_A_1.1EHZ.A.dplot.{pdf,svg}` — dot-plot of the contact map (gnuplot output).
- `1ehz_A_1.1EHZ.A.R2R.sto.{pdf,svg}` — [R2R](https://sourceforge.net/projects/weinberg-r2r/)
  secondary-structure diagram rendered from the annotated Stockholm file.
- `1ehz_A_1.1EHZ.A.PDB.sto` — the input alignment with R-scape's derived `SS_cons` line(s) added,
  e.g. the cloverleaf plus the D-loop/T-loop pseudoknot contact on a separate `SS_cons_1` line.

## Takeaway

This is R-scape's PDB/RNAView path, not its covariation path: one structure in, contacts and a
secondary-structure annotation out, with `.hmm`/`.cm` as unavoidable Infernal build artifacts
rather than a deliberate modeling step. To actually see covariation (`nbp_cov > 0`, E-values,
power analysis) you need a real multi-sequence alignment — see
[`secondary-structure-covariation-and-annotation-with-rscape`](../secondary-structure-covariation-and-annotation-with-rscape)
for that.
