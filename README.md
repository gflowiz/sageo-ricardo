

![](https://i.imgur.com/KgD2D99.png)

*Arabesque* quick tutorial (v.0)

**Réalisation :** Equipe gflowiz, 2019.

**Licence :** [CC-BY-SA 3.0-FR](https://creativecommons.org/licenses/by-nc-sa/3.0/fr/).


## Introduction générale

***arabesque*** est une application web de cartographie thématique des flux développée dans le cadre du projet gflowiz. (Voir [le blog du projet](https://geoflowiz.hypotheses.org) pour plus de détails. 

Arabesque est disponible gratuitement à l'adresse suivante : [http://arabesque.ifsttar.fr/](http://arabesque.ifsttar.fr/) 

Elle fonctionne avec Chromium et Mozilla. La [documentation générale (travail en cours)](https://gflowiz.github.io/arabesque/) et le code informatique sont disponibles sur le dépôt suivant : https://github.com/gflowiz/arabesque

Pour ce tutoriel, nous avons utilisé les flux commerciaux historiques répertoriés dans la base de données [RICARDO](http://ricardo.medialab.sciences-po.fr/#/). Les fichiers utilisés sont disponibles dans ce dépôt et ont la structure suivante :

- [SAGEO_RICardo_nodes.csv](https://raw.githubusercontent.com/gflowiz/sageo-ricardo/master/SAGEO_RICardo_nodes.csv) : fichiers de localisation géographique des entités
	- id (identifiant de l'entité géographique)
	- name (nom de l'entité géographique)
	- type (type de l'entité : country, city, ...)
	- continent (continent)
	- lat (latitude)
	- long (longitude)

- [SAGEO_RICardo_edges_small.csv](https://raw.githubusercontent.com/gflowiz/sageo-ricardo/master/SAGEO_RICardo_edges_small.csv) : flux commerciaux historiques agrégés (pour réduire la taille du jeu de données)
	- idorigine (identifiant de l'entité d'origine du flux)
	- iddestination (identifiant de l'entité de destination du flux)
	- volume (volume financier du flux en Livre sterling)
	- decennie (décennie concernée par le flux)


- [SAGEO_RICardo_edges_nona.csv](https://raw.githubusercontent.com/gflowiz/sageo-ricardo/master/SAGEO_RICardo_edges_nona.csv) : flux commerciaux historiques non agrégés
	- idorigine (identifiant de l'entité d'origine du flux)
	- iddestination (identifiant de l'entité de destination du flux)
	- volume (volume financier du flux en Livre sterling)
	- annee (année de l'échange)
	- periode (période de l'échange)
	- decennie (décennie de l'échange)


***arabesque*** vous permet également d'importer vos propres ensembles de données de flux, sous la forme d'une matrice origine-destination (format liste d'adjacence en CSV), de les explorer, de les filtrer pour créer une carte de flux lisible, en accord avec les principes de la sémiologie cartographique.

La réalisation d'une carte de flux avec arabesque se décompose en 5 grandes étapes :


1. Importation des données de flux (liens et/ou noeuds)
2. Traitement des données de flux (création d'indicateurs, statistiques)
3. Exploration et filtrage des données
4. Symbolisation graphique
5. Exportation


## 1. Importation de données

Pour une première découverte d' ***Arabesque***, vous pouvez utiliser les jeux de données fournis comme exemple dans la section **Démo**. 

![](https://i.imgur.com/LdUeTbj.png)

#### 1.1 Données OD (Origine/Destination)

Arabesque nécessite le chargement d'au moins un ensemble de données de flux : un fichier de lien. au format CSV (séparateur : virgule) et format long. 

Vous devez également déclarer les 3 champs minimums requis pour la cartographie des flux : ceux correspondant aux lieux d'origine, aux lieux de destination et aux valeurs de flux. 

Si la matrice OD est temporelle ou disponible pour différentes catégories, vous devez également choisir une méthode d'agrégation.

Sur la page d'accueil d'([Arabesque](http://arabesque.ifsttar.fr/)), chargez au moins un ensemble de données de flux.

![](https://i.imgur.com/BjvHVHn.png)

**Application**

Chargement des données *SAGEO_RICardo_edges_small.csv*

![](https://i.imgur.com/GjzU9IE.png)

### 1.2. Données géographiques

Si vous avez des données de localisation associées à vos OD, vous pouvez charger les fichiers de nœuds correspondants par "**import Location**", sinon vous pouvez utiliser des localisations pré-définies avec "**Preset Location**".

#### 1.2.1. **Importer les données de localisation**

Si vous sélectionnez "**Import Location**", vous devez charger un fichier GEOJSON ou CSV, puis choisir l'ID des nœuds et leurs coordonnées géographiques lat/long.

**Application**

Chargement des données *SAGEO_RICardo_nodes.csv*

![](https://i.imgur.com/MMhQw1E.png)

#### 1.2.2. **Localisation prédéfinie**

Lorsque vous sélectionnez "**Preset Location**", il vous suffit de choisir le niveau, la région et le code des nœuds géo-numériques correspondants (si disponible). 

![](https://i.imgur.com/c1kEI4g.png)

![](https://i.imgur.com/wUzQPCM.png)

Après le chargement des fichiers de liens et de nœuds, l'application effectue automatiquement une jointure d'attribut entre les deux fichiers. 

Les liens qui n'ont pas d'ID d'origine ou de destination sont automatiquement supprimés, de même pour les nœuds.

La liste des noeuds et liens supprimés est alors affichée, uniquement pour consultation - vous devez la copier si vous souhaitez conserver la liste.

![](https://i.imgur.com/ID0iSq6.png)

## 2. Présentation de l'interface

### Calcul automatique d'indicateurs

Les jeux de données sont automatiquement modifiés lors de leur importation, l'application calcule différents indicateurs - qui sont disponibles dans une liste pouvant être téléchargée au format CSV (Voir sections Export et sauvegarde):

**Indicateurs sur les liens :**
distance euclidienne entre les entités d'origine et de destination

**Indicateurs sur les noeuds :**
Exemple d'indicateurs additionnels calculés sur les noeuds (données RIcardo)

![](https://i.imgur.com/ygefevd.png)

### Symbolisation automatique

Carte réalisée par défaut lors de l'arrivée sur l'interface.

![](https://i.imgur.com/vzw3sW0.png)

L'interface est composée des deux panneaux suivantes.

## 2.1. Panneau de gauche

La gestion des couches est réalisée sur la partie de gauche de l'interface. Elle composée de deux sous-parties:

### Généralités

- Projections
- Titre
- Gestion et symbolisation des couches (*Add Layers*)

### Manipulation, disposition et affichage des couches

- Liens
- Noeuds
- autres couches


## 2.2. Partie centrale de l'interface

La partie centrale correspond à la vue cartographique. Elle résulte du choix des couches à afficher (réalisé sur la partie gauche) et du filtrage des valeurs des liens et des noeuds (réalisé sur la partie droite).

Elle présente en outre différents boutons permettant la mise en oeuvre d'actions primaires.

### 2.2.1. Actions primaires

![](https://i.imgur.com/UpnYI1v.png) Icône permettant de revenir à la [page d'accueil](arabesque.ifsttar.fr) pour commencer une nouvelle visualisation.

![](https://i.imgur.com/Yxwnchy.png) Boutons permettant de réaliser successivement des zooms avant et après de la vue - de la même façon qu'avec la molette de la souris.

![](https://i.imgur.com/YEVxD9F.png) Bouton permettant de sauvegarder le projet pour pouvoir l'utiliser ultérieurement.

![](https://i.imgur.com/SFBC4Vj.png) Bouton visant à exporter la carte au format image (.PNG), en incluant les légendes et les sources des contributeurs pour les fonds externes tels que *NaturalEarth*, par exemple.

![](https://i.imgur.com/mGCeFIv.png) Bouton entraînant le recentrage et l'affichage de l'emprise totale des flux - sans zoomer/dé zoomer ni paner.

![](https://i.imgur.com/imemU85.png) Bouton servant à exporter les données filtrées - celles qui sont visibles sur la carte - sous la forme d'un fichier liste au format .JSON.

![](https://i.imgur.com/dyE0LNv.png) Bouton permettant d'afficher / masquer la légende.

![](https://i.imgur.com/PH3ohE5.png) Bouton permettant de passer en mode d'affichage en plein écran - avec fond noir.

![](https://i.imgur.com/vVdZkTe.png) Bouton permettant d'ouvrir ou de fermer les panneaux  situés de chaque coté de la carte.

### 2.2.2. Légende

Une légende est générée automatiquement pour chaque carte, elle reprend les éléments de symbolisation (taille, couleur et opacité) présents sur la carte pour symboliser les indicateurs présentés. Ici, le volume des flux et le nombre de degrés des lieux. 


## 2.3. Panneau de droite
**L'exploration et le filtrage** des données est effectuée sur la partie droite. 

Elle permet d'agir sur n'importe laquelle des variables caractérisant les noeuds et/ou les liens et/ou la distance parcourue par les flux (variable calculée lors du chargement des données). 

Les résultats de l'application d'un ou de plusieurs filtres sont proposés par défaut en tête du panneau.

![](https://i.imgur.com/22lK9lX.png)


# 3. Projection 

Pour les données observées **à l'échelle mondiale ou régionale (sub-continentale)**, il est possible de changer la projection du fond de carte proposé ou de la vue affichée - pour les données locales, il est possible d'ajouter des tuiles vectorielles (voir section 5.5).

Pour cela, il faut soit sélectionner le système de projection dans une liste pré-établie, soit  renseigner directement son code EPSG identifiant (*European Petroleum Survey Group*).

Exemple : World Mollweide
(EPSG Correspondant : 54009)

![](https://i.imgur.com/jnnRjBi.png)


# 4. Ajout d'un titre

Il est possible d'ajouter un titre simple sur la vue principale.

# 5. Symbolisation et gestion des couches géographiques

Il est possible d'agir sur la symbolisation graphique des différentes couches dessinées en :
-- modifiant leur apparence ;
-- ajouter de nouvelles couches qui serviront d'habillage ;
-- gérant la disposition des différentes couches

![](https://i.imgur.com/8FmSnxG.png)


## 5.1. Symbolisation des noeuds
![](https://i.imgur.com/isQCzon.png)

La symbologie des noeuds consiste à paramétrer leur dessin, et à appliquer des variables visuelles permettant d'enrichir qualitativement la carte. 

### 5.1.1. Couleur

**Couleur / Fixe** :
La teinte est identique pour tous les noeuds.
![](https://i.imgur.com/9vC9K7s.png)

**Application sur les noeuds** : symbolisation des noeuds (barycentre des zones) avec une *forme* cercle (choix unique) de *taille* fixée et de teinte unique noire.

![](https://i.imgur.com/j8Zm1b8.png)

**Couleur / Variable** : 
La teinte des noeuds ne sera pas identique pour tous, mais basée sur un dégradé de ton prédéfini. Le choix  de la progression (divergente ou non) sera fonction du type de caractère (précisé dans le champs type).

Le choix de nuancer la teinte des noeuds est associé ici à un caractère (ici le nombre de degrés pondéré - *weighted degree*) dont on précise le type (quantitatif).

Idéalement, il est nécessaire de paramétrer simultanément la taille des noeuds, en utilisant le même caractère (ici le nombre de degrés pondéré - *weighted degree*) - sinon, les noeuds conserveront la même taille et le résultat de l'application d'une nuance sera peu visible.

![](https://i.imgur.com/EoiKGIi.png)

### 5.1.2. Taille

**Taille / Fixe** :
La taille (surface) des noeuds est identique pour tous et fixée sur une valeur donnée.
![](https://i.imgur.com/hhNWGt0.png)

**Taille / Variable** 
La taille (surface) des noeuds est variable, selon une fonction (racine, racine carrée ou logarithmique) proportionelle à la valeur d'un caractère (quantitatif discret - de stock).

La correspondance entre les valeurs du caractère et leur symbolisation graphique est paramétrable grâce à l'application d'un *ratio*.

![](https://i.imgur.com/MZgbS9o.png)

Le *ratio* est fixé par défaut à 0,02% de la plus grande dimension du rectangle d’encombrement maximal du jeu de données de flux.

### 5.1.3. Texte
Une étiquette, correspondant aux modalités d'un des champs du jeu de données, peut être ajoutée aux noeuds, sa teinte et son opacité fixées. 

![](https://i.imgur.com/qjg23Xc.png)

### 5.1.4. Opacité
L'opacité consite à agir sur le degré de transparence d'une teinte.

**Opacité / Fixe** :
L'opacité de la teinte des noeuds est identique pour tous les noeuds, elle est paramétrable, entre 0 et 1.

![](https://i.imgur.com/u86Tm0M.png)

**Opacité / Variable** :
L'opacité de la teinte des noeuds est variable, en fonction d'un caractère (ici le degré pondéré, *weighted degree*), selon une fonction (linéaire, carrée, racine carrée et logarithmique) paramétrable, dont il est possible de définir les valeurs minimum et maximum, respectivement 0.25 et 0,85, par défaut.

![](https://i.imgur.com/2zhzEth.png)

**Application sur les noeuds** : symbolisation des noeuds avec une *forme* cercle de *taille* *variable* selon une fonction linéaire, représentée avec une teinte noire nuancée avec variation d'opacité.
![](https://i.imgur.com/UxOvM50.png)


## 5.2. Symbolisation des liens
![](https://i.imgur.com/FrioZff.png)

La symbologie des liens consiste à paramétrer leur dessin, et à appliquer des variables visuelles permettant d'enrichir qualitativement la carte. 

Exemple: lien droits bilatéraux orientés, teinte noire unique 
![](https://i.imgur.com/QLhHhIu.png)

## 5.2.1. Géometrie

**Géométrie / Orientée ** 

La géométrie orientée prend en compte la direction des flux, si nécessaire.

![](https://i.imgur.com/9NkzUkE.png)

**Géométrie / Non Orientée** 

La géométrie orientée ne tient pas en compte de l'éventuelle direction des flux.

## 5.2.2 Type (de géométrie du lien)

Le *type* de la géométrie correspond à l'application de la (variable visuelle) forme du corps du lien, que celui-ci soit orienté ou non.

![](https://i.imgur.com/KLhZnjs.png)

**Type / Droit - "Straight"** 
Le lien est rectilinéaire et orienté, grâce à une demi-tête de flèche

**Type / Droit sans crochet - "Straight no hook"**
Le lien est rectilinéaire et orienté, il présente une pointe sans crochet

**Type / Triangle - "Triangle"**
Le lien est rectilinéaire et prend la forme d'un triangle

**Type / courbe - "Curve"**
Le lien est courbe et orienté, sa courbure est paramétrable.

**Type / Triangle courbe - "Triangle curve"**
Le lien est courbe et prend la forme d'une goutte d'eau, sa courbure est paramétrable.

**Type / Non orienté -  "Non oriented"**
Le lien est droit valué ou non, il ne présente pas d'orientation.

## 5.2.3. Flèche (*Arrow*)

La *flèche* de la géométrie du lien correspond à la (variable visuelle) forme de la tête du lien, lorsque celui-ci est orienté.

La courbure de cette tête est générée, selon l'algorithme de Chaikin qui permet de paramétrer sa hauteur et sa base, par rapport aux corps du lien.

![](https://i.imgur.com/0Dvx8yZ.png)

**Arrow / Hauteur** (*Height curve*): La valeur de la hauteur de la tête est le pourcentage de la distance cartographique du lien (distance entre l'origine et la destination) utilisé pour définir la largeur (cartographique) maximale du lien - la largeur étant elle même fonction de la valeur du flux.

**Arrow / Hauteur** (*Base*) : La valeur de ([0,1]) est celle du centre de la courbe ; le point est identifié par l'indication d'un d'éloignement au nœud d'origine du lien.

## 5.2.4. Couleur

**Couleur / Fixe** :
La teinte des liens est identique pour tous.


**Couleur / Variable** : 
La teinte des liens n'est pas identique pour tous, elle est basée sur un dégradé de ton prédéfini. Le choix  de la progression (divergente ou non) sera fonction du type de caractère (précisé dans le champs type).

Le choix de nuancer la teinte des liens est associé ici à un caractère (pseudo) continu dont il est nécessaire de préciser le type (quantitatif).

Idéalement, il est nécessaire de paramétrer simultanément la *taille* des liens, en utilisant un caractère discret (ici le nombre de degrés pondéré - *weighted degree*) et leur couleur en utilisant un caractère continu (rapport ou taux) - sinon, les liens conserveront la même taille et le résultat de l'application d'une nuance sera peu visible.

### 5.3.5. Taille (*size*)

![](https://i.imgur.com/B0xJk9K.png)


![](https://i.imgur.com/6UvEj9J.png)


**Application sur les liens** : symbolisation des liens avec une *forme* *triangle* *courbe* avec une *couleur* *variable* selon une fonction linéaire et présentant une variation *d'opacité*

Paramètres : 
![](https://i.imgur.com/orgWxLd.png)

Carte résultat :

- Sommets placés sous les noeuds
![](https://i.imgur.com/mSOYw2m.png)

- Sommets placés sur les noeuds (voir section gestion des dispositions)
![](https://i.imgur.com/Jn0EtxU.png)

## 5.4. Ajout d'un fond géonumérique

![](https://i.imgur.com/cD3vUpZ.png)
 
Différents fonds de carte ou éléments d'habillage vectoriels, préchargés sont proposés. Leur sélection est réalisée à partir d'une liste.

![](https://i.imgur.com/ywcdDkM.png)
 
La symbolisation de ce nouveau fond d'habillage peut être modifiée en paramétrant l'apparence du dessin de ses contours et fonds, de sa teinte et de son opacité.

Il est également possible d'importer un fond en indiquant son URL : ![](https://i.imgur.com/SQPqh0V.png)

**Applications sur la vue en cours**

- Ajout d'une *bounding box*, symbolisation graphique et disposition en arrière-plan (voir section Gestion des dispositions).
![](https://i.imgur.com/Vw1HWsA.png)

- Ajout de lignes *graticules_20*, symbolisation graphique et disposition au-dessus de la *bounding box* (voir section Gestion des dispositions). 

![](https://i.imgur.com/e5A8SU4.png)

![](https://i.imgur.com/Kwpl7fg.png)

- Ajout d'une couche *land* (espaces continentaux), symbolisation graphique et placement au-dessus de la couche graticules_20

![](https://i.imgur.com/45HJTPe.png)

![](https://i.imgur.com/EHOCgSR.png)

## 5.5. Ajout de couches de tuiles

Pour les données observées à l'échelle locale, il est possible d'ajouter des couches tuiles - la mention des contributeurs sera alors insérée automatiquement sur la carte, en bas à droite.

![](https://i.imgur.com/nSUHJFe.png)

Plusieurs tuiles sont proposées, elles sont triées par fournisseur ...

![](https://i.imgur.com/ENIQ2fm.png)

.. et par type de tuile (texte - Fond de carte)
![](https://i.imgur.com/AK27WOr.png)


### 5.5.1. Exemple de chargement de tuiles

1. Selectionner Carto_basemap dans **Type**
2. Selectionner Carto_Dark_NoLabel dans **tiles**
3. Cliquer sur ![](https://i.imgur.com/3l7BA9c.png)
4. Un fond de carte vient alors recouvrir la carte affichée sur la partie centrale, cachant alors les flux. 
5. Il faut ensuite gérer la disposition des couches pour parfaire l'affichage.


### 5.5.2. Ajout de ses propres tuiles
Il est également possible d'ajouter ses propres tuiles *via* un géo serveur, en cliquant sur ![](https://i.imgur.com/E3zgsmo.png)
  
  
## 6. Import d'une couche .GEOJSON
![](https://i.imgur.com/UuZhMyC.png)

Quelle que soit l'échelle (mondiale, régionale ou locale) il est possible d'ajouter un fond de carte vectoriel quelcoque, au format geojson.

Pour cela,il faut charger son ficher et le nommer.

![](https://i.imgur.com/ZKKAbUA.png)
  
Ensuite, il est possible de modifier son dessin, sa couleur de fond et de contour. 

## 7. Gestion et disposition des couches

L'ajout de couches d'information contribue à masquer les couches initiales de noeuds et de liens ; les dernières couches ajoutées s'étant placées au premier plan. 

![](https://i.imgur.com/eNnmz1d.png)


## 7.1. Modifier la disposition des couches

Pour rendre les flux visibles, il convient de modifier la disposition des différentes couches, en changeant leur ordre - par glisser / déplacer (*drag & drop*).

1. Cliquer sur la couche ***link*** et la maintenir  appuyée ;
2. Glisser / déplacer la couche ***link*** et la placer au premier plan ;
3. Relacher la couche ;
4. Répéter la même opération avec la couche ***node*** si nécessaire.

![](https://i.imgur.com/qUAGkWr.png)

On observe ainsi que la couche des flux vient d'être mis au premier plan.

## 7.2. Gérer l'apparence des couches

Les vignettes correspondant aux différentes couches présentent des icônes permettant de gérer leur apparence.

![](https://i.imgur.com/sRwvjfl.png) : Masquer une couche

![](https://i.imgur.com/VEMrle9.png) : Afficher (rendre visible) une couche

![](https://i.imgur.com/SQAxmbQ.png) : Supprimer une couche

![](https://i.imgur.com/PqDUB2L.png) : Paramétrer une couche de liens

![](https://i.imgur.com/Qwi9fas.png) : Modifier l'apparence d'une couche de liens


### 7.2.1 Paramétrer une couche de liens

L'apparence des couches de liens (forme, couleur, opacité, taille) peut être modifiée à deux moments : soit lors de l'import, ou de la création de la couche - ce qui entraînera alors la suppression de la couche actuelle - (voir section 5.2), soit lors de la gestion des couches affichées, en agissant sur les icônes : ![](https://i.imgur.com/DXbDiWu.png)

**Modifier le style des liens**
Le bouton ![](https://i.imgur.com/itTCnJI.png) permet d'accéder à la fenêtre de paramétrage du style de la couche de liens.

![](https://i.imgur.com/5Pz6Q2H.png)

**Modifier le style des flèches**

Le bouton ![](https://i.imgur.com/Qwi9fas.png) permet de modifier le style des flèches


![](https://i.imgur.com/5EqW8k8.png)

# 8. Filtrage des couches numériques

Il est réalisé soit visuellement à l’aide d’une fenêtre de sélection sur un histogramme interactif à fenêtre coulissante (*slider*), soit de manière numérique (en indiquant un seuil). 

La part d’information sélectionnée, les valeurs minimales et maximales sont indiquées automatiquement sur la figure. Pour les liens, la possibilité d’un filtrage selon la distance géodésique parcourue est en outre proposée.

![](https://i.imgur.com/6E2Tgpg.png)

**Application sur la vue en cours**
L'affichage des filtres par défaut est le suivant.

![](https://i.imgur.com/1zSEsXa.png)

L'application précise littéralement les valeurs de filtrage :

- la part en pourcentage de liens (figurés) représentée (ici 10% de l'ensemble des liens)
- la part en pourcentage du total de l'information de flux (valeur) représentée (83,5%)
- la part en pourcentage de l'ensemble des noeuds : 36,5%

>>***Commentaire*** : *84% de l'information de flux est échangée entre 36% des lieux qui représentent les 10% de liens les plus forts, en volume - seul un tiers des lieux est impliqué dans ces échanges.*

## 8.1. Filtrage numérique
Il est possible de modifier ces paramètres de filtrage, en agissant sur les données de flux (liens ou noeuds)

![](https://i.imgur.com/8w3HdbN.png)

### 8.1.1. Modification des paramètres de filtrage sur le volume

- Représentation de l'ensemble des échanges
![](https://i.imgur.com/050JPXs.png)

- Sélection des 25% des échanges les plus importants,soit 8% des noeuds et 0,6% des liens les plus forts

![](https://i.imgur.com/wCrEodP.png)

- Sélection des 50% des échanges les plus importants,soit 14% des noeuds et 2% des liens les plus forts

![](https://i.imgur.com/b2IrUaK.png)

### 8.1.2. Création d'un filtre sur les liens, selon la distance parcourue

![](https://i.imgur.com/1csaKil.png)

![](https://i.imgur.com/ujHbtWE.png)

- Modification des paramètres de distance parcourue

Sélection des flux parcourant entre 4000 et 12000 kilomètres

![](https://i.imgur.com/iWPJh5W.png)

- Résultat

>> ***Commentaire*** : la sélection des flux commerciaux qui parcourent de l'ordre de 4000 à 12000 kilomètres de distance correspond aux flux commerciaux à moyenne distance, qui s'expriment principalement dans l'hémisphère nord..
Ces flux de moyenne distance représentent 34% du volume total de marchandises qui correspond à 25% des relations financières commerciales les plus importantes, qui s'expriment entre 4% des pays les plus riches. 
On notera que seules l'Amérique du nord et des pays de l'Europe de l'ouest sont impliqués dans ces échanges - dont on rappelle qu'ils correspondent au cumul des valeurs observées sur l'ensemble de la période.

![](https://i.imgur.com/Yst7lLx.png)

### 8.1.3. Création d'un double filtrage sur les liens, selon le volume et la distance parcourue**

Pour appliquer un double filtrage, il suffit d'ajouter deux filtres différents sur les liens, puis de paramétrer chacun d'entre eux. 

**Application sur la vue en cours**

Distance parcourue inférieure à 8000 km (de moyenne à petite longue distance)
Volume total échangé supérieur à 47 millions (paramètre empirique, pris au hasard)

![](https://i.imgur.com/XBXyVmt.png)

![](https://i.imgur.com/J0C06iJ.png)

>> **Commentaire** : les échanges qui s'expriment à moyenne voire longue distance (moins de 8000 km environ) et qui représentent plus de 48 millions de livres sterling échangés correspondent à 50% du total de ces interactions commerciales qui sont réalisées entre les 16% de noeuds les plus importants.

## 8.2. Filtrage temporel

Les données étant découpées dans le temps, il est possible de sélectionner une ou plusieurs dates à représenter. 
Les paramètres décrivant la part d'information représentée sont alors actualisés.

**Application sur la vue en cours**

![](https://i.imgur.com/zOBliM3.png)

# 9. Export et sauvegarde

![](https://i.imgur.com/FVYk6Ji.png) Bouton permettant d'exporter une carte au format image (.PNG).

![](https://i.imgur.com/X6xDvlv.png) Bouton permettant d'exporter la carte au format .ZIP.

Pour ouvrir une carte sauvegardée, il faut charger le fichier .ZIP de sauvegarde - et ne pas l'avoir modifié entre temps.
![](https://i.imgur.com/Chfa3pP.png) 


###### tags: `Templates` `Documentation` `tutorial` `arabesque` `gflowiz`

