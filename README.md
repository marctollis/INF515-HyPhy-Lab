# Lab: Detecting episodic selection in HIV-1 env

**INF415 / INF515 • Comparative Genomics**

How can we distinguish evidence of selection across a gene, along a branch, and at a codon? In this lab you will use three HyPhy analyses through [Datamonkey](https://www.datamonkey.org/): **BUSTED → aBSREL → MEME**. No software installation is required. Allow approximately 45–60 minutes for analysis and interpretation; server queues can add time.

## Biological context

The [HyPhy selection tutorial](https://github.com/veg/hyphy-tutorials/blob/master/docs/selection/README.md) describes these partial HIV-1 env sequences as viral clones from an epidemiologically linked source–recipient pair. D20 labels identify source sequences and R20 labels identify recipient sequences. Tips represent sampled viral sequences, not different people. The tutorial calls the stem leading to the R20 clade the transmission branch. It spans evolutionary history associated with transmission; it does not directly observe the transmission event or prove a transmission-adaptation mechanism.

The example lets us investigate variation in selection across evolutionary history using a documented positive teaching example.

## Learning objectives

By the end of this lab you should be able to:

- Explain dN/dS (omega) as nonsynonymous substitutions per nonsynonymous site relative to synonymous substitutions per synonymous site.
- Distinguish gene-wide, branch-level, and codon-level hypotheses.
- Run the three methods using a consistent alignment and supplied phylogeny.
- Interpret likelihood-ratio tests, corrected branch p-values, and uncorrected site p-values.
- Explain why evidence of selection does not by itself establish its functional cause.

Values below, near, or above omega = 1 are conventionally associated with purifying selection, neutrality, or diversifying selection under the model. A point estimate alone is not a significance test. Averaging across branches and codons can conceal episodic selection.

## Files and preparation

Download [HIV.nex](data/HIV.nex) using GitHub's **Download raw file** control, or download and unzip the repository. Save the actual NEXUS text, not the GitHub webpage. It contains both the alignment and tree; no concatenation is needed.

The source has **16 entries × 864 nucleotides = 288 codons**, with **13 distinct sequences**. Identical source groups are D20_235/D20_236/D20_232 and D20_234/D20_237. Our Datamonkey runs retained 13 entries and tested 21 branches. Record your own counts; duplicate handling and software versions may change them.

Read the [Canvas quiz instructions](ASSESSMENT.md) before beginning. The Canvas quiz is the sole submission; no response document, run log, JSON files, annotated tree, spreadsheet, or screenshot is required. Download and keep the three result JSON files and take brief notes for your quiz responses. Automatically graded result questions use the supplied reference results; report your own run in the short-response item and identify any reference use.

## Keep a copy of your results

After each analysis, use the result page’s export/download control to save the **JSON results**, named `HIV_BUSTED.json`, `HIV_aBSREL.json`, and `HIV_MEME.json`. Do not rely on job-page links remaining available.

To revisit an analysis, open [HyPhy Vision](https://vision.hyphy.org/), choose the matching method if prompted, and load its saved JSON file. This displays the saved analysis; it does not rerun the test. You can also use the supplied reference JSONs this way. **Keep these files for yourself; the Canvas quiz remains the only submission.**

## Part 1 — BUSTED: Is there evidence anywhere in the gene?

**Canvas video 1: Context and BUSTED (4–5 minutes).**

Question: Is there evidence that at least one codon experienced episodic diversifying selection on at least one tested branch?

1. At Datamonkey, open **Methods and Tools → BUSTED** and upload HIV.nex.
2. The uploaded NEXUS file already contains the tree. On the upload form, leave **Genetic Code → Universal code** selected. If a tree-choice control appears later, keep **User Defined Tree** selected.
3. In the branch-selection screen choose **Selection → All**. Confirm that all branches are highlighted, then save the branch selection.
4. For this pilot, BUSTED used synonymous rate variation enabled, multiple hits set to None, and error-sink disabled. Match these if exposed; otherwise record the settings reported in the output.
5. After saving the branch selection, allow the analysis to finish. Read the BUSTED summary statement and its p-value. Decide whether the result is significant at alpha = 0.05.
6. Download the BUSTED JSON for your own records, and note the reported p-value and your conclusion for the Canvas quiz. Our setup tests **all branches**; this describes the analysis you requested, not a separate branch-specific BUSTED result. You do not need to find or report the LRT statistic.

A significant result supports selection somewhere among the tested branches and codons. It does not identify particular branches or codons.

## Part 2 — aBSREL: Which branches show evidence?

**Canvas video 2: aBSREL (3–4 minutes).**

1. Start aBSREL and upload the same HIV.nex.
2. Use the same genetic code and supplied tree. Select **all branches**, save the selection, and submit. Record any other options.
3. Read the branch-results table. Record the branch names and reported test p-values for branches meeting the 0.05 significance threshold. For this all-branches aBSREL analysis, the reported test p-values account for multiple testing.
4. Locate each branch on the tree. Identify internal branches by their descendant tips as well as node names; node numbering can change when duplicates are removed.
5. Download the aBSREL JSON for your own records and record the branch results in your quiz notes. Use the displayed tree to identify the branches.

The summary's “p ≤ 0.05” states the cutoff, not the observed p-value of every branch. Large omega estimates, particularly with very small mixture proportions or few synonymous changes, should not be treated as precise biological effect sizes.

## Part 3 — MEME: Which codons show evidence?

**Canvas video 3: MEME (3–4 minutes).**

1. Start MEME with the same HIV.nex, standard code, and supplied tree.
2. MEME in this Datamonkey interface has **no branch-selection step**. Keep two rate classes and no multiple-hit model if exposed, matching the pilot.
3. Submit, then inspect the site-results table.
4. For this exercise use an **uncorrected per-site p ≤ 0.05**. If the display begins at 0.10, change its display threshold to 0.05. Record codon positions and p-values. Then compare the number of candidates at 0.10.
5. Download the MEME JSON for your own records and record the requested codon results in your quiz notes.

These are candidate codons at the stated per-site threshold. Testing 288 sites creates a multiple-testing problem; these p-values are not equivalent to aBSREL's corrected branch p-values. For INF515, apply Benjamini–Hochberg correction across ALL 288 site tests at FDR 0.05, including nonsignificant sites.

MEME identifies candidate codons across the tree. It does not establish that those codons were selected specifically on the branches identified by aBSREL.

## Canvas quiz and submission

Complete the **HyPhy lab quiz in Canvas**, following [ASSESSMENT.md](ASSESSMENT.md). INF415 completes the 30-point core. INF515 completes the same core plus two BH questions worth 5 points, for 35 points total. This quiz is the only submission.

If a live job fails or differs from the reference, explain that in the run-record short response. The reference questions use a fixed dataset/result set so numerical variation will not be penalized.

## INF515 extension — BH correction (required, 5 points)

The optional Canvas BH video (2–3 minutes) supports this required extension. No extreme-omega or follow-up-design questions are required.

**Benjamini–Hochberg correction:** use the supplied [MEME codon p-values CSV](data/MEME_codon_pvalues.csv), extracted from the reference JSON. It includes all 288 codons with unrounded p-values in alignment order. This is reference data; label it as such if you use it instead of your own run.

1. Open the CSV in Excel or import it into Google Sheets. Column A contains alignment_codon and column B contains p_value.
2. Sort the **entire table**, including both columns, by column B from smallest to largest. Keep the header row at the top.
3. In C1 enter `rank`, in D1 enter `BH_critical_value`, and in E1 enter `meets_criterion`.
4. In C2 enter `=ROW()-1`, in D2 enter `=C2*0.05/288`, and in E2 enter `=B2<=D2`. Fill C2:E2 down through row 289.
5. Find the **largest rank** with TRUE in column E. Retain every site from rank 1 through that rank, even if an earlier row is FALSE. If no row is TRUE, retain no sites.
6. Report the number retained and explain how it differs from using an uncorrected per-site cutoff of 0.05. Keep codon identifiers attached to their p-values throughout.

This is the **Benjamini–Hochberg (BH) procedure**, which controls the false discovery rate. Its threshold increases with rank: **rank × 0.05 / 288**. By comparison, **Bonferroni** uses the same threshold for every test, **0.05 / 288 ≈ 0.000174**, to control the probability of at least one false positive across the tests.

These formulas calculate BH decision thresholds, not adjusted p-values. If using a different run, include all site tests and replace 288 with its actual number of tests. A filtered table of significant sites alone is insufficient.

## Sources

See [SOURCES.md](SOURCES.md) for attribution, method references, and provenance. This course adaptation uses current pilot outputs rather than the older tutorial's expected numerical values. The instructor’s short videos will be recorded in **Kaltura** and embedded in the lab’s **Canvas module**, in this order:

| Video | Coverage | Target length |
|---|---|---:|
| 1. Context and BUSTED | HIV dataset, gene-wide hypothesis, upload, all-branch selection, and results | 4–5 minutes |
| 2. aBSREL | Branch-level hypothesis, all-branch selection, corrected p-values, and tree interpretation | 3–4 minutes |
| 3. MEME | Codon-level hypothesis, setup without a branch-selection step, thresholds, and limitations | 3–4 minutes |
| Optional INF515: BH correction | Spreadsheet demonstration using all 288 MEME p-values | 2–3 minutes |

Watch each video alongside the corresponding written section. The complete procedure is provided here so you can complete the lab without the videos. Videos are delivered through Canvas.
