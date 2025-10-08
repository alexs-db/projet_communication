## Explication du challenge
Un certificat SSL lie une clé cryptographique à des informations sur une organisation. Ici, on utilise un certificat x509 RSA encodé en DER. Certains outils (notamment sous Windows) préfèrent le format DER, mais d'autres exigent le format PEM. Il est donc utile de savoir convertir entre ces formats.

### Conversion DER → PEM

```sh
openssl x509 -inform der -in 2048b-rsa-example-cert.der -out cert.pem
```

### Extraction du modulus

Pour obtenir le modulus (en décimal) de la clé publique du certificat :

```sh
openssl x509 -inform der -in 2048b-rsa-example-cert.der -noout -modulus
```
Le modulus affiché est en hexadécimal. Pour le convertir en décimal :

1. Copier la valeur hexadécimale du modulus.
2. Utiliser un outil en ligne ou la commande suivante en Python :

```python
int("B4CFD15E3329EC0BCFAE76F5FE2DC899C67879B918F80BD4BAB4D79E02520609F418934CD470D142A0291392735077F60489AC032CD6F106ABAD6CC0D9D5A6ABCACD5AD2562651E54B088AAFCC190F253490B02A29410F55F16B93DB9DB3CCDCECEBC75518D74225DE49351432929C1EC669E33CFBF49AF8FB8BC5E01B7EFD4F25BA3FE596579A2479491727D7894B6A2E0D8751D9233D068556F858310EEE81997868CD6E447EC9DA8C5A7B1CBF24402948D1039CEFDCAE2A5DF8F76AC7E9BCC5B059F695FC16CBD89CEDC3FC129093785A75B45683FAFC4184F6647934351CAC7A850E73787201E72489259EDA7F65BCAF8793198CDB7515B6E030C708F859", 16)
```