# Auditoría SGI — Sistema de auditorías internas

Aplicación web para ejecutar auditorías internas de sistemas de gestión, registrar la
evidencia objetiva de cada requisito y generar los informes por proceso.

## Normas incluidas

Cada auditoría se ejecuta **contra una norma**. Las normas de inocuidad se componen de
varios marcos normativos que se auditan juntos pero se reportan por separado.

| Norma | Empresa | Marcos normativos | En la lista | A evaluar | Procesos |
|---|---|---|---:|---:|---:|
| ISO 9001:2015 | COGUSA | ISO 9001:2015 | 65 | 155 | 16 |
| FSSC 22000 v6 — Producción de empaques (Cat. I) | COGUSA | ISO 22000:2018 (69) · INTE/ISO/TS 22002-4:2014 (64) · FSSC v6 §2.5 (64) | 197 | 285 | 12 |
| FSSC 22000 v6 — Almacenamiento y distribución (Cat. G) | DISCA | ISO 22000:2018 (67) · ISO/TS 22002-5:2019 (90) · FSSC v6 (49) | 206 | 206 | 4 |
| FSC Cadena de Custodia | COGUSA | FSC-STD-40-004 V3-1, partes I, II y III | 67 | 67 | 9 |

«En la lista» es el número de requisitos redactados; «a evaluar» es cuántas
verificaciones produce la asignación de origen, contando una por cada proceso al que se
audita un requisito. Ambas columnas cambian al configurar la lista (ver abajo).

Las listas reproducen las listas de verificación de la organización:
`Lista_Verificacion_ISO9001_2015.xlsx` y
`Lista_Verificacion_ISO22000_FSSCv6_con_Proceso.xlsx`.

## Qué se audita y dónde

La lista fuente de cada norma trae un proceso propuesto por requisito, y marca
**«Todos los procesos»** el que se audita en cada área con su propia evidencia. Eso es
solo el punto de partida: **la asignación real la define la organización** desde
**Listas de verificación → Configurar la lista**.

Un requisito puede auditarse en **varios procesos** —cada uno lo demuestra con sus
propios registros— o en **ninguno**, si se decide no evaluarlo. La lista efectiva es,
por tanto, un par *(requisito, proceso)* por fila. Cuando el auditor entra a un proceso
ve exactamente los requisitos que allí se le asignaron.

El configurador ofrece dos formas de trabajar sobre la misma matriz:

- **Por requisito** (vista de entrada) — cada requisito lleva **al lado su propia lista
  de procesos con scroll**, donde se marcan uno o varios sin salir de la fila. La
  cabecera de cada lista indica cuántos procesos van seleccionados y ofrece *Todos* y
  *Ninguno*; un requisito sin ninguno queda resaltado como «No se evalúa».
- **Por proceso** — se elige un proceso y se marca, sobre la norma completa, qué
  requisitos le tocan. Es la forma en que se planifica una auditoría de área.

También se pueden **agregar procesos** que la lista fuente no traía; quedan guardados en
cuanto tienen al menos un requisito asignado.

Los cambios se trabajan sobre un **borrador** y solo se escriben al pulsar **Guardar
cambios**: cambiar la asignación reordena la lista de verificación de toda la
organización, no conviene hacerlo clic a clic. Antes de guardar, la aplicación resume
cuántas asignaciones se agregan y se retiran, cuántos requisitos quedarían sin evaluar y
si hay auditorías en curso de esa norma. **Restablecer** descarta la configuración
guardada y devuelve la norma a la asignación de la lista fuente.

Cada fila de la lista de verificación se identifica por el requisito **y** el proceso
(`iso9001-r17@Compras`), de modo que reasignar un requisito no mueve el registro
guardado de ningún otro. Los requisitos importados a una norma después de configurarla
conservan su asignación de origen, para que ampliar una lista no los deje fuera de la
auditoría sin avisar.

> La lista de **FSC Cadena de Custodia** está redactada sobre la estructura oficial de
> FSC-STD-40-004 V3-1 y se marca en la aplicación como **borrador**: coteje el texto de
> cada cláusula contra la copia controlada del estándar antes de usarla en una auditoría
> de certificación.

## Requisitos comunes entre marcos

Un mismo requisito puede aparecer en varios de los marcos que componen una norma. En
lugar de preguntarlo tres veces, la aplicación lo presenta **una sola vez** y registra la
respuesta contra todas las cláusulas equivalentes.

