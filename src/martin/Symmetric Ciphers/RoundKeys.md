# Challenge : AddRoundKey (AES)

## Explication du Défi

Ce challenge porte sur l'étape **`AddRoundKey`** (Ajout de Clé de Tour) du chiffrement par blocs **AES (Advanced Encryption Standard)**, qui est la seule étape où la clé est directement mélangée aux données.

### Le Principe de `AddRoundKey`

L'opération `AddRoundKey` est simple : elle effectue un **OU Exclusif (XOR)** entre :
1.  L'état actuel des données (représenté par une matrice 4x4).
2.  La **clé de tour** correspondante (également une matrice 4x4) générée lors de la phase `KeyExpansion`.

Cette étape est cruciale car elle injecte le secret (la clé) dans le processus de chiffrement. Le XOR est facilement réversible si la clé est connue (simplement en appliquant à nouveau le XOR avec la même clé).

### La Phase du Chiffrement

Le processus AES commence par une étape `AddRoundKey` initiale et la répète comme dernière étape de chacune des 10 à 14 "rondes" (tours) de chiffrement.

### La Tâche à Accomplir

1.  **Compléter la fonction `add_round_key`** dans le fichier `add_round_key.py`. Cette fonction doit implémenter l'opération XOR entre l'état actuel et la clé de tour.
2.  **Utiliser la fonction `matrix2bytes`** fournie pour convertir la matrice d'état finale en une séquence d'octets.

Le résultat en octets sera votre *flag*.

## Résolution du Défi

Ce code simule l'étape AddRoundKey du chiffrement AES en appliquant une opération de OU Exclusif (XOR) entre deux matrices 4x4, mais en utilisant une syntaxe très compacte : la compréhension de liste imbriquée.

```Python
state = [
    [206, 243, 61, 34],
    [171, 11, 93, 31],
    [16, 200, 91, 108],
    [150, 3, 194, 51],
]

round_key = [
    [173, 129, 68, 82],
    [223, 100, 38, 109],
    [32, 189, 53, 8],
    [253, 48, 187, 78],
]

def add_round_key(s, k):
    return [[sss^kkk for sss, kkk in zip(ss, kk)] for ss, kk in zip(s, k)]

print(add_round_key(state, round_key))
```