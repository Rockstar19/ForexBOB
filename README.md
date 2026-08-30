# Visor Multi-Divisa

Sitio estático (sin build). Estructura:

- `index.html` — la aplicación (visor de velas, dibujo, Fibonacci, SMA/EMA, calculadora).
- `lightweight-charts.js` — librería de gráficos TradingView (embebida localmente, sin CDN).
- `bob_data.js` — datos históricos del boliviano paralelo, precargados como `window.__BOB_DATA__`.

## Desplegar en Vercel desde Git

    git init
    git add .
    git commit -m "Visor multidivisa"
    git branch -M main
    git remote add origin https://github.com/<tu-usuario>/<tu-repo>.git
    git push -u origin main

Luego conectar el repo a Vercel (proyecto en el equipo oporto-ind). No requiere build:
framework "Other", sin comando de build, output = raíz.
