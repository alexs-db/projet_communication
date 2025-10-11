# Challenge : L'Inverse Multiplicatif

## Explication du Défi

Le défi consiste à trouver l'**inverse multiplicatif** d'un nombre dans un **corps fini** $\mathbf{F}_p$ (ici, $\mathbf{F}_{13}$).

Concrètement, nous devons déterminer un nombre entier unique, noté $d$, tel que la multiplication de l'élément donné (**3**) par $d$ donne un résultat équivalent à **1** modulo le nombre premier $p$ (**13**).

---

## La Question

Quel est l'élément inverse $d$ (souvent noté $3^{-1}$) qui satisfait la congruence suivante :

$$3 \cdot d \equiv 1 \pmod{13}$$

---

## Solution Efficace (Méthode Python)

Pour résoudre ce problème de manière rapide et sécurisée, on utilise le **Petit Théorème de Fermat** qui permet de calculer l'inverse $a^{-1} \pmod{p}$ comme $a^{p-2} \pmod{p}$.

En Python, la fonction `pow(base, exposant, module)` effectue ce calcul de manière optimisée.

Ici, $\text{base}=3$, $\text{module}=13$, et l'exposant est $13 - 2 = 11$.

```python
# pow(base, exposant, module)
# Calcule 3**(13-2) % 13
>>> pow(3, 13 - 2, 13)
>>> 9
```