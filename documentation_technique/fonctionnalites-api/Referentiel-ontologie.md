
tag : #documentation_technique 

# Objectifs


# [[Brainstorm]] pour Referentiel-ontologie


## Brainstorm du 20260603 
Dans `/excalidraw/20260603 avnu-refactore-ajustement-ref-1.excalidraw` on a fait un schema qui présente la direction que l'on veut implémenter.

![Brainstorm du 20260603](../../excalidraw/20260603-avnu-refactore-ajustement-ref.png)
```javascript
// WIP
const refTypeBloc: any = {  
    id: "type",  
    type: "string",  
    ontologyType: "rdf:Classe",  
};  
  
const refNameBloc: any = {  
    id: "name",  
    type: "string",  
    ontologyType: "xml:String",  
};  
  
const refShortDescriptionBloc: any = {  
    id: "name",  
    type: "string",  
    ontologyType: "rdf:String",  
};  
  
const refFullNameBloc: any = {  
    id: "fullname",  
    type: "string",  
     ,  
};  
  
const refStringBloc: any = {  
    id: "string",  
    type: "string",  
    ontologyType: "rdf:String",  
};

interface 
```


```javascript
// Mongo > Ref > Compatibilité > JSONLD  
// Mongo > Ref > Compatibilité > Référentiel  
const refPersonne2 = {  
    refFullNameBloc,  
};
  
const refPersonne = {  
    type: {  
        primitive: refTypeBloc,  
        cardinality: "1..1",  
    },  
    name: {  
        primitive: refNameBloc,  
        cardinality: "1..1",  
    },  
    shortDescription: {  
        primitive: refShortDescriptionBloc,  
        cardinality: "1..1",  
    },  
    disambiguatingDescription: {  
        primitive: refShortDescriptionBloc,  
        cardinality: "1..1",  
    },  
    fullname: {  
        primitive: refFullNameBloc,  
        cardinality: "1..1",  
    },  
    catchPhrase: {  
        primitive: refStringBloc,  
        cardinality: "0..1",  
    },  
};  

const referentielPersonne = {  
    compatibility: "avnu",  
    ref: refPersonne,  
};  

/**  
 * Entité personne * compatibilité : AVNU
 */
const personneVersAvnuBlueprint = (Document, ref) => {  
	const avnu = {  
	        "Person.fullname":
		        "avnu:fullname",  
	        "Person.spiritName": {  
	            property: 
		            refPersonne,  
	            transformer: 
		            concatenateTransormer([
			            "Person.firstName", 
			            " ", 
			            "Person.catchPhrase"
		        ]),  
	        },  
	        "Person.name":
		        "avnu:name",  
	    };  
	};
	return avnu;
}  

const concatenateTransormer = (params: Array<any>) => {  
    return "love is real";  
};
```

## Brainstorm du 2026-06-17
Dans `/excalidraw/20260603 avnu-refactore-ajustement-ref-1.excalidraw`.


## Brainstorm du 2026-06-26

https://www.w3.org/TR/rdf11-concepts/#section-Datatypes

```javascript
  
const name =  {  
    //PrimitiveName  
    type: "xsd:string", 
}  
  
const RefPerson = {  
	type: "rdfs:Class",
    properties: {  
        firstName: {  
            cardinality: "0..1",  
            rawType: "dans-le-document",// | virtuel | static | programmatic  
            constraint:"min:8",  
            compatibility: {  
                datascene: {}  
            },  
            type: {  
                slug: "string | createRefType('string')",  
                label: "Nom",  
                description: "Nom de l'entité",  
                litteral: {  
                    ...name  
                }  
            }  
        },  
    },  
    transformedProperties: {  
        fullName: {  
            cardinality: "0..1",  
            rawType: "virtuel",//programmatic  
            compatibility: {  
                datascene: {}  
            },  
            type: {  
                slug: "string | createRefType('string')",  
                label: "Nom",  
                description: "Nom de l'entité",  
                primitive: {  
                    ...name,  
                    url: createPrimitiveUrl("name"),  
                }  
            }  
        }  
    }  
}  
  
const RefEventFormat = {  
    type: {  
        type: "string",  
        rdfType: "rdf:string",  
        autreType: "string",  
    },//createRefType("string")  
    referentiel: {//documentation  
        route: createPrimitiveUrl("eventFormat"),  
        label: "Format de l'événement",  
        description: "L'événement se déroule de quelle façon : 'En ligne', 'Présentiel' etc.",  
        note: "Parmis EventFormatEnum",  
    }  
};  
  
const RefEvent = {  
    ref: {  
        eventFormat: {  
            cardinality: "0..1",  
            constraints: {  
                enum: EventFormatEnum,  
            },  
            compatibility: [],  
            ref: RefEventFormat,  
            type: {  
  
            },  
        }  
    },  
    referentiel: {  
        route: createPrimitiveUrl("eventFormat"),  
        label: "Format de l'événement",  
        description: "L'événement se déroule de quelle façon : 'En ligne', 'Présentiel' etc.",  
        note: "Parmis EventFormatEnum",  
    }  
};
```

### Post ajout de m-a
je pense surtout qu'il faut ajouter le vocubulaire + l'info qu'on a besoin au niveau structure (RDF).

```javascript
const name =  {  
    //PrimitiveName  
    type: "string",  
    rdf: "rdf:*string",  
    url: createPrimitiveUrl("name")  
}  
```

# [[Conception]] pour Referentiel-ontologie


# Structure

```javascript

```

## Exemple

```javascript

```


# Todo



# Planifié
