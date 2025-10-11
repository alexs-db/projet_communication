# Challenge : Calcul de la Clé Privée RSA

## Explication du Défi

Ce challenge est une étape fondamentale dans la compréhension du chiffrement **RSA** : le calcul de la **clé privée $d$**.

### Le Rôle de la Clé Privée ($d$)

La clé privée $d$ est la "trappe secrète" qui permet de déchiffrer rapidement un message. Sa sécurité repose sur le fait qu'elle est extrêmement difficile à calculer si l'on ne connaît pas les facteurs premiers du modulus $N$ (le défi de la factorisation).

### Le Calcul Mathématique

En RSA, l'exposant privé $d$ est défini comme l'**inverse multiplicatif modulaire** de l'exposant public $e$, modulo $\phi(N)$ :

$$d \equiv e^{-1} \pmod{\phi(N)}$$

où $\phi(N)$ est l'**indicatrice d'Euler** de $N$.

---

## La Tâche à Accomplir

En utilisant les deux nombres premiers ($p$ et $q$) qui composent le modulus $N$, vous devez :

1.  **Calculer $\phi(N)$** (sachant que $N = p \cdot q$ et $p, q$ sont premiers).
2.  **Trouver l'inverse multiplicatif** de l'exposant public $e=65537$ modulo $\phi(N)$.

Vous devez trouver l'entier **$d$** tel que :

$$d \cdot e \equiv 1 \pmod{\phi(N)}$$

Le *flag* à soumettre est la valeur de la clé privée **$d$**.

## Résolution du Défi

Ce script calcule l'exposant privé d (la clé privée) d'un système RSA, à partir des deux nombres premiers p et q et de l'exposant public e.

```Python
p = 857504083339712752489993810777
q = 1029224947942998075080348647219
e = 65537
phi = (p-1)*(q-1)
d = pow(e, -1, phi)
print(d)
```
