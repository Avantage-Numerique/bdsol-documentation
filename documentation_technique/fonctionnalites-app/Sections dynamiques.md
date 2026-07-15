tag : #documentation_technique 

# Objectifs
Permettre des modifications du contenu en dehors des version de l'application.

# [[Brainstorm]] pour Sections dynamiques

![[section-dynamique-app-0-1.png]]
# [[Conception]] pour Sections dynamiques

WIP version 0.0.1

# Structure

## Une section
| Propriété  | description                            | Note                                                                                 |
| :--------: | -------------------------------------- | ------------------------------------------------------------------------------------ |
|     id     | identifiant unique de la section       | intelligible ou pas, déterminé lors de la sauvegarde de l'objet/json                 |
|    type    | Enum de type de sections supportées    | Doit être restraint à des valeurs prédéterminé ENUM, selon ce qu'on a d'implémenter. |
|  content   | Propriétés nécessaires pour la section | Chaque type sections a ses besoins et fonctionnalité reliés au content.              |
|            |                                        |                                                                                      |
|   order    | nombre naturel N                       | Pour réordonner les sections lorsqu,il en a plusieurs.                               |


```typescript
{
    id: "123safdosd",
    type: "content_basic",
    content: {
        title: "1234 arachides",
        content: "<p>asdasdasd</p>",
        cta: {
            label: "click ici man",
            url: "https://avnu.ca/asd",
        },
        image: {
            url: "",
            alt: ""
        }
    },
    order: N
}
```

## Une page de l'application

```typescript
{
	homePage: {
	    afterData: {
	        sections: [
	            {id:"asdasdasd", ...}
	        ]
	    }
	}
}
```

## Exemple

```json
{
	"homePage": {
	    "sections": {
	        "afterData": [
	            {
				    "id": "123safdosd",
				    "type": "content_basic",
				    "content": {
				        "title": "1234 arachides",
				        "content": "<p>asdasdasd</p>",
				        "cta": {
				            "label": "click ici man",
				            "url": "https://avnu.ca/asd",
				        },
				        "image": {
				            "url": "",
				            "alt": ""
				        }
				    },
				    "order": N
				}
	        ],
	        "footer": [
	        ]
	    }
	}
}
```


# Todo


# Planifié
