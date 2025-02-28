# Introduction aux Promesses et à `fetch()`

## Qu'est-ce qu'une promesse en JavaScript ?

En JavaScript, une **promesse** est un objet qui représente une opération asynchrone en attente de son résultat final. Elle peut être dans l’un des trois états suivants :

1. **Pending (en attente)** : l’opération n’est pas encore terminée.
2. **Fulfilled (réussie)** : l’opération a réussi et retourne une valeur.
3. **Rejected (échouée)** : l’opération a échoué et retourne une erreur.

### Syntaxe de base d’une promesse
```javascript
const maPromesse = new Promise((resolve, reject) => {
    let condition = true; // Change en false pour tester le reject
    if (condition) {
        resolve("Succès");
    } else {
        reject("Échec");
    }
});
```

### Consommer une promesse avec `.then()` et `.catch()`
```javascript
maPromesse
    .then(resultat => console.log("Réussi :", resultat))
    .catch(erreur => console.error("Erreur :", erreur));
```

## `fetch()` : récupérer des données depuis un serveur

### Syntaxe de base
La fonction `fetch()` permet de faire des requêtes HTTP et retourne une promesse.

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
    .then(response => response.json()) // Convertit la réponse en JSON
    .then(data => console.log("Données reçues :", data))
    .catch(error => console.error("Erreur de requête :", error));
```

### Explication étape par étape
1. `fetch(url)` effectue une requête vers l’URL donnée.
2. `.then(response => response.json())` transforme la réponse en JSON.
3. `.then(data => console.log(data))` affiche les données reçues.
4. `.catch(error => console.error(error))` capture les erreurs.

---

# Utilisation de `fetch()` avec `POST` et manipulation du DOM

## Envoi de données avec `POST`
Pour envoyer des données à un serveur, on utilise `fetch()` avec la méthode `POST`.

```javascript
fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        title: "Mon titre",
        body: "Mon contenu",
        userId: 1
    })
})
.then(response => response.json())
.then(data => console.log("Réponse du serveur :", data))
.catch(error => console.error("Erreur :", error));
```

### Explication de la structure
1. **Méthode** : `POST` est utilisé pour envoyer des données.
2. **Headers** : Définissent le type de contenu (`application/json`).
3. **Body** : Convertit l’objet JS en JSON pour l’envoi.

### Manipulation du DOM après un `fetch()`

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
    .then(response => response.json())
    .then(data => {
        let div = document.createElement("div");
        div.innerHTML = `<h2>${data.title}</h2><p>${data.body}</p>`;
        document.body.appendChild(div);
    })
    .catch(error => console.error("Erreur :", error));
```

### Étapes
1. Récupération des données avec `fetch()`.
2. Création d’un élément `<div>` dynamiquement.
3. Ajout du contenu HTML avec les données reçues.
4. Ajout de l’élément au `body`.

---

# Utilisation avancée avec `async/await`

## Réécriture de `fetch()` avec `async/await`

```javascript
async function obtenirPost() {
    try {
        let response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
        let data = await response.json();
        console.log("Données reçues :", data);
    } catch (error) {
        console.error("Erreur :", error);
    }
}

obtenirPost();
```

### Pourquoi utiliser `async/await` ?
- **Code plus lisible** : On évite la chaîne de `.then()`.
- **Gestion d’erreurs plus propre** : On utilise `try/catch`.
- **Plus facile à déboguer**.

---

# Organisation du code et bonnes pratiques

## Définir la signature des fonctions

Une fonction bien structurée doit suivre ce modèle :

```javascript
async function envoyerDonnees(url, donnees) {
    try {
        let response = await fetch(url, {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(donnees)
        });
        return await response.json();
    } catch (error) {
        console.error("Erreur lors de l'envoi :", error);
        throw error;
    }
}
```

### Bonnes pratiques
1. **Nom explicite** : `envoyerDonnees()` décrit bien son rôle.
2. **Utilisation de `async/await`** : Facilite la lecture.
3. **Utilisation de `try/catch`** : Capture les erreurs.
4. **Retourner `response.json()`** : Permet d'utiliser la fonction ailleurs.
5. **Rendre le code réutilisable** en passant `url` et `donnees` en paramètres.

