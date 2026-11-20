# Programming in data science project

> *Description courte du projet à venir...*

---

## Installation & Configuration (Setup)

Ce projet utilise **[uv](https://docs.astral.sh/uv/)** pour la gestion rapide des environnements virtuels et des dépendances. Toutefois, des instructions alternatives avec `pip` et `conda` sont également fournies ci-dessous.

### 1. Cloner le dépôt

```bash
git clone https://github.com/votre-utilisateur/nom-du-projet.git
cd nom-du-projet
```

---

### 2. Configurer l'environnement et installer les dépendances

#### Option A : Avec `uv` (Recommandé)

1. **Installer `uv`** (si ce n'est pas déjà fait) :
   * **macOS / Linux :**
     ```bash
     curl -LsSf https://astral.sh/uv/install.sh | sh
     ```
   * **Windows (PowerShell) :**
     ```powershell
     powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
     ```

2. **Synchroniser l'environnement et installer les dépendances :**
   ```bash
   uv sync
   ```
   *(Cela créera automatiquement un dossier `.venv` et installera les packages définis dans `pyproject.toml` / `uv.lock`).*

3. **Commandes utiles avec `uv` :**
   * **Ajouter un nouveau package :** `uv add <nom-du-package>`
   * **Exécuter un script dans l'environnement :** `uv run python main.py`
   * **Activer l'environnement manuellement :** `source .venv/bin/activate` (Linux/macOS) ou `.venv\Scripts\activate` (Windows).

---

#### Option B : Équivalent avec `pip` (Standard Python)

1. **Créer et activer l'environnement virtuel :**
   ```bash
   python -m venv .venv
   # Sur Linux / macOS :
   source .venv/bin/activate
   # Sur Windows :
   .venv\Scripts\activate
   ```

2. **Installer les dépendances :**
   ```bash
   pip install .
   ```

3. **Ajouter un package :**
   ```bash
   pip install <nom-du-package>
   ```

---

#### Option C : Équivalent avec `conda`

1. **Créer et activer l'environnement :**
   ```bash
   conda create -n mon-env python=3.11
   conda activate mon-env
   ```

2. **Installer les dépendances :**
   ```bash
   pip install -r requirements.txt
   # Ou via pyproject.toml :
   pip install .
   ```

3. **Ajouter un package :**
   ```bash
   conda install <nom-du-package>
   # Ou via pip à l'intérieur de l'environnement conda :
   pip install <nom-du-package>
   ```

---

### 3. Configuration des données (`data/`)

Le dossier `data/` est présent à la racine du projet, mais il est **volontairement vide** (les fichiers de données étant trop volumineux pour etre Git).

Pour faire fonctionner le projet :
1. Téléchargez les fichiers de données nécessaires depuis votre source.
2. Placez-les directement dans le dossier `data/` à la racine :

```text
nom-du-projet/
├── data/               <-- Placez vos fichiers ici
│   ├── fichier1.csv
│   └── fichier2.parquet
├── src/                <-- Code ici
├── pyproject.toml
└── README.md
```