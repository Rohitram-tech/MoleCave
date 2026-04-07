# 🧪 The MoleCave — Intelligent Chemical Data Management System

> A modern, open-source web application for storing, searching, and analyzing chemical compound data — built with Python, Flask, and RDKit.

---

## 🌟 Features

- 🔍 **Smart Compound Search** — Search by name, SMILES string, molecular formula, or InChIKey
- 📥 **Automatic Data Fetching** — Enter any drug name and the system fetches all data automatically from PubChem and ChEMBL
- 🧬 **2D Structure Visualization** — Renders molecular structures using RDKit
- 🔗 **Multi-Database Integration** — Links to PubChem, ChEMBL, and DrugBank for every compound
- 🛡️ **Intelligent Deduplication** — Uses InChIKey-based matching to prevent duplicate entries
- ⚗️ **Molecular Property Calculation** — Automatically calculates molecular formula, weight, and Morgan fingerprints
- 🗄️ **Pre-loaded Database** — Comes seeded with 91 antibiotic and pharmaceutical compounds

---

## 🖥️ Screenshots

### Dashboard
![Dashboard](screenshots/Dashboard.png)
*Home page showing total compounds stored in the database*

### Search
![Search](screenshots/search.png)
*Real-time compound search by name, SMILES, or formula*

### Compound Details
![Compound Details](screenshots/compound_detail.png)
*Detailed view showing 2D structure, molecular properties, and external database links*

### Upload New Compound
![Upload](screenshots/upload.png)
*Upload any compound by name, SMILES string, or InChIKey — data is fetched automatically*

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, Flask |
| Cheminformatics | RDKit, MolVS |
| Database | SQLite |
| APIs | PubChem REST API, ChEMBL API, UniChem API |
| Frontend | HTML, CSS, Jinja2 Templates |
| Environment | Conda |

---

## ⚙️ How It Works

```
User inputs drug name / SMILES / InChIKey
        ↓
System detects input type automatically
        ↓
Fetches data from PubChem API → gets SMILES, names, CID
Fetches data from ChEMBL API → gets additional drug data
        ↓
RDKit processes the SMILES:
  → Normalizes SMILES (MolVS)
  → Generates 2D structure image (SVG)
  → Calculates molecular formula and weight
  → Computes Morgan fingerprint (ECFP4, 2048 bits)
  → Derives InChI and InChIKey
        ↓
Checks database for duplicates using InChIKey
  → Exists? Redirect to existing compound page
  → New? Save to SQLite database
        ↓
Displays compound page with full details and external links
```

---

## 🚀 Setup & Installation

### Prerequisites
- [Anaconda](https://www.anaconda.com/download) or Miniconda must be installed

### Step 1 — Clone the Repository
```bash
git clone https://github.com/yourusername/MoleCave.git
cd MoleCave
```

### Step 2 — Create Conda Environment
```bash
conda env create -f environment.yml
```

### Step 3 — Activate Environment
```bash
conda activate chemical-repo
```

### Step 4 — Initialize and Seed Database
```bash
python seed.py
```
This creates the SQLite database and pre-loads it with 91 pharmaceutical compounds.

### Step 5 — Run the Application
```bash
python -m gui_app.app
```

### Step 6 — Open in Browser
```
http://127.0.0.1:5000
```

---

## 📁 Project Structure

```
The-MoleCave/
│
├── gui_app/
│   ├── app.py                  # Flask routes and application logic
│   ├── normalize_compound.py   # Core cheminformatics engine (API calls + RDKit)
│   ├── templates/              # HTML pages
│   │   ├── index.html          # Dashboard
│   │   ├── search.html         # Search page
│   │   ├── compound.html       # Compound detail page
│   │   └── upload.html         # Upload page
│   └── static/
│       └── style.css           # Styling
│
├── schema.sql                  # Database schema
├── seed.py                     # Database initialization and seeding script
├── remove_duplicates.py        # Database cleanup utility
├── environment.yml             # Conda environment file
└── database.db                 # SQLite database (auto-generated)
```

---

## 🧠 Key Technical Concepts

### InChIKey-Based Deduplication
Every compound has a unique 27-character InChIKey hash. Before saving, the system checks if the InChIKey already exists in the database — preventing duplicate entries regardless of how the compound was inputted.

### Morgan Fingerprints
Each compound's Morgan fingerprint (ECFP4, 2048 bits) is stored as a binary string. This enables future ML-based drug similarity searches and activity prediction.

### Multi-source API Pipeline
The system queries PubChem first, then ChEMBL, then resolves DrugBank links via UniChem — building a comprehensive data record from multiple trusted scientific databases.

---

## 🔮 Future Improvements

- [ ] ML-based drug activity prediction using stored Morgan fingerprints
- [ ] ADMET property prediction integration (SwissADME)
- [ ] Molecular similarity search using fingerprint comparison
- [ ] Bulk CSV upload support
- [ ] REST API endpoints for programmatic access
- [ ] Docker containerization

---

## 📚 Databases Used

| Database | Purpose |
|---|---|
| [PubChem](https://pubchem.ncbi.nlm.nih.gov/) | SMILES, names, molecular properties |
| [ChEMBL](https://www.ebi.ac.uk/chembl/) | Drug activity and bioassay data |
| [DrugBank](https://go.drugbank.com/) | Approved drug information |
| [UniChem](https://www.ebi.ac.uk/unichem/) | Cross-database compound mapping |

---

## 👨‍💻 Author

**Rohit Ram**
M.Sc. Bioinformatics | Mumbai, India
[LinkedIn](https://linkedin.com/in/rohitram) • [GitHub](https://github.com/rohitram)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