La correlación proviene de la matriz de requisitos comunes de la organización: **33
grupos temáticos** que agrupan las cláusulas de FSSC 22000 v6, ISO/TS 22002-5 e
ISO 22000, con su nivel de solapamiento y el enfoque de verificación conjunta. En la
auditoría de DISCA, **205 de los 206 requisitos** quedan correlacionados a un grupo.

Cada requisito muestra el grupo al que pertenece, las cláusulas equivalentes de los otros
marcos y la evidencia común sugerida. La declaración de hallazgo cita todas las cláusulas
afectadas.

## Cómo audita un auditor

1. Ingresa con su correo y contraseña.
2. Abre la auditoría y **elige su proceso** de una lista con scroll que muestra, para cada
   uno, cuántos requisitos tiene, cuántos lleva evaluados, cuántas NC y el porcentaje de
   cumplimiento.
3. Se despliega la lista de verificación de ese proceso: los requisitos que se le
   asignaron en **Listas de verificación → Configurar la lista**.

## Qué registra cada requisito

Los campos siguen el orden real de la verificación:

1. **Evidencia documental**: los documentos evaluados, con código, revisión y fecha
2. **Observaciones**: lo observado en esos documentos
3. **Resultado**: Cumple / Cumple Parcialmente / No Cumple / No Aplica / Pendiente
4. **Tipo de hallazgo**: Conformidad, Observación, NC Menor, NC Mayor, NC Crítica

El resultado y el tipo de hallazgo se eligen con **botones**, no con desplegables: las
opciones están a la vista y cada una lleva el color de su estado, que pasa al fondo al
seleccionarla. Así se ve de un vistazo en qué quedó cada requisito.
5. **Declaración de hallazgo sugerido**: requisito + evidencia objetiva + desviación

La aplicación llega hasta la declaración del hallazgo. La gestión de las acciones
correctivas —responsable, fecha compromiso, causa raíz, avance y cierre— se lleva en otra
plataforma, así que aquí no se registra.

### Eliminar una auditoría

En **Programa de auditorías**, el administrador tiene un botón **Eliminar** en cada fila,
y otro en la cabecera de la auditoría abierta. La confirmación indica cuántos registros de
requisitos se perderán antes de borrar. Al eliminar la auditoría caen con ella todas sus
respuestas.

El avance de cada fila usa siempre el tamaño de la lista de verificación vigente. Si la
lista crece —por ejemplo al expandir los requisitos transversales—, las auditorías
anteriores muestran el denominador actualizado en lugar del que tenían guardado.

### Guardar, modificar y eliminar un requisito

Cada requisito tiene su propia barra de acciones con el estado del registro:

| Estado | Qué muestra | Acciones |
|---|---|---|
| **Sin registrar** | Todavía no se le ha dado resultado | Guardar |
| **Pendiente de guardar** | Hay captura sin confirmar | Guardar · Cancelar · Eliminar |
| **Registrado** | Quién lo registró y cuándo | Modificar · Eliminar |

Una vez registrado, los campos quedan **bloqueados**: para cambiar la evidencia hay que
pulsar **Modificar**, y **Cancelar** descarta los cambios y recupera lo último guardado.
**Eliminar** borra todo lo registrado del requisito —evidencia, observaciones, resultado,
tipo de hallazgo y declaración— previa confirmación, y lo devuelve a pendiente.

El bloqueo es para no alterar por descuido una evidencia ya registrada. La aplicación
sigue guardando en segundo plano mientras se captura, de modo que nada se pierde si se
cierra el navegador antes de pulsar Guardar.

Además, cada requisito muestra los **documentos sugeridos** que conviene solicitar y, si
pertenece a un grupo de requisitos comunes, las cláusulas equivalentes de los otros marcos.

### Hallazgo sugerido automático

Cuando el auditor escribe en las observaciones una frase de incumplimiento —«no se
evidencia», «no cumple», «no se cuenta con», «sin registro», «no está documentado» y
otras—, la aplicación marca el resultado como **No Cumple**, lo clasifica como **No
Conformidad Menor** y redacta la declaración citando el requisito, las cláusulas
equivalentes, la evidencia objetiva y la desviación.

El texto se mantiene sincronizado mientras el auditor sigue capturando. En cuanto lo
edita a mano, deja de regenerarse y queda bajo su control; la columna `nc_autogenerada`
registra si el texto lo escribió el sistema o el auditor.

## Informes

Réplica de las nueve secciones del informe de auditoría de la organización: datos
generales, objetivo y metodología, resumen por marco normativo y por proceso, hallazgos
por tipo, no conformidades declaradas, desarrollo narrativo por proceso, conclusiones,
recomendaciones y firmas. Se puede generar el informe completo o el de un solo proceso,
e imprimir a PDF.

