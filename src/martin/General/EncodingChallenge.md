# Challenge : Automation d'Encodages (100 Niveaux)

## Explication du Défi

Ce challenge est un exercice de programmation visant à **automatiser la gestion de multiples types d'encodage** pour obtenir un *flag*.

Le but est de **réussir 100 niveaux consécutifs** en vous connectant à un serveur interactif (similaire à un *socket*) :

1.  Le serveur vous **envoie un message encodé** (ou un *challenge*).
2.  Vous devez **identifier le type d'encodage**.
3.  Vous devez **décoder le message**.
4.  Vous devez **renvoyer la réponse décodée** au serveur.

Si vous réussissez les 100 échanges, le serveur vous révélera le *flag*.

### Ressources Fournies :

* **`13377.py` :** Le code source du programme qui tourne sur le serveur.
* **`pwntools_example.py` :** Un exemple de début de solution utilisant la bibliothèque `pwntools` pour interagir avec le serveur.

## Résolution du Défi

# Explication Synthétique du Code d'Automatisation

Ce script Python utilise **`pwntools`** pour automatiser un challenge interactif de 100 niveaux. L'objectif est de décoder différents types d'encodages (Base64, Hex, ROT13, etc.) envoyés par un serveur.

---

## Fonctionnement Clé

1.  **Connexion :** Le script établit une connexion (*socket*) au serveur distant.
2.  **Mappage des Décodeurs :** Un dictionnaire (`d`) associe chaque nom d'encodage reçu (ex. `"base64"`) à la fonction Python capable de le décoder.
3.  **Boucle de 100 Niveaux :**
    * Le script **reçoit** le message du serveur sous format **JSON**.
    * Il **identifie** le type d'encodage.
    * Il **décode** la donnée reçue.
    * Il **renvoie** la réponse décodée au serveur, encapsulée à nouveau en **JSON**.
4.  **Succès :** Après 100 échanges réussis, le script utilise `io.interactive()` pour recevoir et afficher le **flag** final.

Ce programme permet donc de **gagner du temps** en gérant automatiquement la communication et le décodage répétitif.

```python
from pwn import *
from Crypto.Util.number import *
import json, codecs

d = {
        "base64": b64d,
        "hex": unhex,
        "rot13": lambda s: codecs.encode(s, 'rot_13').encode(),
        "bigint": lambda s: long_to_bytes(int(s, 0)),
        "utf-8": bytes
}

def dec(o):
    return d[o["type"]](o["encoded"])

io = remote("socket.cryptohack.org", 13377)
for _ in range(100):
    o = json.loads(io.recvline())
    io.sendline(json.dumps({"decoded": dec(o).decode()}))
io.interactive()
```
