---
{"dg-publish":true,"permalink":"/mes-notes/https/xca/"}
---


# Générer une autorité de certification et un certificat auto-signé avec XCA

### 1ère étape: Créer une Autorité de Certification (CA)

Sur XCA, dans l'onglet Clés Privées, créez une nouvelle clée privée.

Ensuite, dans l'onglet Certificat, créez un nouveau certificat.

-   Dans "Source", n'oubliez pas de sélectionnez `[default] CA` en bas de la page, et d'appuyer sur "Appliquer tout"
-   Dans "Sujet", renseigner les différents champs demandés. La clé privée que vous avez précédemment créée devrait être séléctionné par défaut en bas de la page.

Notre autorité de certification est maintenant créée. Nous pourront signer des certificat avec.

### 2ième étape: Créer une demande de certificat

Dans l'onglet "Requête de signature de certficat", créez une requête.

-   Dans "Source", sélectionnez `[default] TLS_server` , puis "Appliquer tout"
-   Dans "Sujet", remplisser les champs demandés. _**Dans le champs "commonName, mettez le nom exact du site web"**_
-   Toujours dans "Sujet", créez une nouvelle clé privée.
-   Dans "Extension", modifier le DNS (la ligne "Subject Alternative Name"). Par exemple:

```
DNS: test.com, IP: 192.168.0.3
```

Votre requête est maintenant créée!

### 3ième étape: Signer la requête à l'aide de votre CA

Dans l'onglet "Requête", clic droit sur votre requête, et sélectionnez "Signer". Sur la page qui s'ouvre, au milieu, appuyez sur "Utiliser ce certificat pour signer", et choissisez l'autorité de certification que vous avez créer à la 1ère étape. Pas besoin de modèle en bas de la page.

Votre certificat est maintenant signé!

### 4ième étape: Exporter votre CA, votre clé et votre certificat.

Premièrement, on va exporter notre autorité de certification. Clic droit sur votre CA, et choisissez "Exporter", puis "Fichier". Laissez l'extension par défaut (_.cert_).

Deuxièmement, votre certificat et votre clé privée. On va les exporter en un seul fichier. Pour cela, sélectionnez votre certificat, clic droit dessus, choisissez "Exporter", puis "Fichier". Dans la fenêtre qui s'ouvre, changez l'extension pour `Chaîne PKCS#12 (.pfx)` . Ce fichier contient à la fois votre certificat et votre clée.