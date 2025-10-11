## Explication du challenge

```python
def matrix2bytes(matrix):
    return bytes(sum(matrix, []))
```

La fonction `matrix2bytes` prend en entrée une matrice 4x4 (utilisée dans l'algorithme AES) et la convertit en une séquence de 16 octets. Elle "aplatit" la matrice en une seule liste, puis transforme cette liste en objet `bytes`. Cela permet de repasser du format matriciel (utilisé pour les opérations internes d'AES) au format brut des données (utilisé pour le chiffrement ou le déchiffrement).