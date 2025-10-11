# Challenge : Transparence des Certificats (Certificate Transparency)

## Explication du Défi

Ce challenge porte sur la **sécurité des certificats TLS/SSL** et le concept de **Transparence des Certificats (CT)**.

### Le Problème
Le modèle de sécurité du web repose sur les **Autorités de Certification (CA)**, qui doivent émettre des certificats TLS uniquement aux propriétaires légitimes des domaines. Historiquement, des CA ont été compromises ou ont commis des erreurs, émettant des certificats frauduleux pour des domaines légitimes (comme Google ou Microsoft), ce qui met en péril la sécurité de la navigation.

### La Solution : Certificate Transparency (CT)
Depuis 2018, de grands acteurs comme Google exigent que toute CA publie **chaque certificat émis** dans un journal public et consultable. Ce système permet aux propriétaires de domaines et aux utilisateurs de surveiller et de détecter rapidement tout certificat frauduleux.

---

## La Tâche à Accomplir

Un fichier **`transparency.pem`** contenant une **clé publique RSA (au format PEM)** est fourni. Cette clé correspond à un certificat TLS qui a été publié.

**Votre mission est :**

1.  **Rechercher** cette clé publique dans les **journaux publics de Certificate Transparency** (CT logs).
2.  **Identifier** le sous-domaine de `cryptohack.org` qui utilise cette clé publique dans son certificat TLS.
3.  **Visiter** ce sous-domaine pour obtenir le *flag*.

## Résolution du Défi

Ce script Python lit une clé publique RSA au format PEM et calcule son empreinte numérique (fingerprint) en utilisant l'algorithme de hachage SHA-256. Ce résultat est souvent utilisé pour rechercher la clé dans les bases de données publiques comme celles de la Transparence des Certificats (Certificate Transparency).

```Python
import hashlib
from Crypto.PublicKey import RSA

pem = open('transparency.pem', 'r').read()

key = RSA.importKey(pem).public_key()

der = key.exportKey(format='DER')

sha256 = hashlib.sha256(der)

sha256_fingerprint = sha256.hexdigest()

print(f"Public Key SHA256: {sha256_fingerprint}")
```