## Archivos

| Archivo | Descripción |
|---|---|
| `auditoria-sgi-v2.html` | **Versión en revisión.** Cuatro normas, lista completa de DISCA, requisitos comunes correlacionados, ingreso por proceso, listas de verificación configurables y hallazgo sugerido automático. Pendiente de aprobación para pasar a la raíz. |
| `index.html` | **Versión en producción.** Tres normas. Se sirve en la raíz del dominio. |
| `confirmado.html` | Página de aterrizaje de los correos de Supabase: confirma la cuenta, avisa si el enlace venció y permite pedir uno nuevo. |
| `auditoria-sgi.html` | Versión autónoma publicada como Artifact de Claude, con almacenamiento propio. Se conserva como respaldo. |

Ambas son un único archivo HTML sin proceso de compilación.

## Puesta en marcha (versión Supabase)

1. Sirva el archivo por HTTP (no lo abra con `file://`):

   ```bash
   npx serve .
   ```

   o despliéguelo en Vercel, Netlify, GitHub Pages o cualquier hosting estático.

2. Abra la aplicación y cree su cuenta desde **Crear cuenta**.
   El primer usuario registrado queda como **Administrador**.

3. Los demás auditores crean su propia cuenta; el administrador les asigna el rol
   definitivo desde la vista **Usuarios**.

### Roles

| Rol | Permisos |
|---|---|
| Administrador | Gestiona usuarios y roles, crea y **elimina** auditorías, configura y **restablece** las listas de verificación, registra hallazgos |
| Auditor líder | Crea auditorías, configura las listas de verificación y registra hallazgos |
| Auditor | Registra evidencia y hallazgos |
| Consulta | Solo lectura de listas de verificación e informes |

## Base de datos

Esquema en PostgreSQL (Supabase), con Row Level Security activo en las cuatro tablas:

| Tabla | Contenido |
|---|---|
| `perfiles` | Usuario, correo, rol y estado. Se crea automáticamente al registrarse |
| `auditorias` | Código, norma, empresa, sitio, alcance, equipo, fechas, estado y resumen |
| `respuestas` | Un registro por requisito auditado, con evidencia, hallazgo, declaración de NC y `nc_autogenerada` |
| `listas_config` | Una fila por norma: a qué procesos se audita cada requisito (`asignaciones`, mapa `baseId → [procesos]`) |

Reglas aplicadas:

- Solo usuarios **activos** acceden a auditorías y respuestas
- Solo **administrador** y **auditor líder** crean auditorías; solo el administrador las elimina
- Solo **administrador** y **auditor líder** configuran las listas de verificación; solo el
  administrador puede restablecer una norma a su asignación de origen
- El rol **consulta** no puede escribir
- Nadie puede auto-asignarse el rol de administrador
- `respuestas` está publicada en Realtime: los auditores ven los registros de sus
  compañeros al instante, sin sobrescribir el campo que estén editando

## Configuración

La URL del proyecto y la clave *publishable* de Supabase están al inicio del bloque
`<script>` de `index.html`:

```js
const SUPABASE_URL = "https://<proyecto>.supabase.co";
const SUPABASE_KEY = "sb_publishable_...";
```

La clave *publishable* está diseñada para viajar en el cliente: por sí sola no da acceso
a los datos, que quedan protegidos por las políticas RLS. Aun así, **se recomienda
mantener este repositorio privado**, ya que el esquema y las listas de verificación
reflejan información interna de la organización.

Si Supabase exige confirmación de correo y prefiere omitirla para uso interno,
desactive *Confirm email* en el panel: **Authentication → Sign In / Providers → Email**.

### Confirmación de correo

Las aplicaciones envían el enlace de confirmación a `confirmado.html`, resuelto de forma
relativa a la página, en lugar de depender del *Site URL* del proyecto. Para que Supabase
acepte ese destino hay que registrarlo en **Authentication → URL Configuration**:

| Campo | Valor |
|---|---|
| Site URL | `https://avgomezf-afk.github.io/auditoriainterna/` |
| Redirect URLs | `https://avgomezf-afk.github.io/auditoriainterna/**` |

Mientras el *Site URL* siga en `http://localhost:3000`, los correos apuntarán a localhost
y el enlace no abrirá nada en la máquina del usuario.

La página distingue tres situaciones: cuenta confirmada, enlace vencido o inválido —con la
opción de reenviar— y visita directa sin datos de confirmación.
