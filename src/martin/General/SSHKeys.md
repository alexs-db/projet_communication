# Challenge : Clés Publiques SSH et Modulus

## Explication du Défi

Ce challenge porte sur le protocole **SSH (Secure Shell)**, un standard de chiffrement essentiel pour sécuriser les communications et l'administration à distance sur Internet.

SSH utilise la **cryptographie asymétrique (clés publique/privée)** pour l'authentification et l'établissement d'une connexion sécurisée :

1.  **Serveur** stocke la **clé publique** de l'utilisateur.
2.  **Utilisateur** (Bruce) stocke la **clé privée** sur son appareil.
3.  Lors de la connexion, le serveur défie le client avec un message chiffré par la clé publique ; seul le détenteur de la clé privée correspondante peut déchiffrer ce message et prouver son identité.

### Le Format des Clés

* **Clé Privée :** Stockée en format **PEM** (ex. `-----BEGIN RSA PRIVATE KEY-----`).
* **Clé Publique (Objet du Challenge) :** Stockée dans un format spécifique, plus simple, souvent dans le fichier `authorized_keys` du serveur. Ce format commence généralement par `ssh-rsa` ou similaire.

---

## La Tâche à Accomplir

La clé publique SSH est une structure qui contient plusieurs valeurs mathématiques, dont le **modulus ($n$)** utilisé dans les algorithmes de chiffrement (comme RSA).

## Résolution

Conversion au format PEM : Nous convertissons la clé publique SSH au format PEM et la sauvegardons dans un fichier nommé "bruce_rsa.pem".
Extraction du Modulus : Enfin, nous récupérons le modulus (n) à l'aide du code Python suivant :

```python
from Crypto.PublicKey import RSA

f = open('bruce_rsa.pem', 'r')
pubkey = RSA.import_key(f.read())

print(pubkey.n)
```


