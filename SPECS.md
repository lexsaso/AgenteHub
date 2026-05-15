# AgentHub Admin Dashboard - Especificacion Completa (v1.0)

## 1) Proposito del proyecto
Construir un dashboard administrativo web para operar un catalogo de agentes de IA en entorno empresarial.

El resultado final debe ser una interfaz usable en desktop y mobile, visualmente consistente, con informacion hardcodeada realista y comportamiento interactivo funcional sin backend.

## 2) Alcance

### En alcance
- Una SPA administrativa montada en `index.html`.
- Navegacion por secciones sin recargar pagina.
- Soporte de tema claro/oscuro con persistencia en `localStorage`.
- Componentes interactivos: tablas, dropdowns de acciones, acordeones, modal, menu mobile.
- Datos estaticos coherentes para usuarios, agentes, skills, contrataciones y errores.

### Fuera de alcance
- Integracion con APIs reales o base de datos.
- Autenticacion/autorizacion real.
- CRUD persistente en servidor.
- Checkout ecommerce y flujo de compra (archivos `catalogo.html`, `producto.html`, `carrito.html`, `checkout.html` se consideran legacy y no son objetivo de esta entrega).

## 3) Resultado final esperado
Un dashboard administrativo de una sola pagina, con navegacion lateral en desktop y menu alterno en mobile, que permita al usuario:

1. Ver metricas de estado general.
2. Consultar informacion de usuarios y agentes.
3. Expandir detalle de skills por agente y de catalogo de skills.
4. Revisar contrataciones activas y en riesgo.
5. Revisar log de errores con severidad.
6. Ejecutar acciones de interfaz (abrir/cerrar dropdown, modal, acordeones, menu mobile) sin fallos visuales.

## 4) Requerimientos funcionales detallados

### RF-01 Navegacion por secciones
- Deben existir exactamente estas secciones: `dashboard`, `usuarios`, `agentes`, `skills`, `contratos`, `errores`.
- Solo una seccion visible a la vez.
- Al cambiar de seccion debe actualizarse el titulo del header.
- En desktop, el item activo del sidebar debe reflejar estado visual seleccionado.

### RF-02 Layout responsive
- Desktop (`>=768px`): sidebar fijo visible + contenido principal.
- Mobile (`<768px`): sidebar oculto, boton `Menu` visible y panel mobile desplegable.
- El menu mobile debe cerrarse al seleccionar una seccion.

### RF-03 Dashboard KPI
- Mostrar 4 tarjetas KPI con datos hardcodeados:
	- Ingresos Totales
	- Perdida por Descuentos
	- Agentes Activos
	- Agentes Fallando
- Incluir un bloque de grafico placeholder con copy explicativo.

### RF-04 Tabla de usuarios
- Tabla con columnas: Nombre, Email, Plan, Estado, Acciones.
- Minimo 5 filas.
- Al menos una fila debe tener menu de acciones (`Ver detalle`, `Eliminar`).
- El boton `Ver detalle` abre modal informativo.

### RF-05 Tabla de agentes
- Tabla con columnas: Agente, Tipo, Version, Estado, Uso 24h, Skills.
- Minimo 4 agentes.
- Columna Skills con boton `Expandir` que despliega texto de habilidades por fila.

### RF-06 Catalogo de skills
- Lista de al menos 4 skills en formato acordeon.
- Cada item debe expandir/colapsar descripcion al click.

### RF-07 Contrataciones
- Tabla con columnas: Cliente, Agente asignado, Inicio, Monto, Estado.
- Minimo 4 contratos con estados variados (`Vigente`, `Renovacion`, `En riesgo`).

### RF-08 Log de errores
- Tabla con columnas: Fecha, Agente, Codigo, Descripcion, Severidad.
- Minimo 6 registros.
- Debe haber mas de un nivel de severidad (Baja/Media/Alta/Critica).

### RF-09 Tema claro/oscuro
- Boton de tema visible en header.
- Persistencia en `localStorage` usando clave `theme`.
- Respetar preferencia del sistema cuando no exista preferencia guardada.

### RF-10 Dropdowns y modal
- Dropdown de acciones se abre/cierra por boton.
- Clic fuera del dropdown lo cierra.
- Modal debe bloquear scroll del body al abrir y restaurarlo al cerrar.
- Clic sobre backdrop debe cerrar modal.

## 5) Requerimientos no funcionales

