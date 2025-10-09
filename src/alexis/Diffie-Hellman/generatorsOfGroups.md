## Explication du challenge

### Théorème pour identifier un générateur

On utilise le théorème suivant (issu de la théorie des corps) :
> Soit \( p > 2 \) un nombre premier et \( \alpha \in \mathbb{Z}_p^* \). Alors \( \alpha \) est un élément primitif modulo \( p \) si et seulement si
> \[
> \alpha^{\frac{p-1}{q}} \not\equiv 1 \pmod{p}
> \]
> pour tout nombre premier \( q \) tel que \( q \mid (p-1) \).

Le code suivant permet de trouver le plus petit élément primitif de \( \mathbb{F}_p \) pour \( p = 28151 \) :

```python
from primefac import primefac

p = 28151
totient = p - 1 
totient_factors = set(primefac(totient))

for candidate in range(2, p):
    is_primitive = True
    for factor in totient_factors:
        exp = totient // factor
        power = pow(candidate, exp, p)
        if power == 1:
            is_primitive = False
            break
    if is_primitive:
        print(f'Le plus petit générateur pour p={p} est : {candidate}')
        break
```

#### Explication du code

- On calcule les facteurs premiers de \( p-1 \) (car l'ordre du groupe multiplicatif est \( p-1 \)).
- Pour chaque candidat \( g \) de 2 à \( p-1 \), on vérifie pour chaque facteur premier \( q \) de \( p-1 \) que \( g^{(p-1)/q} \not\equiv 1 \pmod{p} \).
- Si cette condition est vérifiée pour tous les facteurs, alors \( g \) est un générateur (élément primitif).
- Le premier candidat qui satisfait cette propriété est le plus petit générateur.