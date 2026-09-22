# Protocole de gestion des données de terrain — HéLiCÉO 💻

Anonymisation, organisation, transfert et dépôt des enregistrements audio et vidéo

---

## 1. Anonymisation et métadonnées

### 1.1 Attribution d'un ID anonymisé au participant

Avant toute collecte de données sur le terrain, chaque participant doit recevoir un identifiant anonymisé unique. Cette étape est un préalable indispensable à toute la suite du protocole : cet identifiant (noté **XXX** dans ce document, code d'anonymisation à définir par l'équipe) est utilisé dans tous les noms de dossiers et de fichiers présentés dans ce guide.

Un identifiant unique est attribué à chaque enfant participant, par exemple via un compteur séquentiel (001, 002, 003...). Cet identifiant remplace toute information directement identifiante (nom, prénom) dans l'ensemble des fichiers et dossiers du projet.

---

### 1.2 Fichier des enregistrements : `recordings.csv`

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

### 1.3 Fichier métadonnées : `children.csv`

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
### 2.1 Créer le dossier source

Sur votre ordinateur, créer un dossier dont le nom suit le format suivant (toujours tout en minuscule) :
 [code_lieu]_data_heliceo
> Ex. : `ilesds_data_heliceo` ou `marq_data_heliceo`

Ce dossier et son contenu seront copiés sur disque dur externe ou clé USB afin d'avoir un doublon.

---

### 2.2 Créer un dossier par participant

Dans le dossier source, créer un dossier par participant, au format :
 [code_lieu]_[XXX]_data_heliceo
 > Ex. : `ilesds_XXX_data_heliceo` (XXX = code d'anonymisation de l'enfant, à définir)

---

### 2.3 Créer les sous-dossiers vidéo et audio
Dans chaque dossier participant, créer deux sous-dossiers : `video` et `audio`.

ilesds_data_heliceo/ └── ilesds_XXX_data_heliceo/ 	├── video/ 	└── audio/

---

## 3. Transfert des données vers disques de stockage

### 3.1 Transfert depuis la GoPro

> **Rappel matériel :** la GoPro Hero permet un enregistrement continu d'environ 1h45, découpé automatiquement en chapitres de 8 min 41 s chacun, soit environ 13 fichiers `.mp4` par journée (12 chapitres complets + un dernier chapitre plus court). Les fichiers sont automatiquement nommés au format `GX[numéro de chapitre][numéro de vidéo]`, ex. `GX010058` (chapitre 1), `GX020058` (chapitre 2), etc. — tous les chapitres d'un même enregistrement partagent le même numéro de vidéo (`0058` dans cet exemple).

**Procédure :**

- À la fin de la journée d'enregistrement, transférer l'ensemble des fichiers de la GoPro dans le dossier video du participant : ilesds_XXX_data_heliceo/video/
- Vérifier que le dossier contient bien l'ensemble des chapitres attendus pour la journée (environ 13, à ajuster selon l'heure exacte de fin d'enregistrement).
- Copier la totalité des enregistrements dans le dossier video.
- Renommer uniquement le premier chapitre de la journée (celui avec le numéro de chapitre 01), au format : [code_lieu]_[XXX]_[date:AAMMJJ]_[heure:HMS]_video_01.mp4
- > Ex. : `ilesds_XXX_260916_143809_video_01`
- Ce premier fichier renommé sert de repère pour identifier l'origine de toute la série. Le renommage des fichiers restants (chapitres 02 à ~13) sera effectué en post-traitement (pas à la charge des stagiaires sur le terrain).
- Après transfert : **supprimez tous les enregistrements de l'appareil.**

---

### 3.2 Transfert depuis l'IzyRec

> **Rappel matériel :** l'IzyRec enregistre par blocs de 4h. À chaque bloc de 4h, l'appareil crée automatiquement un nouveau fichier.

**Procédure :**

1. Une fois tous les enregistrements de la journée terminés, connecter l'IzyRec à l'ordinateur.
2. Ouvrir le dossier créé par IzyRec, nommé d'après la date d'enregistrement du jour. Il contient un fichier `.wav` par bloc de 4h enregistré.
3. Copier chaque fichier `.wav` dans le dossier `audio` du participant : `ilesds_XXX_data_heliceo/audio/`
4. Renommer chaque fichier selon le format : [code_lieu][XXX][AAMMJJ]_[HMS]audio[transfert]


> Ex. : `ilesds_XXX_260915_101350_audio_01.wav` (premier bloc de 4h de la journée), `ilesds_XXX_260915_141350_audio_02.wav` (deuxième bloc), etc.

5. Le numéro de transfert correspond à l'ordre de transfert des fichiers de la journée (1er fichier de 4h, 2ᵉ fichier de 4h, etc.). Respectez le nombre de zéros avant le chiffre du transfert (principe du zero-padding, expliqué ci-dessous).
6. **Différence avec la vidéo à noter :** contrairement à la GoPro (un seul enregistrement continu par jour, renommage du 1er chapitre seulement, le reste en post-traitement), ici chaque fichier audio est renommé directement sur le terrain (max 6 fichiers/jour, donc gérable manuellement).
7. Après transfert : **supprimez tous les enregistrements de l'appareil.**

> 💡 **Astuce :** le nom généré automatiquement par IzyRec contient un timestamp Unix (epoch). En le copiant sur [epochconverter.com](https://epochconverter.com), vous obtenez la date et l'heure exactes de l'enregistrement — utile pour vérifier la date/session avant de renommer.

---

### 3.3 Bon à savoir : pourquoi des zéros devant le chiffre ? (zero padding)

Toujours utiliser le même nombre de chiffres pour numéroter une série de fichiers, en ajoutant des zéros devant les petits numéros.

| Sans zero padding | Avec zero padding |
|-------------------|-------------------|
| 1, 10, 11, 2, 3... → l'ordinateur classe mal (le 10 se retrouve avant le 2) | 01, 02, 03... 10, 11 → l'ordre est correct |

> **Règle :** le nombre de chiffres dépend du nombre max de fichiers possible (99 fichiers → 2 chiffres, 9999 → 4 chiffres).

---

> ⚠️ **Règles d'or**
>
> - Toujours nommer vos fichiers **au moment du transfert** vers votre disque, ne jamais le reporter à plus tard.
> - Toujours **dire à haute voix l'heure de début** à chaque enregistrement audio et vidéo.

---

## 4. Dépôt des données

### 4.1 Serveur : LAAC Uploader

Outil simple d'utilisation — chaque personne dispose d'un identifiant et d'un mot de passe.

---

*Document élaboré par l'équipe ExELang & HéLiCéO — LSCP, École Normale Supérieure*

 





