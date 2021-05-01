# Lust.js (Bêta)

## Un client javascript pour le site <https://net-lust.com/>

<hr/>

`npm i lust.js`

```js
const Lust = require('lust.js');

var app = new Lust("xxx@xxx.xx","xxxxxxxxx")

app.login()

// [...]
```

# docs

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [Lust](#lust)
    -   [login](#login)
        -   [Parameters](#parameters)
        -   [Examples](#examples)
    -   [getProfil](#getprofil)
        -   [Parameters](#parameters-1)
        -   [Examples](#examples-1)
    -   [getHome](#gethome)
        -   [Examples](#examples-2)
    -   [onMessage](#onmessage)
        -   [Parameters](#parameters-2)
        -   [Examples](#examples-3)
    -   [addPost](#addpost)
        -   [Parameters](#parameters-3)
        -   [Examples](#examples-4)
    -   [addComment](#addcomment)
        -   [Parameters](#parameters-4)
        -   [Examples](#examples-5)
    -   [getComments](#getcomments)
        -   [Parameters](#parameters-5)
        -   [Examples](#examples-6)
    -   [search](#search)
        -   [Parameters](#parameters-6)
        -   [Examples](#examples-7)

## Lust

### login

Connexion au compte Lust

#### Parameters

-   `email` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Le mail du compte
-   `password` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Le mot de passe du compte

#### Examples

```javascript
var app = new Lust("xxx@xxxx.xx","xxx")
app.login().then(()=>{
 app.getHome().then(posts=>console.log(posts.postsFollow))
})
```

Returns **[promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)** 

### getProfil

Permet de récupérer les informations d'un profil
(pas besoin d'être connecté)

#### Parameters

-   `username` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**  (optional, default `"nom d'utilisateur si connecté"`)

#### Examples

```javascript
app.getProfil("andronedev").then(console.log)
// return :
  {
    username: 'andronedev',
    imgProfil: 'https://net-lust.com/assets/users/profils/1115514632.gif',
    followersCount: '1',
    memberSince: '20 Feb 2021',
    posts: [
      {
        id: '341',
        username: 'andronedev',
        profilLink: 'https://net-lust.com/profil?pseudo=andronedev',
        date: 'il y a 11 jours',
        message: 'Salut',
        img: null
      },
     [...]
    ]
  }
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;ProfilType>** 

### getHome

Permet de récupérer des informations à partir de la page home.

#### Examples

```javascript
app.getHome().then(posts=>console.log(posts))
// return :
 {
   postsFollow: [
     {
       id: '444',
       username: 'Zartov',
       profilLink: 'https://net-lust.com/profil?pseudo=Zartov',
       date: 'il y a 4 jours',
       message: 'pas mal #FlightSimulator 😅',
       img: 'https://i.imgur.com/tMT4Blv.jpg'
     },
    [...]
 {
```

### onMessage

Permet de faire une action quand un nouveau message est reçu

#### Parameters

-   `callback`  

#### Examples

```javascript
app.onMessage(msg => {
console.log("Nouveau message :\n", msg.username, " : ", msg.message)
})
```

Returns **this** 

### addPost

Permet d'Ajouter un post

#### Parameters

-   `message` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 
-   `img`   (optional, default `""`)
-   `image` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** lien de l'image (ex : <https://i.imgur.com/zabyPE5.jpg>)

#### Examples

```javascript
app.addPost("salut à tous", "https://i.imgur.com/zabyPE5.jpg").then((p) => {
console.log("id du poste : ", p.id);
})
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;{id: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String), url: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)}>** 

### addComment

Permet d'Ajouter un commentaire

#### Parameters

-   `id` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** l'id du post
-   `message` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 

#### Examples

```javascript
app.addComment("Commentaire")
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;{void}>** 

### getComments

Permet de récupérer les commentaires d'un post

#### Parameters

-   `id` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** l'id du poste

#### Examples

```javascript
app.getComments("444").then(console.log)
// return :
[
 {
   username: 'andronedev',
   profilLink: 'https://net-lust.com/profil?pseudo=Zartov',
   date: 'il y a 21 jours',
   message: 'Salut !'
 },
[...]
]
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;CommentsType>** 

### search

Permet de récupérer le resultat d'une recherche

#### Parameters

-   `query` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** champ de recherche

#### Examples

```javascript
app.search("zar").then(console.log)
// return :
  [
    { type: 'hashtag', hashtag: '#ZartovElypse' },
    {
      type: 'account',
      username: 'Zartov',
      profilLink: 'profil?pseudo=Zartov',
      imgProfil: 'assets/users/profils/1115514560.jpg'
    },
   [...]
  ]
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;searchType>** 
