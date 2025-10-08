# CryptoHack Mini-Project

Projet réalisé dans le cadre du cours de **Communication** (Master 1 Cybersécurité, Université de Caen).

## Objectif
Résoudre plusieurs challenges sur [CryptoHack](https://cryptohack.org) pour comprendre et expérimenter les principes fondamentaux et appliqués de la cryptographie. Le projet couvre notamment :

- **Fondamentaux et arithmétique modulaire**
  - notions de base (hex, base64, ascii), manipulation d'entiers et opérations modulo,
  - plus avancé : PGCD, inverse modulaire, théorème du reste chinois, racine carrée modulaire, symboles de Legendre et résidus quadratiques.

- **Cryptographie asymétrique (RSA, signatures)**
  - génération et structure des clés publiques/privées,
  - fonctions arithmétiques utiles (exponentiation modulaire, totient d'Euler),
  - faiblesses et variantes (factoring, RSA multi-prime, attaques pratiques, signatures).

- **Échanges de clés / Diffie-Hellman & courbes elliptiques**
  - groupes et générateurs, arithmétique dans les corps, bases de Diffie-Hellman,
  - introduction aux courbes elliptiques et concepts associés.

- **Chiffrement symétrique et AES**
  - structure d'AES (substitution, permutation, round keys),
  - concepts de confusion et diffusion,
  - modes de fonctionnement (CBC, CTR, etc.), gestion des clés et résistance au bruteforce.

- **Cryptographie appliquée sur le web**
  - protocoles TLS (handshake, décryptage qualitatif), sécurisation des échanges,
  - tokens et authentification (JWT, JOSE), vulnérabilités courantes côté serveur/client.

- **Opérations binaires et encodages**
  - XOR et ses propriétés (attaques basiques), opérations sur les octets et conversion grand entier,
  - encodages courants (hex, base64) et défis d'encodage.

- **Outils et bonnes pratiques**
  - gestion des clés SSH / certificats, automatisation, bonnes pratiques de scripting,
  - structuration du code, tests et documentation.

L'objectif est de combiner la pratique (résolution des challenges) avec l'explication théorique et la mise en perspective pratique (exemples, scripts, captures) dans le rapport.

## Équipe
- Alexis Debra
- Martin Vicquelin

## ️Organisation du dépôt
- `src/` : scripts de résolution des challenges
- `docs/` : gestion de projet (plan, suivi)
- `report/` : rapport LaTeX
- `presentation/` : slides de soutenance