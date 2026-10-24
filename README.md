# Analyse et modélisation des séries temporelles : exportations du Maroc (ARIMA, EViews)

> Application de la méthode de Box-Jenkins à la série des exportations de biens et services du Maroc (2000-2025) : stationnarité, identification, estimation, diagnostic des résidus et prévision jusqu'en 2030.

Projet académique réalisé dans le cadre du module **Économétrie** (Pr. Soumaya Fellaji), Master Intelligence Artificielle pour l'Économie Numérique et la Gestion, Faculté des Sciences Juridiques, Économiques et Sociales de Tanger, Université Abdelmalek Essaâdi.

**Équipe :** Wiam Chentouf, Raouia Benajiba, Ferdaous Attioui, Fatima Rafiai, Imane Naaim, Ibtissam Bakkali Yedri

## Données

| | |
|---|---|
| Série | Exports of Goods and Services for Morocco (`MARBXUSD`) |
| Fréquence | annuelle |
| Période | 2000 à 2025 (26 observations) |
| Unité | dollars US courants |
| Source | FRED (Federal Reserve Bank of St. Louis) |
| Fichier | `data_projet_eco.xlsx` (feuille `Annual`, colonnes `observation_date` et `MARBXUSD`) |

Les exportations passent d'environ 7,9 milliards de dollars en 2000 à environ 68,2 milliards en 2025.

## Contenu du projet

### Partie théorique

- Processus TS (Trend Stationary) et DS (Difference Stationary), lien avec les modèles AR, MA et ARIMA
- Stationnarité, test de Dickey-Fuller augmenté (ADF), transformations (logarithme, différenciation)
- Principe de parcimonie et critères de sélection (AIC, BIC), mesures de qualité de prévision (MAE, RMSE, MAPE)
- Hétéroscédasticité, modèles ARCH et GARCH, différence entre les deux
- Test de normalité de Jarque-Bera
- Caractéristiques des séries financières : queues épaisses (*fat tails*) et volatilité par grappes

### Partie pratique

Étude de la série `MARBXUSD` (voir section Données), réalisée sous **EViews**.

| Étape | Démarche |
|---|---|
| 1. Série brute (EBS) | Analyse graphique, corrélogramme, test ADF |
| 2. Transformation logarithmique (LOG_EBS) | Stabilisation de la variance, nouveau test ADF |
| 3. Différenciation première D(LOG_EBS) | Corrélogramme et ADF, série stationnaire I(1) |
| 4. Identification et estimation | Modèle ARIMA(0,1,0) avec dérive |
| 5. Diagnostic des résidus | Ljung-Box, Jarque-Bera, ARCH-LM |
| 6. Prévision | Prévision jusqu'en 2030 |

## Résultats principaux

### Tests de stationnarité (ADF)

| Série | Spécification | Statistique t | p-value | Conclusion |
|---|---|---|---|---|
| EBS (niveau) | constante et tendance | -1,793 | 0,6775 | racine unitaire non rejetée |
| LOG_EBS (niveau) | constante et tendance | -2,584 | 0,2895 | racine unitaire non rejetée |
| D(LOG_EBS) | constante | -4,281 | 0,0030 | stationnaire, la série est I(1) |

### Modèle retenu : ARIMA(0,1,0) avec dérive

```
ΔLOG_EBS(t) = c + ε(t)          avec c ≈ 0,0863 (p = 0,0024)
```

La constante estimée correspond à une croissance moyenne d'environ 9 % par an des exportations.

### Diagnostic des résidus

| Test | Résultat | Interprétation |
|---|---|---|
| Ljung-Box (corrélogramme des résidus) | p-values entre 0,182 et 0,758 | pas d'autocorrélation, résidus assimilables à un bruit blanc |
| Jarque-Bera | 2,048 (p = 0,359) | normalité non rejetée |
| ARCH-LM | p = 0,5988 | pas d'effet ARCH |
| Durbin-Watson | 1,88 | pas d'autocorrélation d'ordre 1 |

### Prévision (2000-2030)

| Indicateur | Valeur |
|---|---|
| RMSE | 0,348 |
| MAE | 0,277 |
| MAPE | 1,15 % |
| Coefficient d'inégalité de Theil | 0,007 |

La prévision indique une poursuite de la tendance haussière de LOG_EBS jusqu'en 2030.

## Limites

- Seulement **26 observations annuelles** : l'estimation et les tests ont une puissance limitée.
- Un ARIMA(0,1,0) avec dérive est une marche aléatoire avec dérive : la prévision est une droite de tendance et ne capte aucune dynamique conjoncturelle (chocs de 2009 et 2020 par exemple).
- Les indicateurs d'erreur (RMSE, MAE, MAPE) sont calculés sur la série en **logarithme**, ce qui rend le MAPE mécaniquement très faible. Une évaluation hors échantillon (*train / test*) serait plus informative.
- Pistes d'amélioration : comparer avec d'autres spécifications (ARIMA(1,1,0), ARIMA(0,1,1)), ajouter des variables explicatives, évaluer la prévision hors échantillon.

## Outils

EViews (tests ADF, corrélogrammes, estimation, tests de diagnostic, prévision).

## Contenu du dépôt

- `Projet_d_économétrie222.pdf` : rapport complet (partie théorique et pratique)
- `data_projet_eco.xlsx` : données de la série `MARBXUSD`
- `README.md` : ce fichier

## Contact

Fatima Rafiai · fatimarafiai0101@gmail.com · Tanger, Maroc
