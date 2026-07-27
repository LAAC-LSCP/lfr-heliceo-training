# Documentation ELSI — Interface de Support pour l'Héritage ExELang

Bienvenue dans la documentation d'ELSI (ExELang Legacy Support Interface). L'objectif de cette documentation est de présenter les fonctionnalités de l'outil et d'expliquer comment l'utiliser.

## Vue d'ensemble et objectifs

Les enregistrements de longue durée (Long-Form Recordings — LFR) d'enfants en contexte naturel constituent un type de données de recherche riche, mais complexe à exploiter. D'un corpus à l'autre, l'organisation, la documentation et le stockage varient considérablement, ce qui rend les analyses inter-corpus fastidieuses et sources d'erreurs. Les enregistrements bruts sont éthiquement sensibles, or la plupart des outils existants ne proposent aucun mécanisme intégré permettant de gérer des niveaux d'accès différenciés selon les protocoles de consentement et d'éthique. Enfin, l'extraction de métriques significatives — via des classificateurs de type de voix, de maturité vocale ou d'autres modèles d'apprentissage automatique — requiert une expertise technique que de nombreux chercheurs ne possèdent pas.

ELSI (ExELang Legacy Support Interface) est une plateforme logicielle permettant à tout utilisateur, quel que soit son niveau technique, de gérer des jeux de données standardisés, d'appliquer des modèles d'apprentissage automatique et d'extraire des métriques à partir d'enregistrements de longue durée centrés sur l'enfant. ELSI s'appuie sur le framework ChildProject et l'infrastructure DataLad, dont il hérite les pipelines de métadonnées standardisés et les capacités de versionnage.

Plus précisément, le package Python ChildProject pour la gestion des données LFR résout les différences de structure et d'organisation en imposant une structure de répertoires cohérente et un schéma de métadonnées commun à tous les corpus. Chaque corpus suit un schéma partagé avec des métadonnées à trois niveaux : enfant (ex. identifiant, date de naissance), enregistrement (ex. identifiant d'enregistrement, identifiant enfant, date) et annotation. Les métadonnées au niveau de l'annotation, générées automatiquement par ChildProject, associent chaque fichier d'annotation au segment audio correspondant — les annotations humaines des LFR ne couvrant généralement que des sections échantillonnées plutôt que l'enregistrement complet. DataLad ajoute un contrôle de version basé sur git pour les annotations, et git-annex pour la gestion des fichiers volumineux, permettant des structures de jeux de données imbriquées qui favorisent la reproductibilité.

![Figure 1 : L'écosystème ELSI](./img/ELSI_Doc.png)
<figure markdown>
  <figcaption>Figure 1 : L'écosystème ELSI</figcaption>
</figure>
