tag : #documentation_technique 

# Objectifs
Gérer les contenus généré par l'API dans la base de données et dans les retours de l'API.

Conserver la valeur saisie par l'utilisateur pour `shortDescription` et la version générée de `shortDescription` à partir de la propriété description 
1. Ajoutée par un utilisateur 
2. Générée par un algorithme de troncature 

Dans le formulaire de mise à jour, on doit afficher la valeur générée, mais on ne veut pas que le champ `shortDescription` soit sauvegardé. 

La valeur de `shortDescription` n'est stockée que si l'utilisateur l'a définie. 
Des fonctionnalités semblable à `shortDescription` pourrait être utilisée dans le futur. 
D'autres propriétés combinant une valeur générative et une valeur utilisateur sont envisageables pour un même champ. 

Peut être regroupé avec d'autres propriétés qui sont surérogatoire à la finalité principale de la donnée, mais qui restent pertinentes. 

Restez dans les formats pertinents pour mongodb.
Garder le DX nice et facile à maintenir.
# [[Brainstorm]] pour Contenus générés

On a parlé longtemps cette feature pour `shortDescription`.

La deuxième propriété qu'on veut avoir absolument disponible, même si le user n'a pas entré de valeur.
## Donc une propriété à trois valeur possible :
1. par le user
2. généré par l'API
3. vide
## En fait c'est plus deux champs que ça prend :
`shortDescription` user value
`shortDescriptionGenerated` valeur tronqué de `description`.
 ∴ `shortDescription` est vide, on affiche/utilise la version généré.

## Dans la BD

Si l'utilisateur a ajouter une description courte : 

```javascript
{
	description: "Very long text about that entity.",
	shortDescription : "user have writen something",
	_sources: {//not mandatory
		description: {
			generated: false//toujours false par défault si pas de valeur ici.
		},
		shortDescription : {
			generated: false,
			date: "2026-03-10 00:00:00 UTC-4",
			source: "avnu"
			...
		},
		...
	}
}
```

Si l'utilisateur n'a pas ajouter une description courte :

```javascript
{
	description: "Very long text about that entity.",
	shortDescription : "",
	_sources: {//not mandatory
		description: {
			generated: false//toujours false par défault si pas de valeur ici.
		},
		shortDescription : {
			generated: false,
			date: "2026-03-10 00:00:00 UTC-4",
			source: "avnu"
			...
		},
		...
	}
}
```
## Envoyer via le DTO
```javascript
{
	description: "Very long text about that entity.",
	shortDescription : "Generated content",
	_sources: {
		name: {
			...
		},
		shortDescription : {
			generated: true,
			date: "2026-03-10 00:00:00 UTC-4",
			source: "avnu"
			...
		},
		...
	}
}
```


## Sous discussion :
- `_sources` nom assez clair ? : trop compliqué pour l'instant on ajoutera ça 
	- `propertySources`
	- `propertyMeta`
	- 
- Est-ce qu'on met `_sources` dans `meta` dans le fond ?
	- Si oui, est-ce que c'est trop deep `meta._source.shortDescription.property`
	- Si non, est-ce que le fait d'avoir `_source` et `meta` sans le `_` , donc il faut migrer vers le `_` pour `meta` ou mettre `sources` sans le `_`.
- Est-ce qu'on met juste le `generated` dans le DTO ?
# [[Conception]] pour Contenus générés

Après la discussion du 2026-03-11

On garde la données brutes dans le document.
On ajoute un objet `generated` qui regroupe les contenus générés par l'API.

On ajoute la nomenclature avec le `_` donc l'objet devient : `_generated`

# Structure

```json
{
	description: "Very long text about that entity.",
	shortDescription : "User content",
	_generated: {
		shortDescription : "generated value"
		...
	}
}
```

## Exemple

```javascript

```


# Todo


# Planifié
