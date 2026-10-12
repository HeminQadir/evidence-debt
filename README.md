# Evidence Debt: An Auditing-Based Research Prototype

**Status: preliminary research manuscript; synthetic experiments only. Not clinically validated, not a submitted/accepted ICML paper.**

This is a reproducible prototype for **budgeted independent verification of deployed clinical prediction systems** under selective labeling. The method selects labels with positive probability without seeing current outcomes, estimates subgroup false-negative risk from randomized audits, and attaches time-uniform confidence sequences for a frozen classifier in a stationary population.

## Reproduce

```bash
python -m pip install -r requirements.txt
python -m unittest discover -s tests -v
python -m src.evidence_debt --reps 400 --seed 2027 --n 6000 --out results
python -m src.sensitivity
python -m src.make_figures
```

Read `results/summary.json`, `results/replicates.csv`, and `figures/benchmark.png`. Main paper source is `paper/main.tex`; build using `pdflatex main.tex` twice in `paper/` (the final formatted PDF is supplied separately). The present paper is **not** set in an official ICML 2027 template, which must be downloaded when published.

## Assumptions and reproducibility boundaries

* Patient records are **synthetic**. No real clinical data is used.
* The prediction rule is held fixed, subgroup outcomes are iid and subgroup audits do not condition on current unobserved outcomes. The inferential theorem does not cover adaptive treatment effects, outcome drift, policy revisions, or audit decisions driven by unmeasured outcome proxies.
* Clinically obtained labels in the simulation are missing not at random, by construction. Randomized audits do not depend on the current label.
* The audit allocator uses a pilot from the first 20% of chronological arrivals and retrospective group counts. Deployment would require prospective arrival-count estimates and clinical verification consent, ethics review, and resource constraints.
* Simulation results are for estimating a *static* risk, not a clinically actionable guarantee or a claim of superiority on patient datasets.
* The code reports cohort-risk absolute errors but checks confidence-sequence coverage against the known population subgroup risks.

## Repository contents

- `src/evidence_debt.py`: simulator, pilot-based minimax allocator, benchmark.
- `src/make_figures.py`: reproducible plots.
- `src/sensitivity.py`: independently seeded audit-budget sweep.
- `tests/`: smoke tests.
- `results/`: seeded simulation output.
- `paper/main.tex`: seven-page research manuscript.

## Integrity

The term *evidence debt* is a **proposed framing** rather than a verified unique invention. Claims of ICML acceptance, clinical efficacy, optimal dynamic allocation or clinical deployment are **not made**. Prior art and proofs require independent expert review before submission.
