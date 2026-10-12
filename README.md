# 🚌 Prédiction d'Affluence sur les Lignes de Bus (San Sebastián)

Projet tutoré de Machine Learning réalisé dans le cadre de l'année académique **2024-2025** à l'**ESTIA Institute of Technology**.

## 👥 Auteurs

* **Konan Ella Angèle Mélaine**
* **Yeo Foungnigue Samuel**

---

## 📋 Contexte et Objectif du Projet

Les transports publics jouent un rôle crucial dans la mobilité urbaine. Ce projet vise à développer des modèles prédictifs permettant d'anticiper l'affluence des passagers sur les lignes de bus de **San Sebastián** avec une **anticipation de 3 jours**.

L'objectif est d'aider la compagnie de transport à ajuster sa flotte (134 bus dont 38 hybrides et 3 électriques) pour optimiser les ressources, améliorer la satisfaction des usagers et minimiser l'empreinte écologique.

---

## 📂 Structure du Jeu de Données

Le jeu de données historique s'étend du 5 avril 2019 au 8 mars 2023 (36 901 observations) et comprend :

* `dateTime` : Date de l'observation.
* `lineNumber` : Identifiant des 39 lignes de bus.
* `lineType` : Type de ligne (journalière ou nocturne).
* `weather` : Conditions météorologiques.
* `passengersNumber` : Nombre de passagers (variable cible initiale).

---

## ⚙️ Feature Engineering & Prétraitement

Pour améliorer la performance des modèles, plusieurs transformations et nouvelles variables ont été créées :

* **Variables temporelles** : Jour de la semaine, jour du mois, jour de l'année, indicateur de week-end.
* **Variables contextuelles & Événements** : Jours fériés (vacances scolaires zone A), Pâques, et la *Semana Grande*.
* **Variables météo** : Regroupement de la météo en 5 grandes classes.
* **Lags temporels** : Passagers des jours précédents (7, 14, 21 jours) et création de la cible principale : `passengersNumber_+3_Days` (affluence à 3 jours).

---

## 🤖 Modèles Implémentés

Cinq approches de Machine Learning ont été testées et comparées :

1. **XGBoost** (avec optimisation par `RandomizedSearchCV`)
2. **LightGBM** (avec gestion des variables catégoriques)
3. **Random Forest** (avec optimisation par `GridSearchCV`)
4. **Stacking** (combinant les modèles ensemblistes avec une Régression Linéaire en méta-modèle)
5. **Régression Linéaire** (utilisée comme modèle de référence / baseline)

---

## 📊 Résultats et Performances

Le choix de la métrique principale s'est porté sur le **MAE (Mean Absolute Error)**, qui traduit directement l'erreur moyenne en nombre de passagers sans pénaliser excessivement les valeurs extrêmes.

| Modèles | MSE | RMSE | MAE | $R^2$ |
| :--- | :---: | :---: | :---: | :---: |
| **LightGBM** | 144 138,3 | 379,66 | **204,65** | **0,9769** |
| **XGBoost** | 150 811,1 | 388,34 | 215,73 | 0,9758 |
| **Stacking** | 267 811,9 | 517,51 | 301,00 | 0,9570 |
| **Random Forest** | 360 190,4 | 600,16 | 322,94 | 0,9422 |
| **Régression Linéaire** | 1 217 901,0 | 1 103,59 | 653,92 | 0,8046 |

### 🏆 Conclusion

Les modèles **LightGBM** et **XGBoost** se distinguent nettement avec des scores $R^2$ supérieurs à **97%**, prouvant leur efficacité pour capturer la complexité des dynamiques temporelles et l'affluence du réseau de transport.
