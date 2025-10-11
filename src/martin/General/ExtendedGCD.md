# Challenge : Algorithme d'Euclide Étendu

## Explication du Défi

Ce challenge porte sur l'**Algorithme d'Euclide Étendu**, une méthode fondamentale en cryptographie, notamment pour le calcul d'inverses modulaires (utilisé dans RSA).

L'objectif de cet algorithme est de trouver deux entiers, $u$ et $v$, qui vérifient l'équation de Bezout pour deux nombres donnés ($a$ et $b$) :

$$a \cdot u + b \cdot v = \text{gcd}(a, b)$$

où $\text{gcd}(a, b)$ est le plus grand commun diviseur de $a$ et $b$.

---

## La Tâche à Accomplir

En utilisant les deux nombres premiers fournis :
* $p = 26513$
* $q = 32321$

Vous devez trouver les entiers $u$ et $v$ tels que :
$$p \cdot u + q \cdot v = \text{gcd}(p, q)$$

### Question Clé

Étant donné que $p$ et $q$ sont des nombres **premiers distincts**, quelle valeur attendez-vous pour $\text{gcd}(p, q)$ ?

### Soumission du Flag

Une fois que vous avez trouvé les deux entiers $u$ et $v$, le *flag* est l'**entier le plus petit** (le plus bas) entre $u$ et $v$.

## Résolution du Défi

### La Fonction `egcd(a, b)`

La fonction prend deux entiers positifs, $a$ et $b$, et renvoie le triplet `(gcd, x, y)` tel que :
$$a \cdot x + b \cdot y = \text{gcd}(a, b)$$

```python
def egcd(a, b):
    x,y, u,v = 0,1, 1,0
    while a != 0:
        q, r = b//a, b%a
        m, n = x-u*q, y-v*q
        b,a, x,y, u,v = a,r, u,v, m,n
    gcd = b
    return gcd, x, y

print egcd(26513,32321)
```