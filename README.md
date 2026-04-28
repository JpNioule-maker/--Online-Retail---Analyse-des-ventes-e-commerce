# 🛒 Online Retail — Analyse des ventes e-commerce

> Projet collectif réalisé dans le cadre du M2 Data Analytics (2026)  
> **Équipe :** Yasmine · Chaimaa · Juan David Gutierrez · Rayane · Jean Philippe

---

## 📌 Objectif

Analyser les données transactionnelles d'un site e-commerce (Online Retail Dataset) afin de :
- Produire des **indicateurs de performance clés** (CA par pays, saisonnalité, top produits)
- Appliquer des **tests statistiques formels** (ANOVA, régression linéaire multiple)
- Réaliser une **segmentation client** par clustering K-means (approche RFM)
- Formuler des **recommandations marketing actionnables**

---

## 📊 Dataset

| Caractéristique | Valeur |
|---|---|
| Source | [UCI Machine Learning Repository — Online Retail](https://archive.ics.uci.edu/ml/datasets/Online+Retail) |
| Période | Décembre 2010 – Décembre 2011 |
| Lignes brutes | ~541 000 transactions |
| Après nettoyage | ~392 000 lignes valides |
| Clients distincts | 4 339 |
| Commandes uniques | 18 536 |
| Produits distincts | 3 665 |

---

## 🔧 Stack technique

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![pandas](https://img.shields.io/badge/pandas-Data%20Wrangling-150458?logo=pandas)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange?logo=scikit-learn)
![statsmodels](https://img.shields.io/badge/statsmodels-Stats-green)
![matplotlib](https://img.shields.io/badge/matplotlib-Viz-blue)
![seaborn](https://img.shields.io/badge/seaborn-Viz-9cf)

---

## 📁 Structure du projet

```
online-retail-analysis/
│
├── Online_Retail.xlsx          # Dataset source
├── notebook_analyse.ipynb      # Notebook principal (toutes les analyses)
├── rapport_final.pdf           # Rapport synthétique (10 pages)
└── README.md
```

---

## 🔍 Analyses réalisées

### 1. Préparation des données
- Suppression des lignes sans `CustomerID`
- Suppression des transactions annulées (`InvoiceNo` commençant par `C`)
- Conversion des types (`InvoiceDate` → datetime, `CustomerID` → string)
- Création de la variable `TotalPrice = Quantity × UnitPrice`

### 2. Analyse exploratoire (EDA)
- CA par pays : domination du Royaume-Uni (>7,2M€), potentiel international identifié
- Top 10 produits par volume et par CA
- Saisonnalité : pics en novembre–décembre, jours porteurs = jeudi & mardi
- Heatmap horaire : activité concentrée entre 8h et 17h en semaine (clientèle B2B)

### 3. Statistiques descriptives & corrélations
- Forte corrélation Quantity ↔ TotalPrice (r = 0,91)
- UnitPrice quasi indépendant de la quantité achetée (r ≈ 0)

### 4. ANOVA — Impact du pays sur le montant des commandes
- **H₀ :** Le montant moyen des commandes ne diffère pas selon les pays
- **Résultat :** F = 12,21 — p-value = 8,10 × 10⁻⁷¹ → **H₀ rejetée**
- Le pays est un facteur discriminant significatif du comportement d'achat

### 5. Régression linéaire multiple
- **Variable cible :** TotalPrice
- **Variables explicatives :** Quantity, UnitPrice, Pays (dummies), Jour de la semaine
- **R² = 83,3 %** — la quantité achetée est le principal levier du CA
- ⚠️ Résidus non-normaux (skewness = 82,67) en raison de commandes en gros — coefficients interprétables avec précaution

### 6. Segmentation client K-means (RFM enrichi)
Indicateurs construits par client : **Récence · Fréquence · Valeur monétaire · Quantité totale**

| Cluster | Profil | Récence | Fréquence | Valeur | Stratégie |
|---|---|---|---|---|---|
| 1 | Champions | Très faible | Très élevée | Très élevée | Programme VIP |
| 3 | Fidèles | Faible | Élevée | Élevée | Fidélisation |
| 0 | Moyens | Modérée | Modérée | Modérée | Cross-sell / Up-sell |
| 2 | À risque | Très élevée | Faible | Faible | Réactivation |

Nombre de clusters optimal : **k = 4** (méthode du coude)

---

## 💡 Recommandations clés

1. **Programme VIP** pour les Clusters 1 & 3 (offres exclusives, service dédié)
2. **Cross-selling** ciblé pour le Cluster 0 — principal réservoir de croissance
3. **Campagne de réactivation** (remise 20%) pour le Cluster 2
4. **Intensification marketing en octobre** pour anticiper les pics de novembre–décembre
5. **Stratégie d'internationalisation** vers les Pays-Bas, l'Allemagne et la France

---

## ▶️ Lancer le notebook

```bash
# Cloner le repo
git clone https://github.com/votre-username/online-retail-analysis.git
cd online-retail-analysis

# Installer les dépendances
pip install pandas matplotlib seaborn scikit-learn statsmodels openpyxl

# Lancer Jupyter
jupyter notebook notebook_analyse.ipynb
```

Ou directement sur Google Colab :  
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/18vKRla5exyzTEduXY7qOiJRw7qKesD5Z?usp=sharing)

---

## 👥 Équipe

| Nom | Contribution principale |
|---|---|
| Yasmine | EDA & Visualisations |
| Chaimaa | Préparation des données |
| Juan David Gutierrez | Régression & ANOVA |
| Rayane | Clustering K-means |
| Jean Philippe | Rapport & Recommandations |

---

*Projet académique — M2 Data Analytics, 2026*
