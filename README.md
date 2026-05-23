# Prédiction du succès d'une campagne marketing bancaire

Projet de **Data Science appliquée au marketing bancaire** visant à prédire la souscription à un produit d’épargne et à améliorer le ciblage des campagnes téléphoniques.

L’objectif n’est pas seulement de construire un bon modèle, mais de répondre à une question métier concrète :

> **Quels clients contacter en priorité pour maximiser les conversions tout en maîtrisant le coût des campagnes ?**

---

## Objectif

Ce projet repose sur le **Bank Marketing Dataset** et combine :

- une **analyse exploratoire complète** des données ;
- une **préparation rigoureuse** des variables ;
- la comparaison de plusieurs modèles de classification ;
- une réflexion sur le **compromis métier précision / rappel** ;
- une **segmentation client** pour enrichir l’aide à la décision.

---

## Problématique métier

Dans une campagne bancaire, chaque appel a un coût.

L’enjeu est donc de transformer les données clients et l’historique de contact en un système d’aide à la décision capable de :

- repérer les profils les plus susceptibles de souscrire ;
- réduire les appels peu rentables ;
- améliorer le ROI des campagnes ;
- fournir des recommandations compréhensibles par des équipes marketing ou business.

---

## Dataset

| Caractéristique | Détail |
|---|---|
| Source | Bank Marketing Dataset |
| Volume | 45 211 observations |
| variable | 17 variables |
| Variable cible | `y` :binaire (souscription : yes / no) |
| Taux de souscription |**11,7 %** de réponses positives, soit un dataset fortement déséquilibré |

#### Variables exploitées

- **Profil client** : âge, métier, situation familiale, niveau d’éducation, balance, prêts
- **Contexte de contact** : canal, jour, mois
- **Historique marketing** : nombre de contacts, délai depuis le dernier contact, résultat des campagnes précédentes

---

## Démarche analytique : Pipeline

### 1. Analyse exploratoire

L’EDA a permis d’identifier plusieurs signaux utiles pour la décision :
- un fort **déséquilibre de classes** ;
- des variables très discriminantes comme `poutcome`, `contact`, `education`,`job` et `campaign`
- une variable `duration` très explicative, mais non exploitable dans un cadre **pré-appel**, car connue uniquement après le contact

### 2. Préparation des données

Les principales étapes de preprocessing ont été :
- consolidation des observations répétées ;
- nettoyage des doublons chronologiques ;
- conservation des modalités `unknown` comme information métier ;
- traitement spécifique de `pdays` ;
- encodage adapté selon la nature des variables ; `ordinal encoding` · `one-hot encoding` · `label encoding`
- standardisation des variables numériques ;
- séparation train/test stratifiée ;
- rééquilibrage des classes avec **SMOTE** sur l’échantillon d’entraînement.

### 3. Modélisation

Trois modèles supervisés ont été comparés :
| Modèle | Notes |
|---|---|
| Régression Logistique | modèle de base, simple et interprétable | 
| Random Forest | capable de capturer des relations non linéaires | 
| **XGBoost** | **modèle de boosting plus performant sur cette problématique** | 

Le projet intègre aussi une approche non supervisée :
| Modèle | Notes |
|---|---|
| **K-Means**  | segmenter les clients en groupes homogènes et rendre les résultats plus actionnables côté métier  | 

---

## Résultats clés

### Modèle retenu

**XGBoost** est le modèle le plus performant du projet, avec un **ROC-AUC de 0,76**. À seuil optimisé, il permet de mieux détecter les clients susceptibles de souscrire, tout en gardant une précision exploitable dans un contexte marketing.

### Lecture business

Le projet montre qu’en marketing, le meilleur modèle n’est pas uniquement celui qui maximise l’accuracy.

Le vrai sujet est le **choix du seuil de décision** :

- un seuil plus haut limite les appels inutiles ;
- un seuil plus bas augmente la détection des souscripteurs ;
- le bon arbitrage dépend du coût d’un appel et de la valeur d’une conversion.

### Segmentation client

La segmentation **K-Means** a permis d’identifier **3 profils clients**, dont un segment prioritaire avec un taux de conversion de **19 %**, soit près du double de la moyenne globale. Ce cluster se distingue notamment par un historique de contact plus riche, ce qui en fait une cible prioritaire pour les campagnes futures.

---

## Recommandations métier

À partir des résultats obtenus, plusieurs recommandations émergent :

- cibler en priorité les clients avec un **historique de campagne favorable** ;
- exploiter davantage le **canal de contact** et les variables de temporalité ;
- utiliser **XGBoost** comme base de scoring ;
- ajuster le **seuil de décision** selon la stratégie commerciale ;
- compléter le scoring individuel par une logique de **segmentation marketing**.

---

## Visuels clés du projet

### 1. Distribution de la cible
**Pourquoi ce visuel est important :** il montre immédiatement le déséquilibre de la variable cible et justifie le choix de métriques adaptées ainsi que l’usage de SMOTE.

![Distribution de la cible](./assets/target-distribution.png)

### 2. Matrice de corrélation des variables numériques
**Pourquoi ce visuel est important :** il synthétise les relations entre variables quantitatives et pose les bases de l’analyse exploratoire.

![Matrice de corrélation](./assets/correlation-heatmap.png)

### 3. Taux de conversion par variable métier forte
**Pourquoi ce visuel est important :** il met en évidence les segments les plus réceptifs et fait le lien direct entre analyse descriptive et ciblage marketing.

![Taux de conversion par segment](./assets/conversion-by-segment.png)

### 4. Courbe ROC du modèle XGBoost
**Pourquoi ce visuel est important :** il illustre la capacité du modèle retenu à discriminer les souscripteurs potentiels.

![Courbe ROC XGBoost](./assets/xgboost-roc-curve.png)

### 5. Comparaison des performances des modèles
**Pourquoi ce visuel est important :** il permet de justifier de manière synthétique le choix final du modèle.

![Comparaison des modèles](./assets/model-comparison.png)

### 6. Importance des variables XGBoost
**Pourquoi ce visuel est important :** il rend le modèle plus interprétable et met en avant les facteurs les plus actionnables pour les équipes métier.

![Importance des variables](./assets/feature-importance.png)

### 7. PCA et profil des clusters
**Pourquoi ce visuel est important :** il apporte une lecture complémentaire au scoring en montrant des segments clients distincts et exploitables.

![PCA et profils de clusters](./assets/kmeans-pca-clusters.png)

---

## Stack technique

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Scikit-learn**
- **XGBoost**
- **Imbalanced-learn**
- **Jupyter Notebook**

---

## Ce que ce projet démontre

Ce projet illustre ma capacité à :

- structurer un cas de **data science orienté décision** ;
- relier modélisation et **enjeux business** ;
- comparer plusieurs approches de classification ;
- interpréter les résultats avec une logique de **ROI marketing** ;
- produire une analyse exploitable à la fois pour des recruteurs **Data Scientist**, **Data Analyst** et **Business Analyst**.

---

## Structure du projet

```bash
.
├── campagne_marketing_bancaire.ipynb
├── README.md
└── img/
    ├── target-distribution.png
    ├── correlation-heatmap.png
    ├── conversion-by-segment.png
    ├── xgboost-roc-curve.png
    ├── model-comparison.png
    ├── feature-importance.png
    └── kmeans-pca-clusters.png
```

---

## Auteur

**Enzo Kouokam**  
Master Data Science & Business Intelligence — Epitech Toulouse

- [LinkedIn](https://www.linkedin.com/in/enzo-kamhoua/)
- [GitHub](https://github.com/kenzo-kouokam)
