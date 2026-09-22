# Protocole de gestion des données de terrain — HéLiCÉO 💻

Anonymisation, organisation, transfert et dépôt des enregistrements audio et vidéo

---

## 1. Anonymisation et métadonnées

### 1.2 Attribution d'un ID anonymisé au participant

Avant toute collecte de données sur le terrain, chaque participant doit recevoir un identifiant anonymisé unique. Cette étape est un préalable indispensable à toute la suite du protocole : cet identifiant (noté **XXX** dans ce document, code d'anonymisation à définir par l'équipe) est utilisé dans tous les noms de dossiers et de fichiers présentés dans ce guide.

Un identifiant unique est attribué à chaque enfant participant, par exemple via un compteur séquentiel (001, 002, 003...). Cet identifiant remplace toute information directement identifiante (nom, prénom) dans l'ensemble des fichiers et dossiers du projet.

---

### 2.1 Fichier des enregistrements : `recordings.csv`

Ce fichier constitue le registre de tous les enregistrements du dataset, selon le standard ChildProject utilisé par le laboratoire. Il est indispensable au bon fonctionnement du pipeline de traitement : sans lui, les enregistrements ne peuvent pas être validés ni exploités par les outils d'analyse. Le but est de faire correspondre l'anonymisation avec l'enregistrement.

Le jeune chercheur renseigne une ligne par fichier transféré (voir partie 3), dans le tableau qui lui est fourni, avec les champs suivants :

| Champ | Description |
|-------|-------------|
| `recording_filename` | Nom du fichier renommé, y compris l'extension. Si une organisation en sous-dossiers est utilisée, rajouter les sous-dossiers séparés par `/` (ex. `ilesds_XXX_260915_141350_video_01.mp4` ; `XXX/ilesds_XXX_260915_141350_video_01.mp4` si à l'intérieur d'un sous-dossier XXX) |
| `original_filename` | Nom d'origine donné par l'appareil (ex. `GX010058` pour la GoPro, ou nom IzyRec) |
| `child_id` | ID anonymisé du participant (XXX) |
| `date_iso` | Date de l'enregistrement format AAAA-MM-JJ (ex. `2022-05-27`) |
| `start_time` | Heure de début format 24h HH:SS (ex. `17:34`) |
| `duration` | Durée du fichier |
| `recording_device` | `bodycam` ou `izyrec` — termes génériques désignant respectivement l'appareil vidéo et l'appareil audio, indépendamment du modèle exact utilisé |
| `format` | `mp4` ou `wav` |
| `experiment` | Hélicéo-Projet X (ex. `Hélicéo-Projet IlesdS`) |
| `discard` | 0/1 — permet de déterminer si un enregistrement doit être utilisé par ChildProject. `0` signale un enregistrement utilisé, `1` un enregistrement ignoré (ex. enregistrement de test, fichier corrompu, mauvaises conditions d'enregistrement, etc.) |

---

### 2.1 Fichier métadonnées : `children.csv`

Ce fichier constitue le registre des métadonnées démographiques et contextuelles par participant, également selon le standard ChildProject. **Une seule ligne par enfant** (et non par enregistrement), à la différence de `recordings.csv`.

Champs proposés, basés sur le standard ChildProject (seuls `experiment`, `child_id` et `child_dob` sont strictement obligatoires ; les autres s'ajoutent selon les besoins du protocole HéLiCÉO) :

| Champ | Description |
|-------|-------------|
| `experiment` | Hélicéo-Projet X (ex. `Hélicéo-Projet IlesdS`) |
| `child_id` | ID anonymisé du participant XXX (obligatoire) |
| `child_dob` | Date de naissance de l'enfant (obligatoire) format AAAA-MM-JJ (ex. `2017-12-31`) |
| `dob_criterion` | Méthode d'obtention de la date de naissance (ex. déclarée par le participant, extrapolée de son âge reporté) |
| `dob_accuracy` | Précision de la date de naissance (ex. jour, mois) |
| `location_id` | Code du lieu / terrain |
| `child_sex` | Sexe de l'enfant (F/M) |
| `language` | Langue principale de l'environnement (si une seule langue présente) |
| `languages` | Ensemble des langues présentes dans l'environnement, séparées par `;`. Si le pourcentage est connu, l'indiquer avec la langue (ex. `french 35%;english 65%`) |
| `normative` | Développement normatif déclaré (Y/N respectivement oui ou non) |
| `normative_criterion` | Méthode d'évaluation du développement normatif |
| `order_of_birth` | Rang de naissance de l'enfant dans la fratrie (ex. `1` pour aîné) |
| `n_of_siblings` | Nombre de frères et sœurs |
| `siblings_dob_sex` | Date de naissance et sexe de chaque frère/sœur, au format `JJ/MM/AAAA/sexe`, séparés par `;` (ex. `12/03/2020/M;05/07/2022/F`) |
| `household_size` | Taille du foyer en nombre de personnes |
| `discard` | 0/1 — les lignes marquées d'un `1` sont ignorées |

---

## 2. Organiser ses données
### Étape 1 : Création du dossier source et ses sous-dossiers par participant
####1.Créer le dossier source

Sur votre ordinateur, créer un dossier dont le nom suit le format suivant (toujours tout en minuscule) :
 [code_lieu]_data_heliceo
> Ex. : `ilesds_data_heliceo` ou `marq_data_heliceo`

Ce dossier et son contenu seront copiés sur disque dur externe ou clé USB afin d'avoir un doublon.

---

#### 2.Créer un dossier par participant

Dans le dossier source, créer un dossier par participant, au format :
 [code_lieu]_[XXX]_data_heliceo
 > Ex. : `ilesds_XXX_data_heliceo` (XXX = code d'anonymisation de l'enfant, à définir)

---

### 2.3 Créer les sous-dossiers vidéo et audio
Dans chaque dossier participant, créer deux sous-dossiers : `video` et `audio`.

ilesds_data_heliceo/
└── ilesds_XXX_data_heliceo/
    ├── video/
    └── audio/

---

## 3. Transfert des données vers disques de stockage

### 3.1 Transfert depuis la GoPro

> **Rappel matériel :** la GoPro Hero permet un enregistrement continu d'environ 1h45, découpé automatiquement en chapitres de 8 min 41 s chacun, soit environ 13 fichiers `.mp4` par journée (12 chapitres complets + un dernier chapitre plus court). Les fichiers sont automatiquement nommés au format `GX[numéro de chapitre][numéro de vidéo]`, ex. `GX010058` (chapitre 1), `GX020058` (chapitre 2), etc. — tous les chapitres d'un même enregistrement partagent le même numéro de vidéo (`0058` dans cet exemple).

**Procédure :**

1. À la fin de la journée d'enregistrement, transférer l'ensemble des fichiers de la GoPro dans le dossier `video` du participant : `ilesds_XXX_data_heliceo/video/`
2. Vérifier que le dossier contient bien l'ensemble des chapitres attendus pour la journée (environ 13, à ajuster selon l'heure exacte de fin d'enregistrement).
3. Copier la totalité des enregistrements dans le dossier `video`.
4. Renommer **uniquement le premier fichier** de la série, au format :
 





