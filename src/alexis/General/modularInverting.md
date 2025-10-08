## Explication du challenge

**Trouver l'inverse de 3 modulo 13 :**

On cherche \( d \) tel que \( 3 \cdot d \equiv 1 \mod 13 \).

Grâce au petit théorème de Fermat, si \( a \) n'est pas divisible par \( p \), alors :
\[
a^{p-1} \equiv 1 \mod p
\]
Ce qui implique :
\[
a^{p-2} \equiv a^{-1} \mod p
\]
Donc, l'inverse de 3 modulo 13 est :
\[
3^{13-2} \mod 13 = 3^{11} \mod 13 = 9
\]

```python
>>> pow(3, 13-2, 13)
9
```

L'inverse de 3 modulo 13 est donc 9.