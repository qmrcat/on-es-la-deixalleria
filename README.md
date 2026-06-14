# On és la deixalleria mòbil de Reus?

Aplicació web per consultar els dies, horaris i ubicacions de la deixalleria
mòbil de Reus.

La pàgina calcula automàticament les dates mensuals de cada punt a partir de
regles com ara el primer dilluns, el segon i quart divendres o l'últim dia
laborable del mes.

## Funcionalitats

- Calendari mensual dels serveis.
- Proper servei destacat.
- Cerca per carrer o barri.
- Desplegable amb les 16 ubicacions.
- Filtre per mes i any.
- Vista adaptada a ordinadors i dispositius mòbils.
- Enllaços per obrir cada ubicació a Google Maps.
- Detall de l'horari i de la regla aplicada.
- Botó per compartir la pàgina.
- Instal·lació com a aplicació web progressiva (PWA).
- Funcionament sense connexió després de la primera visita.

## Estructura

```text
.
├── index.html
├── punts.json
├── manifest.webmanifest
├── service-worker.js
├── icon.svg
└── README.md
```

- `index.html`: interfície, estils i lògica del calendari.
- `punts.json`: ubicacions i freqüències dels serveis.
- `manifest.webmanifest`: configuració de l'aplicació instal·lable.
- `service-worker.js`: memòria cau i funcionament sense connexió.
- `icon.svg`: icona de la web i de la PWA.

## Modificar les ubicacions

Les dades es troben a `punts.json`. Cada ubicació té aquest format:

```json
{
  "lloc": "Plaça Llibertat",
  "dates": "2n dissabte de mes (matins), l'últim dissabte de cada mes (tardes)"
}
```

Per afegir una ubicació, incorpora un objecte nou dins de la llista i separa'l
de l'anterior amb una coma.

Els dos camps són obligatoris:

- `lloc`: adreça o nom de la ubicació.
- `dates`: regla mensual i, opcionalment, l'horari.

La lògica actual reconeix:

- `primer`, `segon`, `tercer` i `quart`;
- les formes abreujades `1r`, `2n`, `3r` i `4t`;
- els dies de dilluns a diumenge;
- `últim dia laborable`;
- `últim dissabte`, `últim diumenge` o un altre dia concret;
- els horaris de `matí` i `tarda`.

Després de modificar les dades, comprova que el JSON continuï sent vàlid.

## Execució local

El projecte utilitza `fetch()` per carregar `punts.json`, per tant no convé
obrir `index.html` directament amb el protocol `file://`. Cal servir la carpeta
amb un servidor web local.

Amb Python:

```bash
python -m http.server 8000
```

Després obre:

```text
http://localhost:8000
```

No cal instal·lar dependències ni executar cap procés de compilació.

## Publicació

És una web estàtica i es pot desplegar a GitHub Pages, Netlify, Vercel o
qualsevol servidor HTTP.

Repositori:

https://github.com/qmrcat/on-es-la-deixalleria

## Consideracions

El càlcul de l'últim dia laborable exclou dissabtes i diumenges, però no té en
compte els festius locals. Les ubicacions i els horaris s'han de contrastar
amb la informació oficial de l'Ajuntament de Reus.

## Llicència

Aquest projecte es publica sota [CC0 1.0 Universal](LICENSE). En la mesura que
ho permet la llei, es pot copiar, modificar, distribuir i utilitzar, també amb
finalitats comercials, sense demanar permís ni atribuir-ne l'autoria.
