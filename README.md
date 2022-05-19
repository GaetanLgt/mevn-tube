### Crud
{
	--> joker => linux pour node.js /!\ en cas de soucis /!\
	---
	```
	sudo killall -9 node
	```
}


(https://fr.wikipedia.org/wiki/CRUD)
(https://networkop.co.uk/blog/2016/01/01/rest-for-neteng/)

## precs

installer node.js
installer mongodb && mongodb-compass

# Initialisation

===

```
npm init -y

npm i express nodemon
```
modif dans package.json

...
"scripts": {
```
    "start": "nodemon app.js"
```
  },
...

démarrer le serveur : 

---
```
npm run start
```

éteindre le serveur :

---
"ctrl+c"


## créer app.js

dans le ficher =>

```
const express = require('express')
const app = express()
const port = 3000

/** 2 insertion d'évenement en fonction de la route 
//middlewares
app.use('/posts', () => {
	console.log("l'appli du milieu qui te parle !")
} )
**/

//routes
app.get('/', (req, res) => {
	res.send('Salut les poulets !')
})

/* 1 création d'une route suplémentaire
app.get('/posts', (req, res) => {
	res.send('ici c'est le poullaier!')
})
*/

// Comment nous écoutons le serveur
app.listen(port, () => console.log(`Example on écoute le serveur sur le port : ${port}!`))

```

en fonction du crud on peut modifier l'appel à la page :

===

create

--- 
app.post('/posts/....

read

--- 
app.get('/posts/....

update

--- 
app.put('/posts/....

update

--- 
app.delete('/posts/....

## DataBase 

===

```
npm i mongoose 
```

** mlab.com ** => free dataBase
creer un compte et base de donnée

---
pour isoler la connexion a notre compte mongodb
```
npm i dotenv
```

isoler l'adresse de la bdd dans .env et dans le fichier app.js 

```
require ('dotenv/config')
```

pour se connecter inclure les lignes suivantes dans l'app.js avant le app.listen

```
mongoose.connect( process.env.DB_URL, { useNewUrlParser: true },
	() => console.log("Connecté à la base de données :) ")
)
```

## isoler les routes 

créer un dossier routes

---

Dans un ficher types.js inclure 

```
const express = require('express')
const router = express.Router()

router.get('/' , (req, res) => {
	// ici le traitement 
})

module.exports = router
```

inclure les routes dans le app.js

```
// Import des routes
const typesRoute = require('./routes/types')

app.use('/types', typesRoute)
```

pour une route spécifique dans la ressource ( à inclure dans le router )
la route sera /types/nomSpecifique

```
router.get('/nomSpecifique' , (req, res) => {
	// ici le traitement Specifique 
})
```

## Les traitements avec mongoose

créer un dossier models
&& un fichier Type.js
```
const mongoose = require('mongoose');

const TypeSchema = mongoose.Schema({
	title: {
		type: String,
		require: true
	},
	desc: String,
	date: {
		type: Date,
		default: Date.now
	}
});

module.exports = mongoose.model('Types', TypeSchema);
```
## Création 

importer le model dans la route correspondante

```
const Type = require('../models/Type')

router.post('/', (req, res) => { 
	
})
```
mais avant 

```
npm i body-parser
```

dans l'app.js rajouter la bibliothèque
```
const bodyParser = require('body-parser');
/** require('dotenv/config'); **/

app.use(bodyParser.json());
```









































fetch('http://localhost:3000/posts)
	.then(result => {
		return result.json();
	})
	.then(data => {
		
	})