### RNF-01 Tecnologia
- HTML + Tailwind CDN + JavaScript vanilla.
- No frameworks JS adicionales.

### RNF-02 Accesibilidad minima
- Controles interactivos implementados con `button` cuando aplique.
- Texto legible en ambos temas.
- `aria-label` en controles iconicos (ej: toggle de tema).

### RNF-03 Rendimiento y carga
- Primera carga funcional sin dependencia de build step.
- Evitar scripts pesados innecesarios.
- Sin errores JS en consola al navegar secciones y abrir/cerrar componentes.

### RNF-04 Consistencia visual
- Espaciados y tipografias coherentes entre secciones.
- Estados de hover/focus visibles en elementos accionables.
- Tablas con `overflow-x-auto` para no romper layout en pantallas estrechas.

## 6) Estructura de datos (mock)

### Usuarios
- Campos: `nombre`, `email`, `plan`, `estado`.

### Agentes
- Campos: `nombre`, `tipo`, `version`, `estado`, `uso24h`, `skills`.

### Contratos
- Campos: `cliente`, `agenteAsignado`, `fechaInicio`, `monto`, `estado`.

### Errores
- Campos: `fecha`, `agente`, `codigo`, `descripcion`, `severidad`.

## 7) Interacciones obligatorias (DoD de UX)
Se considera incompleta la entrega si falla cualquiera de estos puntos:

1. Cambio de seccion con update de titulo y estado activo.
2. Toggle tema claro/oscuro con persistencia tras recargar.
3. Apertura/cierre de al menos un dropdown y cierre por clic externo.
4. Apertura/cierre de modal y control de scroll del body.
5. Acordeones de skills funcionales.
6. Menu mobile funcional en viewport pequeno.

## 8) Criterios de aceptacion verificables

### CA-01 Integridad de contenido
- Existen todas las secciones definidas en RF-01 y son accesibles desde navegacion.

### CA-02 Comportamiento
- No hay estados rotos: no quedan dos secciones visibles simultaneamente.
- No quedan dropdowns abiertos accidentalmente al hacer clic fuera.

### CA-03 Responsive
- En 375px de ancho no hay desbordes horizontales globales.
- En 1280px la navegacion lateral se mantiene estable y util.

### CA-04 Calidad visual
- Contraste suficiente para texto principal y badges.
- Jerarquia clara: header > contenido > tablas > acciones.

### CA-05 Estabilidad
- Sin errores en consola durante flujo manual completo:
	- abrir pagina
	- cambiar entre 6 secciones
	- abrir dropdown
	- abrir/cerrar modal
	- alternar tema 2 veces

## 9) Restricciones de implementacion
- Mantener solucion en un solo archivo principal (`index.html`) para esta version.
- Se permite CSS embebido minimo para componentes no triviales (ej: acordeon con `max-height`).
- Datos deben permanecer hardcodeados y legibles (no ofuscados).

## 10) Entregables obligatorios
1. `index.html` funcional y navegable.
2. `SPECS.md` actualizado (este documento).
3. Codigo limpio, sin funciones huerfanas y sin errores de sintaxis.

## 11) Plan de implementacion recomendado
1. Definir layout base y navegacion.
2. Implementar secciones con datos mock.
3. Conectar interacciones JS (navegacion, acordeones, dropdown, modal, menu mobile).
4. Implementar tema y persistencia.
5. Validar responsive y flujo manual de aceptacion.

## 12) Definicion de terminado (Definition of Done)
Una entrega se considera terminada solo si:

1. Cumple 100% de RF-01 a RF-10.
2. Cumple RNF-01 a RNF-04.
3. Pasa todos los criterios CA-01 a CA-05.
4. No depende de aclaraciones posteriores para entender que se construyo y como validarlo.

---

## 13) Nota para agentes de codificacion
No iterar sobre supuestos ambiguos.

Antes de cambiar codigo, validar siempre contra esta especificacion:
- Si una decision no esta en el documento, proponerla explicitamente antes de implementarla.
- Si el cambio no mejora un RF/RNF/CA concreto, no implementarlo.
- Priorizar cumplimiento funcional verificable sobre cambios cosmeticos.

## 14) Roadmap de ejecucion por versiones (v2)
Este roadmap define como implementar o mejorar el dashboard sin derrochar tokens ni abrir iteraciones difusas.

Cada iteracion debe tener:
- Objetivo cerrado.
- Lista de cambios permitidos.
- Criterios de salida verificables.
- Evidencia de validacion.

