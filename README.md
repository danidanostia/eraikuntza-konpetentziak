[LEEME.md](https://github.com/user-attachments/files/35017608/LEEME.md)
# App de evaluación por competencias · Easo Politeknikoa
Dpto. Edificación y Obra Civil · CFGS Proyectos de Edificación · versión 2.0.0

## Qué hay en esta carpeta

| Archivo | Para qué sirve | ¿Se sube a GitHub? |
|---|---|---|
| `index.html` | La app completa | Sí |
| `manifest.webmanifest` | Permite instalarla en el móvil | Sí |
| `sw.js` | Hace que funcione sin conexión | Sí |
| `icons/` (4 imágenes) | Iconos de la app instalada | Sí |
| `Code.gs` | Script que va dentro de la hoja de Google | **No** (se pega en Apps Script) |
| `LEEME.md` | Esta guía | Opcional |

---

## 1. Publicar la app en GitHub Pages

1. En GitHub, crea un repositorio nuevo (por ejemplo `easo-competencias`). Para GitHub Pages gratuito tiene que ser **público**: no pasa nada, porque **la app no contiene ningún dato del alumnado**. Los datos están en cada dispositivo y en tu hoja de Google.
2. *Add file → Upload files* y arrastra `index.html`, `manifest.webmanifest`, `sw.js` y la carpeta `icons` entera. *Commit changes*.
3. *Settings → Pages → Build and deployment*: «Deploy from a branch», rama `main`, carpeta `/ (root)`. Guardar.
4. En un par de minutos la app estará en `https://TU-USUARIO.github.io/easo-competencias/`.

> **Nunca subas a GitHub la URL del script ni la clave.** La app las guarda solo en cada dispositivo.

---

## 2. Crear la hoja del departamento con tu cuenta de TRABAJO

Hazlo **una sola vez**, solo tú.

**Antes de empezar:** abre un perfil de Chrome (o una ventana de incógnito) donde **solo** esté iniciada tu cuenta de trabajo. Apps Script falla a menudo cuando hay varias cuentas de Google abiertas a la vez.

1. Entra en Google Drive con la cuenta de trabajo y crea una **hoja de cálculo nueva**. Ponle un nombre, por ejemplo «Evaluación competencias · Edificación».
2. Menú **Extensiones → Apps Script**.
3. Borra lo que aparezca y **pega el contenido completo de `Code.gs`**.
4. Cambia esta línea por una frase larga que solo conozca el departamento (mínimo 8 caracteres):
   ```js
   const CLAVE = "CAMBIA-ESTA-CLAVE";
   ```
   Por ejemplo: `const CLAVE = "edificacion-easo-2026-ladrillo-azul";`
5. Guarda (icono del disquete).
6. **Implementar → Nueva implementación →** rueda dentada → **Aplicación web**.
   - Ejecutar como: **Yo** (tu correo de trabajo)
   - Quién tiene acceso: **Cualquier usuario**
7. Pulsa *Implementar* y autoriza los permisos. Si aparece «Google no ha verificado esta aplicación», es normal en scripts propios: *Configuración avanzada → Ir a (nombre del proyecto)*.
8. Copia la **URL de la aplicación web** (termina en `/exec`).
9. Comprueba que funciona: pega esa URL en el navegador. Debe salir un texto con `"ok":true`.

**Si no aparece la opción «Cualquier usuario»,** el administrador de las cuentas del centro la tiene bloqueada. En ese caso la app no puede conectarse con esa cuenta y hay que pedir al administrador que lo permita para este script.

**Compartir la hoja con los compañeros** (para consultarla, no es necesario para usar la app): *Compartir* → añade sus correos como **Lector**. No les des permiso de edición: la pestaña oculta `_datos` es la base de datos y no debe tocarse a mano.

### Si algún día cambias `Code.gs`
*Implementar → Gestionar implementaciones →* ✏️ *→ Versión: «Nueva versión» → Implementar.* Así la URL sigue siendo la misma y nadie tiene que reconfigurar nada.

---

## 3. Conectar cada dispositivo (tú y los otros cuatro profesores)

1. Abrir la app (el enlace de GitHub Pages).
2. Pulsar el botón **☁️** de la cabecera.
3. Rellenar **tu nombre** (queda registrado quién cambia cada nota), la **URL** del script y la **clave**.
4. *Guardar y sincronizar.*

A los compañeros solo hay que darles **el enlace de la app, la URL del script y la clave**. No necesitan cuenta de Google ni tocar la hoja.

**Conéctate tú primero** y mete el alumnado. Así los demás lo descargan ya hecho.

### Instalarla en el móvil (muy recomendable)
- **Android/Chrome:** menú ⋮ → «Instalar aplicación» (o el botón *Instalar la app* en Ajustes).
- **iPhone/iPad (Safari):** botón Compartir → «Añadir a pantalla de inicio».

En iPhone esto es importante. Si la app **no** está instalada y pasas unos días sin abrirla, Safari puede borrar los datos guardados en el teléfono. Instalada no ocurre, y en cualquier caso la hoja de Google conserva la copia del departamento.

---

## 4. Cómo funciona la sincronización

- Cada nota, actividad, alumno/a y configuración de módulo se guarda por separado, con su fecha y su autor.
- Si dos profesores tocan cosas distintas a la vez, se combinan sin pisarse.
- Si dos tocan **la misma casilla**, se queda la edición más reciente y la app avisa.
- Se sincroniza sola al abrir la app, unos segundos después de cada cambio y cada 2 minutos. También puedes forzarlo en *Ajustes → Sincronizar ahora*.
- **Sin conexión se sigue trabajando.** El punto del botón ☁️ se pone ámbar con los cambios pendientes y se suben al recuperar la conexión.
- Colores del punto ☁️: verde = al día · ámbar = cambios pendientes · azul = sincronizando · rojo = error (pulsa el botón ☁️ para ver el detalle) · gris = sin conectar.

### Qué verás en la hoja de Google
- **Índice:** todos los módulos en uso, con enlace a su pestaña, nº de alumnos, nº de actividades y último cambio (y de quién).
- **Una pestaña por curso + grupo + módulo** (por ejemplo `26-27 1º 0562`), con una fila por alumno/a: nota de cada competencia, nota ordinaria y extraordinaria, estado, control por RA, notas de cada actividad y observaciones. Los aprobados se ven en verde y los suspensos en rojo. Se regenera sola: no la edites.
- `_datos` y `_registro` (ocultas): la base de datos y quién sincronizó cuándo.
- Menú **Easo · Competencias** → «Regenerar todas las pestañas» por si alguna se queda desactualizada.

---

## 5. Uso diario

- **Notas seguidas:** escribe la nota y pulsa **Enter** para bajar al siguiente alumno/a (Mayús+Enter sube). Acepta coma decimal (7,5). Una nota fuera de 0–10 se marca en rojo y no se guarda.
- **Casilla vacía (—)** = sin evaluar: no cuenta en la media ni penaliza.
- **Rúbrica 1–4:** al crear la actividad marca «Calificar con rúbrica». Desde el móvil basta con tocar 1, 2, 3 o 4. Por defecto equivalen a 2,5 / 5 / 7,5 / 10, y puedes cambiarlo en cada actividad.
- **Evaluaciones:** 1ª evaluación, 2ª evaluación, final ordinaria y final extraordinaria. El semáforo es **acumulado**: «2ª evaluación» incluye la 1ª, y la final ordinaria incluye las dos.
- **Recuperaciones:** marca la actividad como «de recuperación» (en la extraordinaria lo son todas). Solo sustituyen las competencias **por debajo de 5**, se queda la nota más alta y la original se conserva en la ficha (orig. → rec.).
- **Nota del módulo** = media ponderada de las competencias según su peso. El módulo figura como **superado** solo si **todas** las competencias que cuentan están en 5 o más. Una competencia con peso 0 % no cuenta.
- **Control por RA:** cada RA toma la nota de sus competencias vinculadas, y el peso del RA da una nota de control (ficha, CSV y hoja).
- **Editar o borrar actividades:** ✎ y ✕ en la cabecera de cada columna. Al borrar aparece **«Deshacer»** durante unos segundos. Lo mismo al dar de baja a un alumno/a o borrar una competencia.
- **Observaciones:** en la ficha de cada alumno/a. Son **de cada módulo**, así que cada profesor tiene las suyas.
- **Acta:** «Imprimir acta» genera una hoja limpia con cabecera (curso, grupo, módulo, periodo, profesor/a), tabla de competencias y firma. «Imprimir ficha» hace lo mismo para un alumno/a.
- **CSV:** compatible con Excel en castellano (punto y coma, coma decimal).
- **Nuevo curso (+):** eliges qué pasa con cada alumno/a (pasa a 2º, repite, no continúa, termina o sigue en 2º). Se copian competencias, RA y, si quieres, las actividades sin notas.
- **ES / EU:** cambia todo el idioma y se recuerda.

---

## 6. Copias de seguridad

- La hoja de Google ya es la copia central del departamento.
- Aun así, al final de cada evaluación: *Ajustes → Descargar copia (JSON)*.
- *Restaurar copia (JSON)* combina la copia con lo que haya: nunca sustituye una nota más reciente por otra más antigua.
- Antes de importar o de borrar los datos del dispositivo, la app guarda sola un estado anterior. Para volver a él: *Ajustes → Volver al estado anterior*.
- **Modo ejemplo** (*Ajustes → Probar con datos de ejemplo*): datos ficticios para enseñar la app. No se guardan ni se suben a la hoja.

---

## 7. Actualizar la app más adelante

Sube el nuevo `index.html` a GitHub y sustituye el anterior. Los dispositivos cogen la versión nueva la próxima vez que abran la app con conexión. Si cambias iconos o el manifiesto, sube también el número de `CACHE` dentro de `sw.js`.

Los datos **no se pierden** al actualizar. Si en un dispositivo había datos de la versión anterior de la app (la de un solo archivo), aparece un aviso para importarlos.

---

## 8. Pendiente de revisar por el departamento
- **Euskera:** la traducción de la interfaz y de las competencias conviene que la revise un compañero euskaldun.
- **Competencias y RA precargados:** son una propuesta actualizada (BIM, escáner láser, Scan-to-BIM, fotogrametría con dron, nubes de puntos, CDE, Código Estructural…). Cada profesor puede ajustarlos en *Ajustes* para su módulo y curso. Lo que cambie se sincroniza para todos.
