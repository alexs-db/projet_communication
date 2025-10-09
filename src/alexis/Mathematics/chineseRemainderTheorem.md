# Explication du challenge

Le théorème des restes chinois permet de résoudre un système de congruences linéaires lorsque les moduli sont premiers entre eux. Ici, nous avons :

- x ≡ 2 mod 5
- x ≡ 3 mod 11
- x ≡ 5 mod 17

Nous cherchons la solution x telle que x ≡ a mod 935, où 935 = 5 × 11 × 17.

Le code Python ci-dessous utilise la fonction `inverse` pour calculer les inverses modulaires nécessaires à l'application du théorème :

```python
from Crypto.Util.number import *

# Système de congruences :
# x ≡ 2 mod 5
# x ≡ 3 mod 11
# x ≡ 5 mod 17

resultat = (
    2 * 11 * 17 * inverse(11 * 17, 5) +
    3 * 5 * 17 * inverse(5 * 17, 11) +
    5 * 5 * 11 * inverse(5 * 11, 17)
) % 935

print(resultat)
```

La solution unique est donc **x ≡ 872 mod 935**.