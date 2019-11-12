---
title: 'arabesque tutorial: quick documentation'
disqus: hackmd
---

![](https://i.imgur.com/KgD2D99.png)

*Arabesque* quick tutorial (v.0)
===
![downloads](https://img.shields.io/github/downloads/atom/atom/total.svg)
![build](https://img.shields.io/appveyor/ci/:user/:repo.svg)
![chat](https://img.shields.io/discord/:serverId.svg)

## Contents

[TOC]

## Introduction générale

***arabesque*** is a web application for thematic flow mapping developped, developed as part of the *geographic flow visualisation (gflowiz project)*. See: https://geoflowiz.hypotheses.org for details. 

arabesque is available free of charge at the following address: http://arabesque.ifsttar.fr/ 

It is working with Chromium and Mozilla 

The general documentation (work in progress) and computer code are provide on the following repository: https://github.com/gflowiz/arabesque

***arabesque*** allows you to import your own flow datasets, in the form of an origin-destination matrix (list format in CSV), explore them, filter them to create a readable flow map, in accordance with the principles of cartographic semiology

The realization of a flowmap in arabesque is composed of 5 steps:
1: Importing flow data
2: flow data Data processing
(creation of indicators, statistics)
3: Data mining and filtering
4: Graphical Symbolisation
5: Export


## 1. Data importation

For a first discovery of ***arabesque***, you can use the data sets provided as example in the **Demo section**. 

![](https://i.imgur.com/LdUeTbj.png)

For this tutorial, we used the French national commuting in 2015 (flows up to 100 commuters).

Source : Mobilités professionnelles en 2015 : déplacements domicile - lieu de travailRecensement de la population - Base flux de mobilité (INSEE, 2015). https://www.insee.fr/fr/statistiques/fichier/3566477/base-excel-flux-mobilite-domicile-lieu-travail-2015.zip

### 1.1 Link dataset

arabesque requires loading at least one set of flow data : a .CSV link file (separator : comma) in long format. 

You must also declare the 3 minimum fields required for flow mapping: those corresponding to the places of origin, the places of destination, and the flow values. 

If the OD the matrix is temporal or categorical, you must also choose and aggregation method if necessary.

On the home page of arabesque ([arabesque](http://arabesque.ifsttar.fr/)) select at least a link flow dataset and 

![](https://i.imgur.com/7ovFJ1V.png)

### 1.2. Node dataset

If you have locationnal data associated to your OD links, you can load the corresponding nodes files  by "**import Location**", else you can "**Preset Location**".

#### 1.2.1. **Import Location**

If selecting "**Import Location**", you have to load a GEOJSON file, then choose the nodes ID and their lat/long geographical coordinates

![](https://i.imgur.com/RAIFQ3t.png)

#### 1.2.2. **Preset Location**

When selecting "**Preset Location**", you just have to choose the corresponding geonumerical nodes level, region and code (if available yet,otherwise you need to load your own node file). 

![](https://i.imgur.com/c1kEI4g.png)

![](https://i.imgur.com/wUzQPCM.png)

After loading the links and nodes files,the application automatically performs an attribute join between the two files. 

Links that do not have an origin or destination ID are automatically deleted, similarly for the nodes.

The complete list of removed is then proposed, only for viewing - so you must copy it if you want to keep the list

![](https://i.imgur.com/ID0iSq6.png)

By clicking ok, you enter directly in the arabesque interface.

## 2. Présentation de l'interface

After loading the data, you enter you enter directly into the application, which offers a first map with default settings.

![](https://i.imgur.com/vzw3sW0.png)

The interface is composed of the following two sections.

## 2.1. Panneau de gauche

La gestion des couches est réalisée sur la partie de gauche de l'interface. Elle composée de deux sous-parties:
-- Projections
-- Titre
-- Gestion et symbolisation des couches (*Add Layers*)

Manipulation, disposition et affichage des couches
-- Liens
-- Noeuds
-- autres couches


## 2.2. Partie centrale de l'interface

La partie centrale correspond à la vue cartographique. Elle résulte du choix des couches à afficher (réalisé sur la partie gauche) et du filtrage des valeurs des liens et des noeuds (réalisé sur la partie droite).

Elle présente en outre différents boutons permettant la mise en oeuvre d'actions primaires.

### 2.2.1. Actions primaires

![](https://i.imgur.com/UpnYI1v.png) Icône permettant de revenir à la page d'accueil arabesque.ifsttar.fr pour commencer une nouvelle visualisation.

![](https://i.imgur.com/Yxwnchy.png)Boutons permettant de réaliser successivement des zooms avant et après de la vue - de la même façon qu'avec la molette de la souris.

![](https://i.imgur.com/YEVxD9F.png) Bouton permettant de sauvegarder le projet pour pouvoir l'utiliser ultérieurement.

![](https://i.imgur.com/SFBC4Vj.png) Bouton visant à exporter la carte au format image (.PNG), en inclant les légendes et les sources des contributeurs pour les fonds externes tels que *NaturalEarth*, par exemple.

![](https://i.imgur.com/mGCeFIv.png) Bouton entraînant le recentrage et l'affichage de l'emprise totale des flux - sans zoomer/dé zoomer ni paner.

![](https://i.imgur.com/imemU85.png) Bouton servant à exporter les données filtrées - celles qui sont visibles sur la carte - sous la forme d'un fichier liste au format .JSON.

![](https://i.imgur.com/dyE0LNv.png) Bouton permettant d'afficher / masquer la légende.

![](https://i.imgur.com/vVdZkTe.png) Bouton permettant d'ouvrir ou de fermer les panneaux  situés de chaque coté de la carte.

### 2.2.2. Légende

Une légende est générée automatiquement pour chaque carte, elle reprend les éléments de symbolisation (taille, couleur et opacité) présents sur la carte pour symboliser les indicaters présentés. Ici, le volume des flux et le nombre de degrés des lieux. 


## 2.3. Panneau de droite
**L'exploration et le filtrage** des données est effectuée sur la partie droite. 

Elle permet d'agir sur n'importe laquelle des variables caractérisant les noeuds et/ou les liens et/ou  la distance parcourue par les flux (variable calculée lors du chargement des données). 

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

Exemple : Résultat 
![](https://i.imgur.com/UxOvM50.png)


## 5.2. Symbolisation des liens
![](https://i.imgur.com/FrioZff.png)

La symbologie des liens consiste à paramétrer leur dessin, et à appliquer des variables visuelles permettant d'enrichir qualitativement la carte. 

## 5.2.1. Géometrie

**Géométrie / Orientée ** 

La géométrie orientée prend en compte la direction des flux, si nécessaire.

![](https://i.imgur.com/9NkzUkE.png)

**Géométrie / Non Orientée** 

La géométrie orientée ne tient pas en compte de l'éventuelle direction des flux.

## 5.2.2 Type (de géométrie du lien)

Le *type* de la géométrie correspond à l'application de la (variable visuelle) forme du corps du lien, que celui-ci soit orienté ou non.

**Type / Droit** 
Le lien est rectilinéaire et orienté, grâce à une demi-tête de flèche
![](https://i.imgur.com/oZeAQh3.png)

**Type / Droit sans crochet**
Le lien est rectilinéaire et orienté, il présente une pointe sans crochet
![](https://i.imgur.com/AV8uFxA.png)

**Type / Triangle**
Le lien est rectilinéaire et prend la forme d'un triangle
![](https://i.imgur.com/4zLzaXE.png)

**Type / courbe**
Le lien est courbe et orienté, sa courbure est paramétrable.
![](https://i.imgur.com/rjcZ9nj.png)

**Type / Triangle courbe**
Le lien est courbe et prend la forme d'une goutte d'eau, sa courbure est paramétrable.
![](https://i.imgur.com/1vYWl6V.png)

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



## 5.4. Ajout d'un fond géonumérique

![](https://i.imgur.com/cD3vUpZ.png)
 
Différents fonds de carte ou éléments d'habillage vectoriels, préchargés sont proposés. Leur sélection est réalisée à partir d'une liste.

![](https://i.imgur.com/ywcdDkM.png)
 
La symbolisation de ce nouveau fond d'habillage peut être modifiée en paramétrant l'apparence du dessin de ses contours et fonds, de sa teinte et de son opacité.

Ex : choix d'ajouter une "bounding box" qui correspond à l'espace de définition de la carte, et symbolisation du fond en bleu.

![](https://i.imgur.com/HUHohCU.png)

Il est également possible d'importer un fond en indiquant son URL : ![](https://i.imgur.com/SQPqh0V.png)

## 5.5. Ajout de couches de tuiles

Pour les données observées à l'échelle locale, il est possible d'ajouter des couches tuiles - la mention des contributeurs sera alors insérée automatiquement sur la carte, en bas à droite.

![](https://i.imgur.com/nSUHJFe.png)

Plusieurs tuiles sont proposées, elles sont triées par fournisseur 

![](https://i.imgur.com/ENIQ2fm.png)

et par type de tuile (texte - Fond de carte)
![](https://i.imgur.com/AK27WOr.png)


### 5.3.2. Exemple de chargement de tuiles
1. Selectionner Carto_basemap dans **Type**
2. Selectionner Carto_Dark_NoLabel dans **tiles**
3. Cliquer sur ![](https://i.imgur.com/3l7BA9c.png)
4. Un fond de carte vient alors recouvrir la carte affichée sur la partie centrale, cachant alors les flux. 
5. Il faut ensuite gérer la disposition des couches pour parfaire l'affichage.


### 5.3.3. Ajout de ses propres tuiles
Il est également possible d'ajouter ses propres tuiles *via* un géo serveur, en cliquant sur ![](https://i.imgur.com/E3zgsmo.png)
  
  
## 5.5. Import d'une couche .GEOJSON
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

![](https://i.imgur.com/6E2Tgpg.png)


Le filtrage numérique s’applique aux données de flux (liens ou noeuds) 

![](https://i.imgur.com/8w3HdbN.png)

>> Sélection des variables

Il est réalisé soit visuellement à l’aide d’une fenêtre de sélection sur un histogramme interactif à fenêtre coulissante (*slider*), soit de manière numérique (en indiquant un seuil). 

La part d’information sélectionnée, les valeurs minimales et maximales sont indiquées automatiquement sur la figure. Pour les liens, la possibilité d’un filtrage selon la distance géodésique parcourue est en outre proposée.


# 9. Export et sauvegarde

![](https://i.imgur.com/FVYk6Ji.png) Bouton permettant d'exporter une carte au format image (.PNG).

![](https://i.imgur.com/X6xDvlv.png) Bouton permettant d'exporter la carte au format .ZIP.

Pour ouvrir une carte sauvegardée, il faut charger le fichier .ZIP de sauvegarde - et ne pas l'avoir modifié entre temps.
![](https://i.imgur.com/Chfa3pP.png) 



arabesque glossaire (english/french)
===








## arabesque ToDoList and FAQ

:::info
**Find this document incomplete?** Leave a comment!
:::

###### tags: `Templates` `Documentation` `tutorial` `arabesque` `gflowiz`

