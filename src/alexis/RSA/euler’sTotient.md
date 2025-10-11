## Explication du challenge

### Calcul de ϕ(N)

L'indicatrice d'Euler pour deux nombres premiers est :

\[
\varphi(N) = (p - 1) \times (q - 1)
\]

### Exemple en Python

```python
p = 857504083339712752489993810777
q = 1029224947942998075080348647219

phi = (p - 1) * (q - 1)

print(phi)
```

Ce code calcule la valeur de ϕ(N) en utilisant les deux facteurs premiers donnés.