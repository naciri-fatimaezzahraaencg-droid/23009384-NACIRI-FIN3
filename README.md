[README (2).md](https://github.com/user-attachments/files/35437065/README.2.md)
# Étude des facteurs de risque d'un portefeuille d'actions

**F5 — Facteurs de risque d'un portefeuille** · Machine Learning en finance · S7 FIN / S7 CI · Groupe Fin3

**Étudiante :** Fatima-ezzahra Naciri · **Code Apogée :** 23009384 · **Date :** 17 novembre 2026

---

## Vue d'ensemble

Ce dépôt contient l'étude du sujet **F5** : la rentabilité mensuelle en excès
d'un portefeuille de **dix grandes entreprises américaines** (pondération
égale, rééquilibrage mensuel) est-elle expliquée par les **trois facteurs de
Fama et French** (marché, taille, valeur), ou subsiste-t-il un **alpha**
statistiquement significatif ?

**Réponse :** le modèle Fama-French à trois facteurs domine le CAPM, et
l'alpha estimé n'est pas significatif — la rentabilité s'explique par
l'exposition aux facteurs de risque, pas par une surperformance anormale.

## Résultats principaux

| Modèle | R² ajusté | RMSE test | AIC |
|---|---|---|---|
| Référence (moyenne seule) | 0,000 | 2,99 % | 744,6 |
| CAPM (1 facteur) | 0,606 | 2,63 % | 622,7 |
| **Fama-French (3 facteurs)** | **0,788** | **1,92 %** | **542,7** |

- Test F de modèles emboîtés : F = 56,91 ; p < 0,0001 → SMB et HML
  améliorent significativement le CAPM.
- Alpha : 0,057 % par mois ; IC à 95 % [−0,274 ; 0,389] ; p = 0,733 →
  non significatif.
- Bêtas : marché 0,753 ; SMB −0,265 (grandes capitalisations) ; HML 0,446
  (orientation valeur) — tous très significatifs.

## Structure du dépôt

```
23009384-NACIRI-FIN3/
├── README.md                            ← ce fichier
├── rapport/
│   └── rapport.pdf                      ← rapport écrit (9 pages)
├── notebooks/
│   ├── NACIRI_F5_3 (1).ipynb            ← notebook principal (analyse complète commentée)
│   └── NACIRI_F5_3.ipynb                ← notebook (version alternative)
├── src/
│   └── naciri_f5_3.py                   ← script Python reproductible
├── data/raw/
│   └── F-F_Research_Data_Factors.csv    ← facteurs Fama-French (mensuel)
└── docs/
    ├── Fiche_Sujet_F5.md                ← fiche détaillée du sujet
    ├── References.md                    ← références bibliographiques et sources
    └── Tp_ML (1).ipynb                  ← exploration des 29 algorithmes (Partie B)
```

## Données

- **Kenneth R. French Data Library** : facteurs mensuels Mkt-RF, SMB, HML
  et RF (usage académique, avec citation de la source).
- **Yahoo Finance** : cours de clôture ajustés des dix titres
  (XOM, CVX, JPM, JNJ, PFE, PG, WMT, KO, GE, T), récupérés avec `yfinance`.
- Échantillon final : 132 observations mensuelles, janvier 2015 à
  décembre 2025, aucune valeur manquante ni doublon.
- Variable cible : `Rp_exc = Portefeuille − RF`.

## Méthodologie

- **Algorithme** : régression linéaire multiple par moindres carrés
  ordinaires (MCO) — algorithme n° 1 de l'annexe A.
- **Modèles comparés** : Référence (moyenne seule) → CAPM → Fama-French 3F.
- **Découpage chronologique** : 75 % apprentissage (99 mois) / 25 % test
  (33 mois) — aucun mélange passé / futur.
- **Inférence robuste** : erreurs-types de Newey-West (3 retards),
  bootstrap de l'alpha (2 000 tirages, graine 42).
- **Diagnostics** : Breusch-Pagan (p = 0,089), Jarque-Bera (p = 0,019),
  Durbin-Watson (1,74), stabilité des coefficients par fenêtres glissantes
  de 36 mois.

## Reproduire l'étude

1. Disposer de **Python 3** (ou Google Colab).
2. Installer les bibliothèques :

   ```
   pip install numpy pandas matplotlib seaborn statsmodels scikit-learn requests yfinance
   ```

3. Vérifier le chemin du fichier des facteurs
   (`data/raw/F-F_Research_Data_Factors.csv`) dans le notebook.
4. Exécuter toutes les cellules dans l'ordre du notebook principal.
5. Vérifier les tableaux, les graphiques et les résultats statistiques.

La graine aléatoire du bootstrap est fixée à **42** pour la reproductibilité.

## Références principales

- Fama, E. F. et French, K. R. (1993). *Common risk factors in the returns
  on stocks and bonds*. Journal of Financial Economics, 33(1), 3–56.
- Newey, W. K. et West, K. D. (1987). *A simple, positive semi-definite,
  heteroskedasticity and autocorrelation consistent covariance matrix*.
  Econometrica, 55(3), 703–708.
- Seabold, S. et Perktold, J. (2010). *Statsmodels: Econometric and
  statistical modeling with Python*. Proceedings of the 9th Python in
  Science Conference.
- Kenneth R. French Data Library, Tuck School of Business, Dartmouth College.
- Yahoo Finance.

Liste complète dans `docs/References.md`.

## Limites

Portefeuille limité à dix titres · biais de survie · coûts de transaction
non intégrés · scissions GE et AT&T affectant la comparabilité des cours ·
trois facteurs seulement (momentum et rentabilité non modélisés) ·
coefficients non parfaitement stables dans le temps.

## Déclaration

Données : Kenneth R. French Data Library et Yahoo Finance. Traitement et
analyse réalisés avec Python et ses bibliothèques statistiques et
graphiques. Toute assistance par intelligence artificielle utilisée pour la
rédaction ou la structuration est déclarée conformément aux consignes de
l'établissement.
