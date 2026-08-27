# Versionnage Sémantique
Nous allons continuer dans le système de version sémantique. Il est largement utiliser dans plusieuers type de logiciels et surtout dans les API.
## Il consiste à ces 3 segement :

`Majeure`. `Mineure`.`Ajustement`

- **Majeure** : Augmenté lorsque vous faites des changements incompatibles dans l'API.
- **Mineure** : Augmenté lorsque vous ajoutez des fonctionnalités de manière rétrocompatible.
- **Ajustement** : Augmenté lorsque que des corrections de bugs de manière rétrocompatible sont faite.

### Par exemple
- **1.0.0** : Première version en ligne.
- **1.1.0** : Ajout d'une nouvelle fonctionnalité.
- **1.1.1** : Correction de bugs dans la fonctionnalité ajoutée.
- **2.0.0** : Changements majeurs qui cassent la compatibilité avec la version 1.x.x.

# API 
L'api utilisera ce système de version

# APP 
L'app aussi utilisera cette version.

# Méthodologie
Pour construire les notes de version automatiquement, on utilise les pull request.

Chaque fonctionnalité / stories devra avoir sa branche. 

Et être merger dans Github pour être en mesure de commenter, d'être révisé et d'être inclus dans les notes de versions.

## Nomenclature des branches
`
Avec du kebab
`Base de la branche`-`version de la branche de base`-`fonctionnalité`

**Important** : L'API et l'APP doivent partager le même nom
- Api : `dev-sameAs`
- App: `dev-sameAs`

Exemple avec une branche de base avec une version : 
- Api : `dev-1-0-4-sameAs`
- App: `dev-1-0-4-sameAs`





