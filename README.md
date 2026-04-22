# Analyse du trafic aérien en France - Modélisation SARIMA

Projet d'analyse de séries temporelles portant sur la fréquentation mensuelle des passagers aériens en France de 1994 à 2019, réalisé dans le cadre du Master MAS (Mathématiques Appliquées et Statistiques).

---

## Objectif

Analyser les composantes structurelles de la série (tendance, saisonnalité, ruptures) et modéliser la dynamique de fréquentation afin de produire une prévision contrefactuelle pour 2020-2021, c'est-à-dire estimer la trajectoire du trafic aérien en l'absence de la crise Covid-19.

---

## Données

Source : INSEE — [Série 010001977](https://www.insee.fr/fr/statistiques/serie/010001977)

La série couvre 312 observations mensuelles de janvier 1994 à décembre 2019. Elle porte sur le nombre total de passagers transitant par les aéroports français (vols intérieurs et internationaux). La période post-2019 est exclue en raison du choc exogène exceptionnel lié au Covid-19.


---

## Méthodologie

Le projet suit la démarche classique d'analyse de séries temporelles.

**Analyse exploratoire** : visualisation de la série, identification du schéma multiplicatif, transformation logarithmique pour stabiliser la variance.

**Décomposition** : isolation des composantes de tendance et de saisonnalité. Désaisonnalisation par décomposition additive appliquée à la série transformée.

**Tests de stationnarité** : procédure séquentielle ADF, test de Phillips-Perron et test KPSS appliqués à la série log désaisonnalisée. Conclusion : série intégrée d'ordre 1, processus DS.

**Tests de rupture** : test de Perron avec variables indicatrices sur les ruptures de 2001 (attentats du 11 septembre) et 2009 (crise financière), confirmées comme hautement significatives.

**Modélisation** : sélection d'un modèle SARIMA via la procédure `auto.arima`, avec d=1 et D=1 (double différenciation). Diagnostic des résidus (test de Ljung-Box, ACF des résidus, normalité).

**Prévision** : projection sur 24 mois avec intervalles de confiance, retransformée en niveau pour interprétation.

---

## Résultats principaux

La série suit un processus DS avec deux ruptures structurelles significatives en 2001 et 2009. Le modèle SARIMA retenu produit des résidus qui se comportent comme un bruit blanc, et reproduit fidèlement la saisonnalité estivale observée. Il surpasse le modèle Holt-Winters sur le critère de diagnostic des résidus.

---

## Prérequis

R version 4.0 ou supérieure, avec les packages suivants :

```r
install.packages(c("xts", "dplyr", "readxl", "forecast", "ggplot2",
                   "astsa", "ggfortify", "fpp2", "urca", "tseries",
                   "knitr", "kableExtra"))
```
