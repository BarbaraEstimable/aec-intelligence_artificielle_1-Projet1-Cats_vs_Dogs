# Cats vs Dogs


## Tables des matières

- [Contexte](#-contexte)
- [Fonctionnalités](#-fonctionnalités)
- [Technologies utilisées](#-technologies-utilisées)
- [Installations](#-installations)
- [Le fonctionnement](#-Le-fonctionnement)



---
## Contexte

Ce projet entraîne un réseau de neurones convolutif (CNN) capable de distinguer des photos de **chats** et de **chiens**. À partir d'un notebook de départ atteignant environ **77 % de précision**, plusieurs configurations ont été testées pour améliorer le modèle, avec l'objectif de dépasser **85 %** sur le jeu de test.
 
**Résultat final : 94,22 % de précision sur le jeu de test.**



---
## Fonctionnalités

- **Chargement des images** depuis une archive zip, conversion en RGB, redimensionnement et étiquetage (0 = chat, 1 = chien).
- **Visualisation** d'un échantillon d'images pour valider le chargement.
- **Prétraitement** : normalisation des pixels entre 0 et 1.
- **Division des données** en jeux d'entraînement, de validation et de test.
- **Modèle CNN** construit avec Keras (couches Conv2D, MaxPool2D, Dropout et Dense).
- **Augmentation des données** (rotation, zoom, décalage, etc.) et callbacks d'entraînement.
- **Expériences comparatives** sur les hyperparamètres et l'architecture.
- **Graphiques d'analyse** : courbes de perte et de précision, matrice de confusion, distribution de confiance du modèle.
- **Sauvegarde** du modèle entraîné.


---
## Technologies utilisées

| Technologie | Utilisation |
|-------------|-------------|
| **Python 3** | Langage principal |
| **TensorFlow / Keras** | Construction, entraînement et évaluation du CNN |
| **NumPy** | Manipulation des images sous forme de tableaux |
| **scikit-learn** | Division des données et matrice de confusion |
| **Matplotlib** | Courbes d'entraînement et histogrammes |
| **Seaborn** | Matrice de confusion sous forme de heatmap |
| **Jupyter Notebook / Google Colab** | Exécution du notebook (GPU de Colab pour l'entraînement) |
| **PyCharm / GitHub Desktop** | Développement et versionnement |
| **Git / GitHub** | Suivi des expériences, un commit par modification |


---
## Installations

---
## Le fonctionnement

---
