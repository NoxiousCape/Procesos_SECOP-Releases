# Procesos SECOP — Releases

Repositorio **público** de descargas de la app de escritorio **Procesos SECOP**.

Aquí sólo viven los instaladores publicados (`ProcesosSECOP-<versión>-Setup.exe`
y su `sha256.txt`). El código vive en [`NoxiousCape/Procesos_SECOP`](https://github.com/NoxiousCape/Procesos_SECOP),
que es **privado**: la app necesita leer este repo sin ningún token, por eso
este hermano es público y el `.exe` no lleva ningún secreto dentro.

## Publicar una versión

Sólo se cambia la versión en el fichero `VERSION` del repo de código; de ahí
salen el nombre del instalador, `GET /health`, el tag y la comparación de
versiones de la app.

```powershell
Set-Content VERSION 1.2.0
scripts\package.ps1
git commit -am "..."
git tag v1.2.0
git push origin main v1.2.0
```

Con eso la workflow `.github/workflows/release.yml` empaqueta y sube el `.exe`
a este repo. También se puede hacer a mano, con el mismo resultado:

```powershell
gh release create v1.2.0 --repo NoxiousCape/Procesos_SECOP-Releases `
  --notes "sha256: <hex>" build\installer\ProcesosSECOP-1.2.0-Setup.exe
```

La **descripción del release** tiene que llevar `sha256: <hex>`: es de donde la
lee la app para verificar el instalador antes de dejararlo en `Descargas`.

## Cómo lo ve el usuario

`Configuración → Actualizaciones` en la app: **Buscar actualización**,
**Descargar** con barra de progreso y **Abrir carpeta** al terminar. El
instalador se guarda en `Descargas` y hay que ejecutarlo a mano.

Enlaces directos: [releases](https://github.com/NoxiousCape/Procesos_SECOP-Releases/releases)
