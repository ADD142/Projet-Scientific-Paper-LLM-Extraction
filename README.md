# Extraction automatique de données OPV via LLM

Pipeline Python d'extraction automatique de données structurées depuis des articles scientifiques PDF sur les cellules solaires organiques (OPV), en utilisant l'API Gemini (Google).

---

## Problème résolu

Les données de performance des cellules solaires OPV sont enfouies dans des PDF scientifiques non structurés.  
Les extraire manuellement est long, fastidieux et source d'erreurs.

Ce projet automatise entièrement ce processus : **PDF → JSON structuré → Excel exploitable**.

---

## Comment ça fonctionne

```
1. PDF scientifique
      
2. Upload vers Gemini API
      
3. Prompt engineering (one-shot, normalisation, séparation des configurations)
      
4. JSON structuré par dispositif
      
5. Aplatissement et export Excel
```

Pour chaque article, le pipeline :
1. Uploade le PDF directement vers Gemini
2. Envoie un prompt expert pour identifier chaque configuration de dispositif
3. Normalise automatiquement les solvants, unités et structures
4. Exporte toutes les données dans un fichier Excel exploitable

---

## Données extraites par dispositif

| Champ | Description |
|---|---|
| `donor` / `acceptor` | Matériaux actifs (ex: PM6, Y6) |
| `ratio_weight` | Ratio donneur:accepteur |
| `solvent` | Solvant normalisé (ex: CB → Chlorobenzene) |
| `annealing_temperature_celsius` | Température de recuit |
| `pce_percent` | Efficacité de conversion (valeur champion) |
| `voc_volts` | Tension en circuit ouvert |
| `jsc_ma_cm2` | Densité de courant de court-circuit |
| `ff_percent` | Facteur de forme |

---

## Technologies utilisées

- **Python 3.13** — langage principal
- **Google Gemini API** (`gemini-1.5-flash`) — modèle LLM multimodal
- **Pandas** — nettoyage et transformation des données
- **Prompt Engineering** — one-shot, normalisation, séparation des configurations expérimentales

---

## 🚀 Installation et utilisation

### 1. Cloner le repo
```bash
git clone https://github.com/ton-username/Projet-Scientific-Paper-LLM-Extraction.git
cd Projet-Scientific-Paper-LLM-Extraction
```

### 2. Installer les dépendances
```bash
pip install -r requirements.txt
```

### 3. Configurer la clé API
Crée un fichier `.env` à la racine :
```
GOOGLE_API_KEY=ta_cle_api_ici
```

### 4. Ajouter tes PDFs
Place tes articles scientifiques dans le dossier `test/`

### 5. Lancer le notebook
```bash
jupyter notebook demoOPV.ipynb
```

---

## 📁 Structure du projet

```
extraction-llm-scientifique/
│
├── demoOPV.ipynb          # Notebook principal
├── requirements.txt       # Dépendances Python
├── README.md              # Ce fichier
├── .gitignore             # Fichiers exclus de Git
│
├── test/                # PDFs scientifiques
│   └── exemple.pdf
│
└── output/                # Fichiers Excel générés
    └── scanned_pdf_extraction.xlsx
```

---

## 💡 Points clés du prompt engineering

- **Séparation des configurations** : chaque variation (ratio D:A, température, solvant) génère un objet JSON séparé
- **Normalisation automatique** : `CB → Chlorobenzene`, `DIO → 1,8-Diiodooctane`, etc.
- **Inférence de structure** : `ITO/PEDOT:PSS/...` → `Conventional`, `ITO/ZnO/...` → `Inverted`
- **Gestion des valeurs manquantes** : `"Not reported"` systématiquement au lieu de champs vides

---

## Auteure

**Aida Diop** — Étudiante ingénieure Big Data, JUNIA ISEN Lille  
📧 aidadiop1014@gmail.com

---

*Projet réalisé dans le cadre du Master 1 Big Data — JUNIA ISEN (Nov 2025 – Avr 2026)*
