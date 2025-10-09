## Explication du challenge

Pour trouver l'inverse de `g = 209` modulo le nombre premier `p = 991`, on cherche un entier `d` tel que :

```
(g × d) mod p = 1
```

En Python, on peut utiliser la fonction intégrée `pow` avec trois arguments pour calculer l'inverse modulaire efficacement :

```python
p = 991
g = 209

# Calcul de l'inverse modulaire de g modulo p
d = pow(g, -1, p)
print(d)  
```

### Résultat

L'inverse de `209` modulo `991` est `569`, ce qui vérifie bien que `(209 × 569) % 991 = 1`.