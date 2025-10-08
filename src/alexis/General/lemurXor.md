## Explication du challenge

Ce script Python utilise la bibliothèque PIL pour effectuer un XOR visuel entre deux images (`lemur.png` et `flag.png`). Pour chaque pixel, il applique l'opération XOR sur les composantes RGB correspondantes des deux images, puis sauvegarde le résultat dans une nouvelle image (`lemur_xor_flag.png`). Cela permet de révéler une image cachée si les deux images ont été chiffrées avec la même clé.

### Code

```python
from PIL import Image

lemur = Image.open("lemur.png")
flag = Image.open("flag.png")

pixels_lemur = lemur.load() 
pixels_flag = flag.load()

for i in range(lemur.size[0]): 
    for j in range(lemur.size[1]):
        
        l = pixels_lemur[i,j]
        f = pixels_flag[i,j]

        
        r = l[0] ^ f[0]
        g = l[1] ^ f[1]
        b = l[2] ^ f[2]

        
        pixels_flag[i,j] = (r, g, b)

flag.save("lemur_xor_flag.png")
```