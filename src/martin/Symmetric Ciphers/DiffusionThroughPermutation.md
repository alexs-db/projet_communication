# Challenge : Diffusion (ShiftRows et MixColumns)

## Explication du Défi

Ce challenge porte sur la **diffusion**, la seconde propriété essentielle d'un chiffrement sécurisé (avec la confusion). La diffusion garantit qu'une petite modification dans le texte clair affecte largement le texte chiffré (**Effet Avalanche**).

Les étapes **`ShiftRows`** et **`MixColumns`** d'AES travaillent de concert pour réaliser cette diffusion.

---

### 1. ShiftRows (Décalage de Lignes)

C'est l'opération la plus simple, mais vitale :

* Elle **déplace (décale)** les octets de chaque ligne de la matrice d'état vers la gauche (avec enveloppement).
* La ligne 1 ne bouge pas, la ligne 2 décale d'une colonne, la ligne 3 de deux, et la ligne 4 de trois.
* **Objectif :** Empêcher que les colonnes soient chiffrées indépendamment, assurant ainsi que la substitution d'un octet affecte toute la ligne.

### 2. MixColumns (Mélange de Colonnes)

C'est l'opération la plus complexe, réalisée après `ShiftRows` :

* Elle applique une **multiplication matricielle** dans le **corps de Galois de Rijndael ($\text{GF}(2^8)$)** entre chaque colonne de l'état et une matrice fixe prédéfinie.
* **Objectif :** Garantir que chaque octet d'une colonne influence *tous* les octets de la colonne résultante.

En combinant `ShiftRows` et `MixColumns`, chaque octet de la matrice d'état influence tous les autres octets en seulement deux tours d'AES.

---

## La Tâche à Accomplir

Vous devez implémenter l'étape inverse pour le déchiffrement :

1.  **Implémenter la fonction `inv_shift_rows`** (l'inverse de `ShiftRows`, qui décale les lignes vers la droite).
2.  Appliquer les opérations suivantes à l'état initial (chiffré) :
    * **`inv_mix_columns`** (fourni).
    * **`inv_shift_rows`** (que vous implémentez).
3.  **Convertir** la matrice d'état finale en octets pour obtenir le *flag*.

## Résolution du Défi

Ce code Python implémente les étapes de diffusion du chiffrement AES, y compris ShiftRows et MixColumns, et utilise les fonctions inverses pour déchiffrer un état de matrice donné.

```Python
def shift_rows(s):
    s[0][1], s[1][1], s[2][1], s[3][1] = s[1][1], s[2][1], s[3][1], s[0][1]
    s[0][2], s[1][2], s[2][2], s[3][2] = s[2][2], s[3][2], s[0][2], s[1][2]
    s[0][3], s[1][3], s[2][3], s[3][3] = s[3][3], s[0][3], s[1][3], s[2][3]


def inv_shift_rows(s):
    s[1][1], s[2][1], s[3][1], s[0][1] = s[0][1], s[1][1], s[2][1], s[3][1]
    s[2][2], s[3][2], s[0][2], s[1][2] = s[0][2], s[1][2], s[2][2], s[3][2]
    s[3][3], s[0][3], s[1][3], s[2][3] = s[0][3], s[1][3], s[2][3], s[3][3]


# learned from http://cs.ucsb.edu/~koc/cs178/projects/JT/aes.c
xtime = lambda a: (((a << 1) ^ 0x1B) & 0xFF) if (a & 0x80) else (a << 1)


def mix_single_column(a):
    # see Sec 4.1.2 in The Design of Rijndael
    t = a[0] ^ a[1] ^ a[2] ^ a[3]
    u = a[0]
    a[0] ^= t ^ xtime(a[0] ^ a[1])
    a[1] ^= t ^ xtime(a[1] ^ a[2])
    a[2] ^= t ^ xtime(a[2] ^ a[3])
    a[3] ^= t ^ xtime(a[3] ^ u)


def mix_columns(s):
    for i in range(4):
        mix_single_column(s[i])


def inv_mix_columns(s):
    # see Sec 4.1.3 in The Design of Rijndael
    for i in range(4):
        u = xtime(xtime(s[i][0] ^ s[i][2]))
        v = xtime(xtime(s[i][1] ^ s[i][3]))
        s[i][0] ^= u
        s[i][1] ^= v
        s[i][2] ^= u
        s[i][3] ^= v

    mix_columns(s)


state = [
    [108, 106, 71, 86],
    [96, 62, 38, 72],
    [42, 184, 92, 209],
    [94, 79, 8, 54],
]

inv_mix_columns(state)
inv_shift_rows(state)
print(bytes(sum(state, [])))
```