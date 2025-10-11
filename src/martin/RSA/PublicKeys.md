# Challenge : Chiffrement RSA de Base

## Explication du Défi

Ce challenge est une introduction au **chiffrement RSA** (Rivest–Shamir–Adleman). Il vous demande d'effectuer l'opération mathématique fondamentale de chiffrement.

### Le Principe RSA

Le chiffrement RSA utilise une **clé publique** composée d'un **modulus** ($N$) et d'un **exposant** ($e$). Le modulus $N$ est le produit de deux grands nombres premiers ($p$ et $q$).

L'opération de chiffrement d'un message $m$ pour obtenir le chiffré $c$ est une simple exponentiation modulaire :

$$c = m^e \pmod{N}$$

---

## La Tâche à Accomplir

Vous devez chiffrer le nombre $m = 12$ en utilisant les paramètres fournis :

1.  **Calculer le Modulus $N$** :
    $$N = p \cdot q = 17 \cdot 23$$
2.  **Appliquer la Formule de Chiffrement** :
    $$c = 12^{65537} \pmod{N}$$

Le *flag* à soumettre est le **nombre obtenu comme chiffré $c$**.

## Résolution du Défi

Le but de ce script est de chiffrer un message simple (le nombre 12) en utilisant les paramètres d'une clé publique RSA (N,e).

```Python
e = 65537
p = 17
q = 23
N = p * q
plaintext = 12
ciphertext = pow(plaintext, e, N)
print(ciphertext)
```