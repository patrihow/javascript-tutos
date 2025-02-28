# Requêtes HTTP : POST et GET

## Introduction

Lorsque vous créez une application web, vous devez souvent envoyer des données du client (navigateur) au serveur. Deux des méthodes HTTP les plus courantes sont **GET** et **POST**. Ces méthodes permettent d'interagir avec le serveur de différentes manières. 

---

## 1️⃣ La méthode GET

### 🔹 Qu'est-ce que GET ?

- Utilisée pour récupérer des données depuis le serveur.
- Les données sont envoyées dans l'URL sous forme de **paramètres de requête**.
- Visible dans la barre d'adresse du navigateur.
- Non sécurisée pour les données sensibles.

### 📌 Exemple : Formulaire en GET

```html
<form action="traitement.php" method="GET">
    <label for="nom">Nom :</label>
    <input type="text" id="nom" name="nom" required>
    
    <label for="email">Email :</label>
    <input type="email" id="email" name="email" required>
    
    <button type="submit">Envoyer</button>
</form>
```

### 📌 Traitement en PHP

```php
<?php
// Récupération des données envoyées via GET
$nom = htmlspecialchars($_GET['nom']);
$email = htmlspecialchars($_GET['email']);

// Affichage des données
echo "Nom : $nom";
echo "<br>Email : $email";
?>
```

### 🔹 Résultat après soumission

Si l'utilisateur remplit le formulaire avec **"Jean"** et **"jean@example.com"**, l'URL sera :
```text
traitement.php?nom=Jean&email=jean@example.com
```

🚨 **Attention** : Les données envoyées via GET sont visibles dans l'URL, ce qui n'est pas recommandé pour des informations sensibles comme des mots de passe.

---

## 2️⃣ La méthode POST

### 🔹 Qu'est-ce que POST ?

- Utilisée pour envoyer des **données au serveur** de manière sécurisée.
- Les données ne sont pas visibles dans l'URL.
- Permet d'envoyer des formulaires contenant des fichiers.

### 📌 Exemple : Formulaire en POST

```html
<form action="traitement.php" method="POST">
    <label for="nom">Nom :</label>
    <input type="text" id="nom" name="nom" required>
    
    <label for="email">Email :</label>
    <input type="email" id="email" name="email" required>
    
    <button type="submit">Envoyer</button>
</form>
```

### 📌 Traitement en PHP

```php
<?php
// Récupération des données envoyées via POST
$nom = htmlspecialchars($_POST['nom']);
$email = htmlspecialchars($_POST['email']);

// Affichage des données
echo "Nom : $nom";
echo "<br>Email : $email";
?>
```

### 🔹 Différence avec GET

Contrairement à GET, la méthode **POST** ne montre pas les données dans l'URL. Elles sont envoyées dans le **corps de la requête**, ce qui les rend plus sûres pour des informations sensibles.

---

## 🧐 Différences principales entre GET et POST

| Caractéristique | GET | POST |
|----------------|-----|------|
| Visibilité des données | Visible dans l'URL | Caché dans le corps de la requête |
| Sécurité | Faible (exposé dans l'URL) | Meilleure (non visible) |
| Taille des données | Limitée par l'URL | Aucune limite théorique |
| Utilisation recommandée | Récupération de données | Envoi de formulaires, authentification |

---

## Conclusion

- **GET** est utilisé pour récupérer des données et afficher du contenu sans modification sur le serveur.
- **POST** est utilisé pour envoyer des informations sensibles et modifier des ressources sur le serveur.

🎯 **Bonnes pratiques :**
✅ Utiliser GET pour les requêtes sans effet de modification (exemple : recherche d'articles).  
✅ Utiliser POST pour l'envoi de données sensibles (exemple : connexion, formulaire d'inscription).