### 14.1 MVP (Sprint 1)

#### Objetivo
Entregar una base administrativa totalmente navegable, responsive y estable, con interacciones primarias funcionando de punta a punta.

#### Incluye
- RF-01, RF-02, RF-03, RF-04, RF-05, RF-06, RF-09, RF-10.
- RNF-01, RNF-03.

#### Excluye
- Ajustes finos de accesibilidad avanzada.
- Mejoras cosmeticas no vinculadas a RF/RNF.
- Refactors de estilo que no cambien comportamiento.

#### Criterios de salida MVP
1. Navegacion entre todas las secciones sin recarga y sin errores.
2. Tema claro/oscuro persistente tras refresh.
3. Modal y dropdown cerrando correctamente por clic externo.
4. Menu mobile funcional en ancho 375px.
5. Flujo de prueba manual completo sin errores en consola.

#### Evidencia minima requerida
- Captura o registro de prueba manual de los 5 puntos anteriores.
- Lista de RF cumplidos con check explicito.

### 14.2 v1.1 (Sprint 2)

#### Objetivo
Consolidar calidad de datos operativos y robustecer tablas de contratos y errores para uso de monitoreo diario.

#### Incluye
- RF-07 y RF-08 completos.
- RNF-04 completo.
- Verificacion de CA-01 a CA-03.

#### Cambios permitidos
- Ajustar estructura visual de tablas para legibilidad.
- Normalizar etiquetas/estados y consistencia semantica de badges.
- Mejorar textos de vacio/placeholders si aplica.

#### Criterios de salida v1.1
1. Contratos con al menos 4 filas y estados variados.
2. Log de errores con al menos 6 filas y severidades multiples.
3. Sin desbordes horizontales globales en 375px.
4. Tablas legibles y operables en 1280px.

#### Evidencia minima requerida
- Checklist de CA-01, CA-02 y CA-03 con resultado `PASS/FAIL`.

### 14.3 v1.2 (Sprint 3)

#### Objetivo
Cerrar la version lista para demo ejecutiva: accesibilidad minima completa, consistencia visual y definicion de terminado al 100%.

#### Incluye
- RNF-02 completo.
- Validacion final de CA-04 y CA-05.
- Limpieza final de codigo y funciones no usadas.

#### Cambios permitidos
- Mejoras de contraste y foco visibles.
- Ajustes de copy y microinteracciones si impactan usabilidad.
- Correcciones menores de estructura HTML para semantica.

#### Criterios de salida v1.2
1. Todos los RF y RNF en estado cumplido.
2. Criterios CA-01 a CA-05 en `PASS`.
3. Flujo de demo sin errores funcionales ni bloqueos visuales.

#### Evidencia minima requerida
- Matriz final RF/RNF/CA con estado y nota breve de verificacion.

## 15) Regla de eficiencia para agentes (anti-desperdicio de tokens)

### Protocolo obligatorio antes de codificar
1. Citar que RF/RNF/CA cubrira el cambio solicitado.
2. Definir impacto exacto: archivos, secciones y funciones.
3. Si no existe criterio de aceptacion, no ejecutar; primero proponer criterio y confirmar.

### Protocolo obligatorio despues de codificar
1. Reportar que RF/RNF/CA quedaron cubiertos.
2. Reportar pruebas ejecutadas y resultado.
3. Reportar riesgos residuales (si existen) en maximo 3 lineas.

### Condiciones de bloqueo (no continuar)
- Requisito contradictorio con el alcance de esta version.
- Cambio pedido sin criterio verificable.
- Solicitud de refactor masivo sin beneficio funcional medible.

## 16) Plantilla de tarea para futuras iteraciones
Usar esta plantilla en cada nueva peticion para mantener eficiencia:

1. Objetivo de negocio (1-2 lineas).
2. RF/RNF/CA impactados.
3. Archivos a tocar.
4. Criterio de aceptacion puntual.
5. Prueba manual minima esperada.
6. Definicion de terminado de la iteracion.

## 17) Criterio de aprobacion final del proyecto
El proyecto se aprueba unicamente cuando:

1. Se completa MVP, v1.1 y v1.2 con evidencia.
2. No hay criterios CA en estado `FAIL`.
3. No hay dependencias abiertas de aclaracion funcional.
4. El documento `SPECS.md` permite ejecutar el trabajo sin preguntas de alcance basico.
