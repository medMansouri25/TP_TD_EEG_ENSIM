# Analyse et Exploitation des Signaux EEG

Projet de Travaux Pratiques et Travaux Dirigés sur l'analyse des signaux EEG pour l'estimation de la charge cognitive du conducteur.

## Objectif

Construire une **chaîne complète d'analyse de signaux EEG** :
- Compréhension et visualisation des données
- Prétraitement et filtrage
- Extraction de features
- Classification et analyse

## Structure du projet

```
TP_TD_EEG_ENSIM/
├── TD1+2.ipynb                  ← Compréhension et visualisation
├── TD3.ipynb                    ← Prétraitement EEG
├── TD4.ipynb                    ← Feature engineering
├── TP_complet.ipynb             ← Travail pratique complet
├── Data/
│   ├── EEG/                     ← Signaux EEG bruts (21 participants)
│   ├── EEG_Features_10s/        ← Features extraites (10s)
│   ├── Labels/                  ← Étiquettes de charge cognitive
│   ├── Normalized_Features_10s/
│   └── Normalized_Features_10s_With_Label/
└── README.md
```

## Contenu des Travaux Dirigés

### TD1+2 — Compréhension et Visualisation
- Contexte et problématique de la charge cognitive
- Structure du dataset CL-Drive
- Visualisation des signaux EEG bruts
- Pipeline d'analyse

### TD3 — Prétraitement EEG
- Filtrage passe-bande Butterworth (0.4 – 75 Hz)
- Filtre notch (60 Hz)
- Inspection et validation des signaux prétraités
- Traitement par lot du dataset complet

### TD4 — Feature Engineering
- Extraction de features fréquentielles (delta, theta, alpha, beta, gamma)
- Puissance spectrale via Welch
- Entropie spectrale
- Préparation pour classification

### TP_complet — Travail Pratique Intégré
- Intégration complète de la chaîne d'analyse
- Application sur l'ensemble du dataset

## Dataset

- **Participants** : 21 sujets
- **Niveaux de difficulté** : 9 niveaux
- **Canaux EEG** : AF7, AF8, TP9, TP10
- **Fréquence d'échantillonnage** : 256 Hz
- **Fichiers par participant** : Signaux EEG + baseline

## Installation

```bash
# Créer et activer un environnement virtuel
python -m venv .venv
source .venv/bin/activate  # Linux/macOS
# ou
.venv\Scripts\activate  # Windows

# Installer les dépendances
pip install numpy pandas scipy matplotlib scikit-learn tqdm jupyter
```

## Utilisation

```bash
# Lancer Jupyter
jupyter lab
```

Puis ouvrir les notebooks dans l'ordre :
1. `TD1+2.ipynb` — Compréhension et visualisation
2. `TD3.ipynb` — Prétraitement
3. `TD4.ipynb` — Feature extraction
4. `TP_complet.ipynb` — Application intégrée

## Auteurs

- Mohammed Mansouri — `Mohammed.Mansouri.Etu@univ-lemans.fr`
- Thomas Hyaumet — `Thomas.Hyaumet.Etu@univ-lemans.fr`
- Jade — `Jade.Barbier.Etu@univ-lemans.fr`

ENSIM — 4A INFO ALT— 2025/2026
