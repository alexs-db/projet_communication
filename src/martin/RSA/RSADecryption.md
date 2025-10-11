# Challenge : Déchiffrement RSA

## Explication du Défi

Ce challenge est une application directe du déchiffrement dans le système de cryptographie **RSA** (Rivest–Shamir–Adleman).

### Le Principe

Le chiffrement RSA fonctionne avec une paire de clés : une clé publique (connue de tous) et une clé privée (gardée secrète).

* **Chiffrement :** Le message secret ($m$) est chiffré par l'émetteur en utilisant la clé publique du destinataire (composée de **$N$** et **$e$**) pour obtenir le chiffré $c$ :
    $$c = m^e \pmod{N}$$
* **Déchiffrement :** Seul le destinataire, qui détient la **clé privée** correspondante (composée de **$d$** et $N$), peut déchiffrer $c$ pour retrouver le message original $m$ :
    $$m = c^d \pmod{N}$$

---

## La Tâche à Accomplir

Vous recevez ici le **chiffré $c$** et les paramètres publics **$N$** et **$e$**.

1.  **Récupérer la Clé Privée ($d$) :** Utiliser l'exposant privé ($d$) que vous avez calculé lors du challenge précédent (où vous deviez trouver l'inverse modulaire de $e$ par rapport à $\phi(N)$).
2.  **Déchiffrer le Message :** Appliquer la formule de déchiffrement RSA :

$$\text{Secret} = c^d \pmod{N}$$

Le *flag* à soumettre est le **nombre secret déchiffré**.

## Résolution du Défi

Ce script réalise l'opération fondamentale de déchiffrement RSA pour retrouver un message secret (m) à partir d'un message chiffré (c) et de la clé privée.

```Python
N = 882564595536224140639625987659416029426239230804614613279163
c = 77578995801157823671636298847186723593814843845525223303932

d = 121832886702415731577073962957377780195510499965398469843281

plain = pow( c, d, N )

print(plain)
```