# Challenge : Déchiffrement AES Complet (AES-128)

## Explication du Défi

Ce challenge représente l'aboutissement de la série sur la structure d'AES. Il s'agit d'assembler toutes les étapes étudiées pour réaliser un **déchiffrement AES-128 complet** d'un chiffré fourni.

### Le Principe du Déchiffrement AES

Le déchiffrement AES inverse les étapes du chiffrement, en appliquant les opérations inverses dans l'ordre inverse :

1.  **`KeyExpansion`** est exécutée en premier (comme pour le chiffrement) pour générer toutes les clés de tour.
2.  Les étapes inverses (`InvSubBytes`, `InvShiftRows`, `InvMixColumns`) sont appliquées, et les clés de tour sont utilisées en **ordre inverse**.
3.  L'opération **`AddRoundKey`** est sa propre inverse (grâce à la propriété auto-inverse du XOR) et reste la même.

### La Tâche à Accomplir

1.  **Rassembler le Code :** Intégrer toutes les fonctions que vous avez codées (ou qui sont fournies) pour les étapes inverses (`InvSubBytes`, `InvShiftRows`, `InvMixColumns`, `AddRoundKey`).
2.  **Compléter la Fonction `decrypt` :** Écrire la logique de la fonction `decrypt` dans `aes_decrypt.py` pour orchestrer le processus de déchiffrement sur le chiffré donné, en respectant l'ordre inverse des opérations sur les clés de tour.

Le résultat final du déchiffrement est le **texte clair**, qui est le *flag*.

## Résolution du Défi

La fonction decrypt a pour but de déchiffrer un message chiffré (ciphertext) en utilisant la clé secrète (key) selon l'algorithme AES.

```Python
def decrypt(key, ciphertext):
    round_keys = expand_key(key) # Remember to start from the last round key and work backwards through them when decrypting

    # Convert ciphertext to state matrix
    state = bytes2matrix(ciphertext)

    # Initial add round key step
    state = add_round_key(state, round_keys[-1])

    for i in range(N_ROUNDS - 1, 0, -1):
        inv_shift_rows(state)
        inv_sub_bytes(state)
        state = add_round_key(state, round_keys[i])
        inv_mix_columns(state)

    # Last round
    inv_shift_rows(state)
    inv_sub_bytes(state)
    state = add_round_key(state, round_keys[0])

    # Convert state matrix to plaintext
    plaintext = matrix2bytes(state)

    return plaintext
```