# Visor Multi-Divisa

Sitio estático (sin build). Estructura:

- `index.html` — la aplicación (visor de velas, dibujo, Fibonacci, SMA/EMA, calculadora).
- `lightweight-charts.js` — librería de gráficos TradingView (local, sin CDN).
- `bob_data.js` — datos históricos del boliviano paralelo, precargados como `window.__BOB_DATA__`.
- `data/` — CSV crudos de las divisas extranjeras, cargados automáticamente al abrir.

## Datos: cómo se cargan y cómo actualizarlos

Al abrir el sitio:
- El **boliviano** viene precargado y liviano desde `bob_data.js` (ya procesado a velas horarias).
- **USD/PEN, USD/CLP y USD/ARS blue** se cargan automáticamente desde `data/` si el
  archivo existe. El visor los procesa con su parser (auto-detecta separador decimal, BOM,
  columna Cierre/Último).

Archivos esperados en `data/` (CSV crudo de Investing.com, tal cual se descarga):
- `data/usd_pen.csv`
- `data/usd_clp.csv`
- `data/usd_arsb.csv`

### Actualizar una divisa (sobreescritura vía Git)
1. Descargá el CSV nuevo desde Investing.com.
2. Reemplazá el archivo correspondiente en `data/` (mismo nombre).
3. `git add data/ && git commit -m "actualizar datos" && git push`
4. Vercel redespliega solo. El sitio arranca con los datos nuevos.

El **botón "Cargar CSV" del sitio sigue funcionando** para pruebas: un archivo cargado a mano
pisa temporalmente al del repo, solo en memoria, sin tocar nada permanente.

### Boliviano desde CSV crudo (opcional)
Por defecto el boliviano viene de `bob_data.js` (más rápido). Si preferís servirlo desde un
CSV crudo en el repo, poné `data/usd_bob.csv` y descomentá la línea `bob:` en `DATA_FILES`
dentro de `index.html`. Es más pesado: se procesa en cada visita.

## Desplegar en Vercel desde Git

    git init
    git add .
    git commit -m "Visor multidivisa"
    git branch -M main
    git remote add origin https://github.com/<tu-usuario>/<tu-repo>.git
    git push -u origin main

Conectar el repo a Vercel (equipo oporto-ind). No requiere build:
framework "Other", sin comando de build, output = raíz.
