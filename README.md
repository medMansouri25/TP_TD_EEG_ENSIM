# TP / TD — Analyse et exploitation des signaux EEG

Travaux pratiques et dirigés de 4ᵉ année à l'**ENSIM** (École Nationale Supérieure d'Ingénieurs du Mans, Université du Mans). Cours **Analyse et exploitation des signaux EEG**.

L'objectif transversal est de construire, étape par étape, une **chaîne complète d'estimation de la charge cognitive du conducteur à partir de signaux EEG** : compréhension du problème → visualisation → prétraitement → extraction de features → classification, en se basant sur le dataset public **CL-Drive**.

## Référence

Angkan, P., Behinaein, B., Mahmud, Z., Bhatti, A., Rodenburg, D., Hungler, P., & Etemad, A. (2023).
**CL-Drive: A Continuously Labeled Multimodal Dataset of Cognitive Load During Driving**.
[arXiv:2304.04273](https://arxiv.org/abs/2304.04273) *(PDF inclus : [`2304.04273v2.pdf`](2304.04273v2.pdf))*.

Le dataset est hébergé sur Borealis : [doi:10.5683/SP3/JJ2YZZ](https://doi.org/10.5683/SP3/JJ2YZZ).

## Structure du dépôt

```
TP_TD_EEG_ENSIM/
├── 2304.04273v2.pdf           ← papier de référence CL-Drive
├── CL-Drive_EEG_part1.zip     ← partie 1 du dataset EEG (~73 MB)
├── CL-Drive_EEG_part2.zip     ← partie 2 du dataset EEG (~76 MB)
├── TD1+2.ipynb                ← compréhension du papier + visualisation EEG
├── TD3.ipynb                  ← prétraitement EEG (filtrage + batch)
├── TD4.ipynb                  ← feature engineering EEG
└── README.md
```

Après extraction des deux ZIP, le dossier `doi-10.5683-sp3-jj2yzz/EEG/` est créé avec **21 participants × 18 fichiers** CSV (`eeg_data_level_{1..9}` + `eeg_baseline_level_{1..9}`).

## Contenu des TD

### TD1+2 — Compréhension du papier et visualisation
- Contexte du dataset CL-Drive, définition de la charge cognitive, échelle PAAS
- Modalités mesurées, protocole expérimental, scénarios de conduite
- Échantillonnage / segmentation temporelle
- Formulation du problème d'apprentissage automatique
- Visualisation des signaux EEG bruts
- Pipeline général du projet

### TD3 — Prétraitement EEG
- Filtre passe-bande Butterworth (ordre 2, 0.4 – 75 Hz, zero-phase)
- Filtre notch IIR à 60 Hz (Q = 30) pour éliminer la raie secteur (CL-Drive a été enregistré au Canada)
- Inspection PSD avant/après pour valider la chaîne
- Application aux 4 canaux du casque Muse S : **AF7, AF8, TP9, TP10**
- Rapport qualité par canal après prétraitement
- **Prétraitement par lot** sur les 378 CSV du dataset avec `tqdm`, idempotence (`skip_existing`) et diagnostic par fichier

### TD4 — Feature engineering
- Bandes fréquentielles EEG (delta, theta, alpha, beta, gamma)
- PSD via Welch et features de puissance par bande
- Entropie spectrale
- Préparation des features pour la classification

## Prérequis

```bash
pip install numpy pandas scipy matplotlib tqdm jupyter
```

Versions testées : Python 3.12, scipy ≥ 1.10.

## Mise en place du dataset

```powershell
# Depuis la racine du dépôt
Expand-Archive -Path CL-Drive_EEG_part1.zip -DestinationPath . -Force
Expand-Archive -Path CL-Drive_EEG_part2.zip -DestinationPath . -Force
```

```bash
# Sous bash / Linux / macOS
unzip CL-Drive_EEG_part1.zip
unzip CL-Drive_EEG_part2.zip
```

Vérification :
```text
doi-10.5683-sp3-jj2yzz/EEG/  → 21 sous-dossiers (1030, 1434, …)
```

## Lancer les notebooks

```bash
jupyter lab
```

Puis ouvrir successivement `TD1+2.ipynb`, `TD3.ipynb`, `TD4.ipynb`. Les notebooks sont indépendants mais leur logique se chaîne : sortir TD3 produit le dossier `doi-10.5683-sp3-jj2yzz/filtered_EEG/` consommé par TD4.

## Conventions du dataset CL-Drive

| Paramètre | Valeur |
|---|---|
| Casque | Muse S (4 électrodes) |
| Canaux EEG | AF7, AF8, TP9, TP10 |
| Fréquence d'échantillonnage | 256 Hz |
| Filtre passe-bande | Butterworth ordre 2, 0.4 – 75 Hz |
| Filtre notch | 60 Hz, Q = 30 |
| Participants | 21 (IDs : 1030, 1434, …) |
| Niveaux de difficulté | 9 (level_1 à level_9) |
| Fichiers par participant | 18 (`eeg_data_*` + `eeg_baseline_*`) |

## Auteurs

- Mohammed Mansouri — `Mohammed.Mansouri.Etu@univ-lemans.fr`
- Thomas Hyaumet — `Thomas.Hyaumet.Etu@univ-lemans.fr`
- Jade ([@MoggleJ](https://github.com/MoggleJ))

ENSIM — 4ᵉ année — 2025/2026
