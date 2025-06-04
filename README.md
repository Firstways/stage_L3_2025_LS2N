# Stage_L3_2025_LS2N

## Présentation du repos
Architecture des fichiers:
```
-ML-DOCTOR
-FL
  -stl10_cnn
  -stl10_fmnist
  -utkface_cnn
  -......
```
Ce repo contient 2 dossiers : 
- L'un contenant le code de ML doctor comme suit
- L'autre contenant les différents scripts pour faire sauvegarder les modèles fédéré avec différents dataset

## Utilisation 

On peut soit utiliser ML-Doctor comme dans la version de base disponible à cette adresse.
```
https://github.com/liuyugeng/ML-Doctor
```
Sinon on peut charger dans le dossier ML-Doctor/demoloader/trained_model/ un modèle en .pth.
Où encore entraîner un modèle avec les scripts dans FL pour entraîner et sauvegarder un modèle que l'on pourra ensuite utiliser avec ML-Doctor

Concernant l'utilisation des scripts pour l'apprentissage fédéré. Il y'a 3 paramètres importants dans la deuxième cellule
- NUM_CLIENTS : Définit le nombre de client.
- BATCH_SIZE : Taille du batch. Attention plus le nombre de client est important lors de l'entrainement et de l'évaluation plus la taille du batch doit etre petit.
- MAX_ROUND : Nombre de rounds d'entrainement du serveur centrale

### Strategy
La strategy utilisé dans mes scripts est FedAvg. C'est-à-dire que le serveur met à jour ses poids selon la moyenne de tous les poids reçus.

**Le nom du fichier contenant le modèle doit être au format dataset+model_path**

## Modification du code source de ML-Doctor
Dans cette section, je vous explique dans les grandes lignes les modifications que j'ai apportées par rapport au code source.

- Ajout du paramètre "model_path" qui contient la deuxième partie du fichier qui contient le modèle à tester. le nom du fichier source
- Ajout de la fonction def test_meminf_with_custom_model(...) pour charger le modèle avec le 
- Modification de la classe UTKFaceDataset
- Ajout de la clase EdgeIIot **Attention à cette classe, elle n'a pas été testée correctement**
- Ajout de la classe MLP

## Script FL
Dans le dossier script FL, il y'a 5 scripts pour entrainer des modèles fédéré à savoir:
- Le dataset edgeIIot avec un MLP
- le dataset FMNIST avec alexnet
- Le dataset FMNIST avec un simple cnn
- Le dataset STL10 avec un simple cnn
- le dataset UTKFace avec un simple cnn

Le dernier script est mon script pour le préprocess de edgeIIot.
