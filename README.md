<h1 align="center">ReactJS Plesk hosting</h1>

## Vorwort

Bevor das Script funktionieren kann muss der `build`-Ordner der Anwendung hochgeladen werden!

Mehr Informationen zum hosten einer ReactJS Anwendung gibt in der [create-react-app Dokumentation](https://create-react-app.dev/docs/deployment/).

## index.js`

**Achtung:** _Wenn es sich um eine mehrseitige ReactSJ Anwendung handelt dann muss `app.get('/', ...)` durch `app.get('/*', ...)` setzt werden um alle Routen abrufen zu können._

```javascript
const express = require('express');
const path = require('path');
const app = express();

app.use(express.static(path.join(__dirname, 'build')));

app.get('/', function (req, res) {
  res.sendFile(path.join(__dirname, 'build', 'index.html'));
});

app.listen(80);

```

## .htaccess

**Anmerkung:** _Für Apache2 Server falls manche Routen nicht erreicht werden können._

```
Options -MultiViews
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^ index.html [QSA,L]
```