# Cats vs Dogs


## Tables des matières

- [Contexte](#-contexte)
- [Fonctionnalités](#-fonctionnalités)
- [Technologies utilisées](#-technologies-utilisées)
- [Installations](#-installations)
- [Le fonctionnement](#-Le-fonctionnement)
- [Modification](#modification)
- [Résultats](#résultats)



---
## Contexte

Ce projet entraîne un réseau de neurones convolutif (CNN) capable de distinguer des photos de **chats** et de **chiens**. À partir d'un notebook de départ atteignant environ **77 % de précision**, plusieurs configurations ont été testées pour améliorer le modèle, avec l'objectif de dépasser **85 %** sur le jeu de test.
 
**Résultat final : 94,22 % de précision sur le jeu de test.**



---
## Fonctionnalités

- **Chargement des images** depuis une archive zip stockée sur Google Drive, conversion en RGB, redimensionnement à 160 × 160 et étiquetage (0 = chat, 1 = chien).
- **Visualisation** de 10 images (5 chats, 5 chiens) pour valider le chargement.
- **Prétraitement** : normalisation des pixels entre 0 et 1.
- **Division des données** en jeux d'entraînement, de validation et de test, avec la même proportion de chats et de chiens dans chaque jeu.
- **Modèle CNN** construit avec Keras : 4 couches Conv2D, MaxPool2D, Dense, Dropout et une sortie sigmoid.
- **Augmentation des données** : rotation, décalage, zoom et retournement horizontal.
- **Callbacks d'entraînement** : EarlyStopping et ReduceLROnPlateau.
- **Évaluation** sur le jeu de test avec rapport de classification (précision, rappel, F1-score).
- **Graphiques d'analyse** : courbes de perte et de précision, matrice de confusion, distribution de confiance du modèle et évolution du taux d'apprentissage.
- **Sauvegarde** du modèle entraîné (`cats_dogs_model.keras`).


---
## Technologies utilisées

| Technologie | Utilisation |
|-------------|-------------|
| **Python 3** | Langage principal |
| **TensorFlow / Keras** | Construction, entraînement et évaluation du CNN |
| **NumPy** | Manipulation des images sous forme de tableaux |
| **Pillow (PIL)** | Ouverture, conversion RGB et redimensionnement des images |
| **pathlib / zipfile** | Extraction de l'archive et parcours des dossiers |
| **scikit-learn** | Division des données, rapport de classification et matrice de confusion |
| **Matplotlib** | Visualisation des images, courbes d'entraînement et histogrammes |
| **Seaborn** | Matrice de confusion sous forme de heatmap |
| **Google Colab / Google Drive** | Exécution du notebook avec GPU et stockage des images |
| **Git / GitHub** | Développement et versionnement , suivi des expériences, un commit par modification |

---
## Installations

Le notebook est conçu pour **Google Colab**. Toutes les librairies utilisées sont déjà installées dans Colab.
 
1. Télécharger le jeu de données [Kaggle Cats and Dogs](https://www.microsoft.com/en-us/download/details.aspx?id=54765) (`kagglecatsanddogs_5340.zip`).
2. Déposer le fichier zip à la racine de son **Google Drive** (`MyDrive`).
3. Ouvrir le notebook avec le bouton **Open in Colab**.
4. Activer le GPU : *Exécution → Modifier le type d'exécution → GPU*.
5. Exécuter toutes les cellules dans l'ordre (*Exécution → Tout exécuter*) et autoriser l'accès à Google Drive lorsque Colab le demande.
> Si le zip est placé ailleurs dans le Drive, modifier la variable `ZIP_PATH` à l'étape 1.
> L'entraînement prend environ **1 minute par époque** avec le GPU de Colab, soit une trentaine de minutes au total.

---
## Le fonctionnement

Le notebook est organisé en 14 étapes :
 
1. **Import des bibliothèques et configuration** : définition du chemin du zip, de la taille des images (`IMG_SIZE = 160`) et du nombre d'images par classe (`MAX_IMAGES_PER_CLASS = 9000`).
2. **Extraction et chargement des données** : montage de Google Drive, extraction du zip et chargement de **18 000 images** (9 000 chats, 9 000 chiens).
3. **Visualisation** : affichage de 10 exemples d'images.
4. **Normalisation** : division des pixels par 255 pour obtenir des valeurs entre 0 et 1.
5. **Division train / validation / test** : 15 % des images pour le test, puis 20 % du reste pour la validation.
   | Jeu | Nombre d'images |
   |-----|----------------:|
   | Entraînement | 12 240 |
   | Validation | 3 060 |
   | Test | 2 700 |
6. **Construction du modèle CNN** :
   | Couche | Détail |
   |--------|--------|
   | Conv2D + MaxPool2D | 32 filtres |
   | Conv2D + MaxPool2D | 64 filtres |
   | Conv2D + MaxPool2D | 128 filtres |
   | Conv2D + MaxPool2D | 256 filtres |
   | Flatten | — |
   | Dense | 256 neurones, ReLU |
   | Dropout | 0,5 |
   | Dense (sortie) | 1 neurone, sigmoid |
   Compilé avec l'optimiseur **Adam** (`learning_rate = 0.0005`) et la perte `binary_crossentropy`, pour un total de **4 583 233 paramètres**.
7. **Augmentation des données et callbacks** : rotation jusqu'à 40°, décalages de 20 %, zoom de 20 % et retournement horizontal. EarlyStopping arrête l'entraînement si `val_loss` ne s'améliore pas pendant 8 époques, et ReduceLROnPlateau divise le taux d'apprentissage par 2 si `val_loss` stagne pendant 4 époques.
8. **Entraînement** : 30 époques avec des lots de 32 images.
9. **Graphiques de la perte et de la précision** pour le train et la validation.
10. **Évaluation sur le jeu de test** et rapport de classification.
11. **Sauvegarde** du modèle dans `cats_dogs_model.keras`.
12. **Matrice de confusion visuelle** (heatmap).
13. **Distribution de confiance du modèle** (histogramme des probabilités par classe).
14. **Évolution du taux d'apprentissage** au fil des époques.

---
## Modifications
 
Chaque modification a été testée séparément et a fait l'objet d'un commit distinct.
 
| # | Modification | Changement |
|---|--------------|------------|
| 1 | Nombre d'époques | 30 → 50 |
| 2 | Taux d'apprentissage | 0,001 → 0,0005 |
| 3 | Architecture | Ajout d'une couche `Conv2D(256)` + `MaxPool2D(2)`, `Dense(256)` |
| 4 | Dropout | 0,5 → 0,6 |
| 5 | Nombre d'images | 2 000 → 4 000 par classe |
 
### Meilleure configuration
 
| Paramètre | Modèle de base | Configuration retenue |
|-----------|----------------|-----------------------|
| `MAX_IMAGES_PER_CLASS` | 2 000 | **9 000** |
| `IMG_SIZE` | 128 | **160** |
| Couches de convolution | 32, 64, 128 | **32, 64, 128, 256** |
| Couche Dense | 128 | **256** |
| Learning rate | 0,001 | **0,0005** |
| `rotation_range` | 20 | **40** |
| **Précision sur le test** | 77,17 % | **94,22 %** |
 
---
 
## Résultats
 
### Entraînement
 
Après 30 époques, le modèle atteint **91 %** de précision sur l'entraînement et **92,8 %** sur la validation. Les courbes de perte et de précision du train et de la validation évoluent ensemble, sans signe marqué de surapprentissage.
 
<!-- ![Courbes de perte et de précision](images/courbes_entrainement.png) -->
 
### Évaluation sur le jeu de test
 
**Précision : 94,22 %** — perte : 0,1536
 
| Classe | Précision | Rappel | F1-score | Support |
|--------|----------:|-------:|---------:|--------:|
| Chat | 0,94 | 0,94 | 0,94 | 1 350 |
| Chien | 0,94 | 0,94 | 0,94 | 1 350 |
 
### Matrice de confusion
 
|  | Prédit Chat | Prédit Chien |
|--|------------:|-------------:|
| **Vrai Chat** | 1 273 (94,3 %) | 77 (5,7 %) |
| **Vrai Chien** | 79 (5,9 %) | 1 271 (94,1 %) |
 
Les erreurs sont presque également réparties entre les deux classes : le modèle n'a pas de biais marqué envers les chats ou les chiens.
 
 
### Distribution de confiance
 
La grande majorité des prédictions se situe près de 0 (chat) ou de 1 (chien), ce qui montre que le modèle est confiant dans ses réponses. Peu de prédictions tombent autour du seuil de 0,5.
 
 
### Taux d'apprentissage
 
Le taux d'apprentissage est resté à 0,0005 pendant les 30 époques : la perte de validation a continué de s'améliorer, donc ReduceLROnPlateau n'a jamais eu besoin de le réduire.

---
 
