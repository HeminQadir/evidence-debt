# Reproducing the draft

From the repository root (Python 3.10+):

```bash
python -m pip install -r requirements.txt
python -m unittest discover -s tests -v
python -m src.evidence_debt --reps 400 --seed 2027 --n 6000 --out results
python -m src.sensitivity
python -m src.make_figures
(cd paper && pdflatex -interaction=nonstopmode -halt-on-error main.tex && pdflatex -interaction=nonstopmode -halt-on-error main.tex)
```

The research document is a preliminary two-column PDF, not official ICML 2027 formatting.
All simulated outcomes are artificial. Do not interpret the results as clinical validation.

## Publishing to an empty GitHub repository

Create an empty repository on GitHub first, then from this directory:

```bash
git init
git add .
git commit -m 'Add reproducible Evidence Debt research prototype'
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_NEW_REPO.git
git push -u origin main
```

For anonymous conference review, follow the official conference instructions for anonymous code repositories and remove identifying account details.
