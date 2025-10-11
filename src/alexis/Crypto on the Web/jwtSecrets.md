## Explication du challenge

```python
import jwt

encoded = jwt.encode({'username':'cb', 'admin':'true'}, 'secret', algorithm='HS256')
print(encoded)
```

Ce code utilise la bibliothèque Python `jwt` pour générer un token JWT signé avec l'algorithme HS256 (HMAC-SHA256). Les données embarquées dans le token sont le nom d'utilisateur (`username`) et un indicateur d'administrateur (`admin`). La clé secrète utilisée pour signer le token est simplement `'secret'`, ce qui est très faible et dangereux en production.

**Explication :**
- HS256 est un algorithme symétrique : la même clé sert à signer et à vérifier le token.
- Si cette clé est compromise ou trop simple, n'importe qui peut générer des tokens valides et usurper des sessions, y compris des sessions administrateur.
- Il est donc crucial d'utiliser une clé secrète forte et de la protéger correctement, ou mieux, d'utiliser un algorithme asymétrique comme RS256.