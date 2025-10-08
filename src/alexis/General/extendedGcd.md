## Explication du challenge

L'algorithme d'Euclide étendu permet de trouver des entiers `u` et `v` tels que :

```
a * u + b * v = gcd(a, b)
```

où `gcd(a, b)` est le plus grand commun diviseur de `a` et `b`. Cet algorithme est utile, par exemple, pour calculer l'inverse modulaire en cryptographie (RSA).

Voici le code Python correspondant :

```python
def egcd(a, b):
    x, y, u, v = 0, 1, 1, 0
    while a != 0:
        q, r = b // a, b % a
        m, n = x - u * q, y - v * q
        b, a, x, y, u, v = a, r, u, v, m, n
    gcd = b
    return gcd, x, y

print(egcd(26513, 32321))
```