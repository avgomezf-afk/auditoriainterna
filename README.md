# Auditoría SGI — Sistema de auditorías internas

Aplicación web para ejecutar auditorías internas de sistemas de gestión, registrar la
evidencia objetiva de cada requisito y generar los informes por proceso.

## Normas incluidas

| Norma | Requisitos | Procesos |
|---|---:|---:|
| ISO 9001:2015 — Sistema de Gestión de la Calidad | 44 | 8 |
| FSSC 22000 v6 — Producción de empaques (Categoría I) | 197 | 13 |
| FSSC 22000 v6 — Almacenamiento y distribución (Categoría G) | 49 | 9 |

La lista de FSSC 22000 para empaques reproduce íntegramente la lista de verificación
integrada de la organización: **ISO 22000:2018** (69 requisitos) + **INTE/ISO/TS
22002-4:2014** (64) + **FSSC 22000 v6, requisitos adicionales de la sección 2.5** (64),
con los mismos procesos y asignaciones utilizados en la auditoría interna.

## Qué registra cada requisito

- **Resultado**: Cumple / Cumple Parcialmente / No Cumple / No Aplica / Pendiente
- **Tipo de hallazgo**: Conformidad, Observación, NC Menor, NC Mayor, NC Crítica
- **Evidencia objetiva**: documento, registro, código y versión o referencia observada
- **Hallazgo / observación**: la desviación o situación encontrada
- **Declaración de no conformidad**: requisito + evidencia + desviación, con redacción
  automática, responsable de la acción y fecha compromiso
- **Documentos sugeridos**: cada requisito muestra la información que conviene solicitar

## Informes

Réplica de las nueve secciones del informe de auditoría de la organización: datos
generales, objetivo y metodología, resumen por marco normativo y por proceso, hallazgos
por tipo, no conformidades declaradas, desarrollo narrativo por proceso, conclusiones,
recomendaciones y firmas. Se puede generar el informe completo o el de un solo proceso,
e imprimir a PDF.

## Archivos

| Archivo | Descripción |
|---|---|
| `auditoria-sgi-supabase.html` | **Versión principal.** App web conectada a Supabase: autenticación real, RLS y sincronización en vivo entre auditores. |
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
| Administrador | Gestiona usuarios y roles, crea y elimina auditorías, registra hallazgos |
| Auditor líder | Crea auditorías y registra hallazgos |
| Auditor | Registra evidencia y hallazgos |
| Consulta | Solo lectura de listas de verificación e informes |

## Base de datos

Esquema en PostgreSQL (Supabase), con Row Level Security activo en las tres tablas:

| Tabla | Contenido |
|---|---|
| `perfiles` | Usuario, correo, rol y estado. Se crea automáticamente al registrarse |
| `auditorias` | Código, norma, empresa, sitio, alcance, equipo, fechas, estado y resumen |
| `respuestas` | Un registro por requisito auditado, con evidencia, hallazgo y declaración de NC |

Reglas aplicadas:

- Solo usuarios **activos** acceden a auditorías y respuestas
- Solo **administrador** y **auditor líder** crean auditorías; solo el administrador las elimina
- El rol **consulta** no puede escribir
- Nadie puede auto-asignarse el rol de administrador
- `respuestas` está publicada en Realtime: los auditores ven los registros de sus
  compañeros al instante, sin sobrescribir el campo que estén editando

## Configuración

La URL del proyecto y la clave *publishable* de Supabase están al inicio del bloque
`<script>` de `auditoria-sgi-supabase.html`:

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
