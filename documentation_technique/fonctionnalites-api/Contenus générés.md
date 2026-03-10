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
- `_sources` nom assez clair ?
	- `propertySources`
	- `propertyMeta`
	- 
- Est-ce qu'on met `_sources` dans `meta` dans le fond ?
	- Si oui, est-ce que c'est trop deep `meta.propertySource`
	- Si non, 
# [[Conception]] pour Contenus générés


# Structure

```json
{
  "_id": {
    "$oid": "67d331b6bce8cba00becb22a"
  },
  "firstName": "Patrick",
  "lastName": "Watson",
  "__v": 0,
  "badges": [],
  "createdAt": {
    "$date": "2025-03-13T19:27:50.043Z"
  },
  "description": "<p>Chanteur</p>",
  "domains": [
    {
      "domain": {
        "$oid": "67d331b4bce8cba00becb1d8"
      }
    }
  ],
  "meta": {
    "state": "pending",
    "lastModifiedBy": {
      "$oid": "67d331b5bce8cba00becb228"
    }
  },
  "_sources" {
	"shortDescription": {
		"generated": "true",
		"date": "2026-03-10 00:00:00 UTC-4",
		"source": "avnu"
	}
  },
  "nickname": "PoW",
  "occupations": [
    {
      "groupName": "3333333",
      "skills": [
        {
          "$oid": "67d331b6bce8cba00becb252"
        },
        {
          "$oid": "67d331b4bce8cba00becb1cb"
        }
      ],
      "subMeta": {
        "order": 2
      }
    },
    {
      "groupName": "444444",
      "skills": [
        {
          "$oid": "68e565aa0a024c0cd38b2536"
        }
      ],
      "subMeta": {
        "order": 3
      }
    },
    {
      "groupName": "111111",
      "skills": [
        {
          "$oid": "68ef9fe5110556c9806237fc"
        }
      ],
      "subMeta": {
        "order": 0
      }
    },
    {
      "groupName": "2222222",
      "skills": [
        {
          "$oid": "68a34026b65efc11cc667c0d"
        }
      ],
      "subMeta": {
        "order": 1
      }
    }
  ],
  "slug": "patrick-watson",
  "updatedAt": {
    "$date": "2025-12-10T21:29:55.958Z"
  },
  "url": [
    {
      "label": "asdasdasd",
      "url": "asdasdasd",
      "subMeta": {
        "order": 0
      }
    },
    {
      "label": "asdasd",
      "url": "asdasdasd",
      "subMeta": {
        "order": 1
      }
    }
  ],
  "catchphrase": "",
  "contactPoint": {
    "email": {
      "address": ""
    },
    "tel": {
      "num": "",
      "ext": ""
    },
    "website": {
      "url": ""
    }
  },
  "region": ""
}
```

## Exemple

```javascript

```


# Todo


# Planifié
