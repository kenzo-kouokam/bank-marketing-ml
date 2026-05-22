# Dataset

Ce projet utilise un jeu de données public sur les campagnes marketing d'une banque portugaise.

## Source

- Dataset : [UCI Bank Marketing Dataset — Kaggle](https://www.kaggle.com/datasets/adityamhaske/bank-marketing-dataset)
- Source originale : [UCI Machine Learning Repository — Bank Marketing](https://archive.ics.uci.edu/dataset/222/bank+marketing)

## Description

Les données décrivent des **campagnes de marketing direct** (appels téléphoniques) d'une institution bancaire portugaise.  
Chaque ligne représente un contact client, avec des informations :

- caractéristiques socio‑démographiques (âge, profession, situation familiale, éducation, etc.)  
- situation financière (crédit immobilier, prêt personnel, solde du compte)  
- historique de contact (nombre de contacts, campagne précédente, délai depuis le dernier contact)  
- contexte de la campagne (mois, jour de la semaine, type de contact)  
- **variable cible `y`** : le client a‑t‑il souscrit un dépôt à terme ? (`yes` / `no`)

Le dataset est **déséquilibré** : la majorité des clients ne souscrivent pas au produit proposé.

## Remarque

Le dataset n'est pas stocké dans ce dépôt GitHub afin de garder le repository léger et d'éviter les problèmes de versionning sur de gros fichiers.  
Pour reproduire l'analyse :

1. Télécharger les données depuis Kaggle ou l'UCI :
   - Kaggle : `bank-marketing-dataset`
   - ou la version UCI d'origine.  
2. Placer le fichier (par exemple `bank.csv` ou `bank-full.csv`) dans un dossier local `data/`.  
3. Adapter le chemin d'accès au fichier dans le notebook si nécessaire.
