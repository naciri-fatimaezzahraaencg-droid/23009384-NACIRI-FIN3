[README(1).md](https://github.com/user-attachments/files/35436769/README.1.md)
# Étude des facteurs de risque d'un portefeuille d'actions

**F5 — Facteurs de risque d'un portefeuille** · Machine Learning en finance · S7 FIN / S7 CI · Groupe Fin3

**Étudiante :** Fatima-ezzahra Naciri · **Code Apogée :** 23009384 · **Date :** 17 novembre 2026

---

## 📌 Vue d'ensemble

Ce dépôt contient l'étude complète du sujet **F5** : la rentabilité mensuelle
en excès d'un portefeuille de **dix grandes entreprises américaines**
(pondération égale, rééquilibrage mensuel) est-elle expliquée par les
**trois facteurs de Fama et French** (marché, taille, valeur), ou subsiste-t-il
un **alpha** statistiquement significatif ?

**Réponse courte :** le modèle Fama-French à trois facteurs domine le CAPM
(R² ajusté **0,788** contre 0,606 ; RMSE de test **1,92 %** contre 2,63 %) et
l'alpha estimé (0,057 %/mois, p = 0,733) n'est **pas significatif** — la
rentabilité s'explique par l'exposition aux facteurs de risque, pas par une
surperformance anormale.

| Modèle | R² ajusté | RMSE test | AIC |
|---|---|---|---|
| Référence (moyenne seule) | 0,000 | 2,99 % | 744,6 |
| CAPM (1 facteur) | 0,606 | 2,63 % | 622,7 |
| **Fama-French (3 facteurs)** | **0,788** | **1,92 %** | **542,7** |

## 🗂️ Structure du dépôt

```
23009384-NACIRI-FIN3/
├── README.md                       ← ce fichier
├── Presentation_F5_3_Naciri_LaTeX.pdf   ← présentation de soutenance (LaTeX Beamer)
├── Presentation_F5_3_Naciri.pdf         ← présentation de soutenance (version originale)
├── index.html                      ← page de téléchargement des PDF
├── .github/workflows/compile-latex.yml  ← compilation automatique du PDF LaTeX
│
├── rapport/
│   └── rapport.pdf                 ← rapport écrit (9 pages)
│
├── notebooks/
│   ├── NACIRI_F5_3 (1).ipynb       ← notebook principal (analyse complète commentée)
│   └── NACIRI_F5_3.ipynb           ← notebook (version alternative)
│
├── src/
│   └── naciri_f5_3.py              ← script Python reproductible
│
├── data/raw/
│   └── F-F_Research_Data_Factors.csv   ← facteurs Fama-French (Kenneth R. French Data Library)
│
├── latex/                          ← source LaTeX Beamer de la présentation
│   ├── Presentation_F5_3.tex
│   ├── figures/                    ← 7 graphiques issus du notebook
│   └── Presentation_F5_3_LaTeX.zip ← archive prête pour Overleaf
│
├── presentation/
│   ├── build_presentation.py       ← script de génération (version ReportLab)
│   └── figures/
│
└── docs/
    ├── Fiche_Sujet_F5.md           ← fiche détaillée du sujet F5
    ├── References.md               ← références bibliographiques et sources
    └── Tp_ML (1).ipynb             ← exploration des 29 algorithmes (Partie B)
```

## 🔬 Méthodologie

- **Algorithme** : régression linéaire multiple par moindres carrés ordinaires
  (MCO) — algorithme n° 1 de l'annexe A.
- **Modèles comparés** : Référence (moyenne seule) → CAPM → Fama-French 3F.
- **Données** : facteurs mensuels Fama-French (Kenneth R. French Data Library)
  et cours ajustés Yahoo Finance (`yfinance`) → 132 mois, janvier 2015 à
  décembre 2025.
- **Découpage chronologique** : 75 % apprentissage (99 mois) / 25 % test
  (33 mois) — aucun mélange passé/futur.
- **Inférence robuste** : erreurs-types de Newey-West (3 retards), bootstrap
  de l'alpha (2 000 tirages, graine 42).
- **Diagnostics** : Breusch-Pagan (p = 0,089), Jarque-Bera (p = 0,019),
  Durbin-Watson (1,74), fenêtres glissantes de 36 mois.

## 🚀 Reproduire l'étude

1. Disposer de **Python 3** (ou Google Colab).
2. Installer les dépendances :

   ```bash
   pip install numpy pandas matplotlib seaborn statsmodels scikit-learn requests yfinance
   ```

3. Vérifier le chemin du fichier des facteurs
   (`data/raw/F-F_Research_Data_Factors.csv`) dans le notebook.
4. Exécuter toutes les cellules dans l'ordre (`notebooks/NACIRI_F5_3 (1).ipynb`).
5. Vérifier les tableaux, graphiques et résultats statistiques.

> La graine aléatoire du bootstrap est fixée à **42** pour la reproductibilité.

## 🖥️ Recompiler la présentation LaTeX

Le PDF LaTeX est recompilé automatiquement par GitHub Actions à chaque
modification de `latex/` (workflow `.github/workflows/compile-latex.yml`) —
le PDF compilé est committé à la racine du dépôt.

En local :

```bash
cd latex
latexmk -pdf Presentation_F5_3.tex   # ou : pdflatex (2 passes)
```

Ou en ligne : importer `latex/Presentation_F5_3_LaTeX.zip` dans
[Overleaf](https://www.overleaf.com) (compilateur pdfLaTeX).

## 📥 Télécharger les présentations

| Fichier | Description |
|---|---|
| [`Presentation_F5_3_Naciri_LaTeX.pdf`](Presentation_F5_3_Naciri_LaTeX.pdf) | Version LaTeX Beamer — 16 pages (12 diapositives + notes orateur) |
| [`Presentation_F5_3_Naciri.pdf`](Presentation_F5_3_Naciri.pdf) | Version originale — 14 pages |

## 📚 Références principales

- Fama, E. F. & French, K. R. (1993). *Common risk factors in the returns on
  stocks and bonds*. Journal of Financial Economics, 33(1), 3–56.
- Newey, W. K. & West, K. D. (1987). *A simple, positive semi-definite,
  heteroskedasticity and autocorrelation consistent covariance matrix*.
  Econometrica, 55(3), 703–708.
- Seabold, S. & Perktold, J. (2010). *Statsmodels: Econometric and statistical
  modeling with Python*. Proc. of the 9th Python in Science Conference.
- Kenneth R. French Data Library : https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/
- Yahoo Finance : https://finance.yahoo.com

Liste complète : [`docs/References.md`](docs/References.md) ·
Fiche du sujet : [`docs/Fiche_Sujet_F5.md`](docs/Fiche_Sujet_F5.md)

## ⚠️ Limites

Portefeuille limité à dix titres · biais de survie · coûts de transaction non
intégrés · scissions GE/AT&T affectant la comparabilité des cours · trois
facteurs seulement (momentum, rentabilité non modélisés) · coefficients non
parfaitement stables dans le temps.

## 🛡️ Déclaration

Données : Kenneth R. French Data Library et Yahoo Finance. Traitement et
analyse réalisés avec Python et ses bibliothèques statistiques et graphiques.
Toute assistance par intelligence artificielle utilisée pour la rédaction ou
la structuration est déclarée conformément aux consignes de l'établissement.
