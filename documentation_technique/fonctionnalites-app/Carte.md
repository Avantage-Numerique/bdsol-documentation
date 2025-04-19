tag : #documentation_technique 
# Objectifs
Afficher une carte

# [[Brainstorm]] pour Carte


# [[Conception]] pour Carte

## Mise en contexte de l'intégration de la carte
Initialement, nous avions implémenté la carte directement avec Leaflet, c'est-à-dire en javascript. Nous avons décider d'intégrer par la suite le package React-Leaflet, pour résoudre quelques problèmes

## Description de l'utilisation de React-Leaflet
Après l'ajout des packages et la résolution de conflits de package, l'ajout de React-Leaflet devait se faire seulement client-side. C'est pour cela que nous déclarons les composantes de cette façon :
```javascript
import dynamic from "next/dynamic";
const MapContainer = dynamic(
	() => import('react-leaflet').then((mod) => mod.MapContainer),
	{ ssr: false }
);
const TileLayer = dynamic(
	() => import('react-leaflet').then((mod) => mod.TileLayer),
	{ ssr: false }
);
const Marker = dynamic(
	() => import('react-leaflet').then((mod) => mod.Marker),
	{ ssr: false }
);
const Popup = dynamic(
	() => import('react-leaflet').then((mod) => mod.Popup),
	{ ssr: false }
);
```

Ensuite, nous avons créer un wrapper pour s'assurer que react n'allait pas remount pour rien. C'est pour cela qu'il existe "MapDynamicLoaded" dans le wrapper "MapWrapper.js" comme suit :
```javascript
const MapDynamicLoaded = dynamic(() => import('@/src/map/Map'), { ssr: false });
const MapWrapper = (props) => {
  return (
    <MapDynamicLoaded
      latLng={props?.latLng}
      setLatLng={props?.setLatLng}
      locationList={props?.locationList}
      coordinatePopUp={props?.coordinatePopUp}
      height={props?.height}
      width={props?.width}
      centerAt={props?.centerAt}
    />
  );
};
export default React.memo(MapWrapper);
```
Finalement, nous pouvons utiliser la carte comme une composante en appellant "MapWrapper" et en lui passant les props comme une composante ordinaire.

## Props et features
À noté que les coordonnées à transmettre à React-Leaflet sont dans le format `[latitude, longitude]`. Par exemple : `[48.236,-79.015]`.

### Notes importantes pour les props
Comme la carte est render client-side et/ou est liée à des formulaires, la carte a la fâcheuse tendance à se remount et donc se reset à chaque input change, input onBlur ou onClick sur la carte. Pour éviter cela, il est primordial de vérifier que chaque props qu'on passe ne se modifie pas.
Par exemple, `setLatLng` modifie un useState qui modifie le centerAt.

Autre exemple, il arrive que parce que les variables passées en props soient elles-mêmes définie dans la composante parente qui elle remount, la variables se réinitialise. Même si elle possède la même valeur, React considère qu'elle est différente car elle a été réindexé dans la mémoire. Pour éviter cela, memoize la valeur :
```javascript
const centerAt = useMemo(() => {
        return [model.location.latitude, model.location.longitude];
    }, []);
```


Voici les props de la carte :
- **className** : transfert à la carte les propriétés css de bootstrap.
- **locationList** : Permet d'afficher des markeurs aux coordonnées. `locationList` doit prendre la forme d'un array d'objet, chacun contenant un objet `location` possèdant une latitude et longitude. Exemple : `locationList = [ { location : { latitude :  x, longitude : y}}, {...}]`.
- **height** : Hauteur de la carte en pixel, si non déclaré, la carte prend 100% de l'espace du contenant.
- **width** : Largeur de la carte en pixel, si non déclaré, la carte prend 100% de l'espace du contenant.
- **centerAt** : Centre la carte sur la coordonnées, sinon la carte possède une valeur par défaut.
- **coordinatePopUp** : Valeur booléenne permettant d'activer le onClick pour afficher la latitude et longitude sur la carte à l'endroit du click.
- **coordinateMsg** : Permet de modifier le message se trouvant au-dessus de la latitude et longitude dans le popup de "coordinatePopUp".
- **setLatLng** : Un setter de state permettant à la carte de transmettre la coordonnée du onClick pour préremplir un champ avec celle-ci.

## Cas d'utilisation
 Page /contribuer/lieux
	- [ ] Page PlaceSingleView
	- [ ] Page PlaceSingleEdit
	- [ ] Page /consulter? (pas implémenter)
### Page /contribuer/lieux (index.js)(Create lieux)
Objectifs :
- Avoir une carte
- Permettre l'utilisateur de choisir la position sur la carte
- Auto-remplir les champs le mieux possible avec la position sélectionnée
- Utiliser une API gratuite

Ces objectifs ont été remplis.
- La carte s'affiche
- Le click affiche la coordonnée et prérempli un champ temporaire
- L'utilisateur peut cliquer sur le bouton de recherche permettant d'effectuer la recherche pour l'auto-remplissage des champs. Un popup montre les données trouvée par l'API et l'auto-remplissage s'effectue si l'utilisateur le désir.
- L'API utilisée est Nomatim qui est basé sur OpenStreetMap. Cependant, cet API possède des conditions d'utilisation pour qu'elle soit gratuite à faire attention pour ne pas se faire banir de l'utilisation de celle-ci.
### Page /contribuer/lieux/slug (PlaceSingleEdit)
Objectifs :
- Ajouter une carte
- La carte doit être clickable et permettre la modification de la coordonné du lieu

La carte a été ajoutée avec le onClick qui modifie le formulaire.

Cependant, cette page est en V1 et devrait être modifiée. En ce moment, le click de la carte modifie la champs input sans demander à l'utilisateur s'il est sûr de cette modification, ce qui pourrait engendrer une mise à jour de la coordonnée non voulu par un clic sur la carte suivi d'une sauvegarde.

### Page /lieux/slug (PlaceSingleView)
Objectifs :
- Ajouter une carte
- Montrer, à l'aide d'un marqueur, l'endroit du lieu de la page Single

Ces objectifs ont été remplis.
- La carte a été ajoutée
- La carte se centre sur le lieu
- La carte affiche un marqueur avec le nom du lieu lorsqu'on clique dessus.
### Page /consulter/lieux (ou carte interactive dans une route dédier)
Non implémenter.
Objectifs : Avoir une carte interactive regroupant visuellement les lieux de la base de données. 


# Structure

## sources
- https://openlayers.org/ (pour les couches d'OSM)
- https://wiki.openstreetmap.org/wiki/OpenLayers
- https://leafletjs.com/
- https://github.com/PaulLeCam/react-leaflet

## Hypothèse 1
- Utiliser https://react-leaflet.js.org/docs/start-introduction/ pour avoir leaflet comme gestionnaire de map pour l'app.
	- https://github.com/PaulLeCam/react-leaflet

```javascript

```

## Exemple

```javascript

```


# Todo


# Planifié
