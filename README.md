# 🔄 ETL Talend – Fusion, enrichissement et contrôle qualité multi-sources

![Talend](https://img.shields.io/badge/Talend-Open%20Studio-FF6D70)
![Power BI](https://img.shields.io/badge/Power%20BI-rapports-F2C811?logo=powerbi&logoColor=black)

Projet d'**analyse de données** (Bachelor 3, Ynov Campus) : un job **Talend** qui fusionne plusieurs fichiers CSV
de transactions hétérogènes, les enrichit avec des référentiels, détecte les anomalies et produit un
**rapport de qualité**, ensuite visualisé dans Power BI.

## 🧱 Le job `Job_Enrichissement_Qualite`

```
 tFileList ─► tFileInputDelimited (5 fichiers de transactions)
                     │
                     ▼
     tMap (fusion + normalisation) ◄── taux de change · catégories · liste noire · transactions spéciales
                     │
          ┌──────────┼───────────────┐
          ▼          ▼               ▼
     tUniqRow    tFilterRow     tAggregateRow
   (doublons)   (anomalies)    (rapport qualité)
          │          │               │
          ▼          ▼               ▼
   CSV_final_   CSV_anomalies   rapport_qualite ──► tSendMail (alerte)
    enrichie
```

| Composant | Rôle |
|---|---|
| `tFileList` + `tFileInputDelimited` | Lecture de tous les fichiers du dossier `Input/main` |
| `tMap` (x3) | Fusion, conversion de devises, catégorisation par montant, jointures référentielles |
| `tUniqRow` / `tSortRow` | Suppression des doublons et tri |
| `tFilterRow` | Isolement des transactions suspectes (liste noire, montants incohérents) |
| `tAggregateRow` | Indicateurs de qualité |
| `tSendMail` | Envoi automatique du rapport de qualité |

## 📂 Données

| Fichier | Contenu |
|---|---|
| `Input/main/input_file_*.csv` | Transactions (ID, nom, prénom, montant, date) |
| `Input/tauxchange.csv` | Taux de conversion vers l'euro |
| `Input/categories.csv` | Tranches de montant → catégorie |
| `Input/blacklist.csv` | Clients sur liste noire et motif |
| `Input/transaction_speciales.csv` | Transactions à vérifier manuellement |
| `output/` | Résultats : données finales enrichies, anomalies, rapport qualité |
| `powerbi/` | Rapports Power BI construits sur les sorties |

## ▶️ Ouvrir le projet

1. Installer Talend Open Studio for Data Integration.
2. **Importer un projet existant** → sélectionner le dossier `LOCAL_PROJECT`.
3. Ouvrir `Job_Enrichissement_Qualite`, adapter les chemins des fichiers d'entrée et de sortie.
4. Pour l'envoi d'e-mail, renseigner vos propres paramètres SMTP dans `tSendMail` (ils ont été retirés de ce dépôt).

## 🛠️ Compétences

`ETL` · `Talend` · `qualité des données` · `enrichissement` · `jointures référentielles` · `Power BI`

---
Khadija Ibisk – Bachelor Dev IA & Data Engineering, Ynov Campus
