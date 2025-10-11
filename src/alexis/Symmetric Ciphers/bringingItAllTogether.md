# Explication du challenge

Ce fichier présente une implémentation minimaliste du déchiffrement AES-128 en Python. L'objectif est de déchiffrer un bloc chiffré à l'aide d'une clé donnée et d'afficher le texte en clair (le flag).

## Structure du code

- **SubBytes / InvSubBytes** : Appliquent une substitution non linéaire sur chaque octet du bloc via la S-box (et son inverse pour le déchiffrement). Cela apporte de la confusion.
- **ShiftRows / InvShiftRows** : Décalent les lignes de l'état pour diffuser les octets.
- **MixColumns / InvMixColumns** : Mélangent les colonnes pour renforcer la diffusion.
- **AddRoundKey** : Combine l'état avec la clé de ronde via XOR. Cette opération est son propre inverse.
- **KeyExpansion** : Génère toutes les clés de ronde à partir de la clé principale.

## Déroulement du déchiffrement

1. **Expansion de la clé** : On génère les clés de ronde nécessaires.
2. **Initialisation de l'état** : On convertit le bloc chiffré en matrice d'état.
3. **Ajout de la dernière clé de ronde** : On commence par la clé de la dernière ronde.
4. **Boucle des rondes inverses** : On applique les opérations inverses dans l'ordre inverse (InvShiftRows, InvSubBytes, AddRoundKey, InvMixColumns).
5. **Dernière ronde** : On termine par InvShiftRows, InvSubBytes et AddRoundKey (sans InvMixColumns).
6. **Conversion en texte** : On récupère le texte en clair.

```python
if __name__ == "__main__":
    plaintext = decrypt(key, ciphertext)
    print(plaintext.decode())
```

Le fichier de résolution est présent dans le même répertoire, si besoin.