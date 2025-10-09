## Explication du code

On considère le système suivant :
- \( N = p \cdot q \)
- \( c_1 = (2p + 3q)^{e_1} \mod N \)
- \( c_2 = (5p + 7q)^{e_2} \mod N \)

L'objectif est de retrouver les valeurs de \( p \) et \( q \) connaissant \( N, c_1, c_2, e_1, e_2 \).

### Étapes de résolution

1. **Calcul intermédiaire**  
    On élève chaque \( c_i \) à la puissance de l'exposant de l'autre équation :
    - \( q_1 = c_1^{e_2} \mod N \)
    - \( q_2 = c_2^{e_1} \mod N \)

2. **Simplification**  
    Ces calculs donnent :
    - \( q_1 \equiv (2p + 3q)^{e_1 e_2} \mod N \)
    - \( q_2 \equiv (5p + 7q)^{e_1 e_2} \mod N \)

    Si les expressions sont binomiales, on peut isoler les termes en \( p \) :
    - \( q_1 \equiv (2p)^{e_1 e_2} \mod q \)
    - \( q_2 \equiv (5p)^{e_1 e_2} \mod q \)

3. **Calcul du diviseur commun**  
    On forme la différence :
    - \( D = 5^{e_1 e_2} q_1 - 2^{e_1 e_2} q_2 \)
    Cette différence est divisible par \( q \).

4. **Extraction de q**  
    On obtient alors :
    - \( q = \gcd(D, N) \)
    - \( p = N // q \)

### Script Python

```python
from math import gcd

# Données du problème
n = ... 
e1 = ... 
e2 = ... 
c1 = ... 
c2 = ... 


q1 = pow(c1, e2, n)
q2 = pow(c2, e1, n)


d = pow(5, e1 * e2, n) * q1 - pow(2, e1 * e2, n) * q2


q = gcd(d, n)
p = n // q

assert(p * q == n)
```