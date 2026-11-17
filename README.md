# Cuaderno de Gastos

Aplicación web de gestión de gastos personales. Funciona completamente en el navegador, sin backend ni base de datos: todos los datos se guardan en `localStorage`.

## Cómo ejecutarla

1. Descomprime el archivo ZIP.
2. Abre `index.html` con doble clic (o "Abrir con" tu navegador preferido: Chrome, Edge, Firefox).
3. No requiere instalación, servidor ni conexión a internet, salvo para cargar las tipografías (Google Fonts). Si no hay conexión, la app funciona igual con las tipografías de respaldo del sistema.

## Funcionalidades

- **Registro de movimientos**: ingresos y gastos con descripción, monto (CLP), fecha y categoría.
- **Edición**: haz clic en cualquier movimiento de la lista para cargarlo en el formulario y actualizarlo.
- **Eliminar**: botón "×" en cada fila.
- **Navegación mensual**: flechas para moverte entre meses; los totales y gráficos se recalculan automáticamente.
- **Resumen del mes**: ingresos, gastos y balance.
- **Presupuestos por categoría**: define un límite mensual por categoría (botón "Presupuestos"). Las barras de la categoría cambian de color según el consumo:
  - Verde: dentro del presupuesto (menos del 80%).
  - Ámbar: cerca del límite (80–100%).
  - Rojo: presupuesto superado.
- **Movimientos recurrentes**: marca un movimiento como recurrente y usa "Aplicar recurrentes del mes anterior" para duplicarlos automáticamente al mes en curso (evita duplicados si ya fueron aplicados).
- **Tendencia de 6 meses**: gráfico de barras con el balance (ingresos − gastos) de los últimos 6 meses.
- **Comparación con el mes anterior**: variación porcentual de ingresos y gastos respecto al mes previo, con flechas e indicadores de color.
- **Distribución de gastos (gráfico de dona)**: porcentaje que representa cada categoría dentro del gasto total del mes.
- **Meta de ahorro mensual**: define un monto objetivo de ahorro para el mes y sigue el progreso según el balance real.
- **Mayores gastos**: lista de los 5 movimientos de mayor monto del mes.
- **Perfil con RUT chileno**: guarda tu nombre y RUT con validación del dígito verificador (módulo 11) y formato automático (12.345.678-5).
- **Gastos deducibles**: marca un gasto como "con boleta/factura" y registra el N° de documento.
- **Resumen tributario (simulación local)**: lista anual de gastos con respaldo, con IVA estimado (19%) y totales; exportable a CSV o imprimible/PDF. **No se conecta al SII** ni envía datos a ningún servicio: es solo un reporte ordenado para tu declaración.
- **Calculadora de IVA (19%)**: desde un monto total o neto, calcula neto, IVA y total.
- **Resumen anual**: tabla mes a mes con ingresos, gastos y balance del año; haz clic en un mes para saltar a él.
- **Filtros y orden**: por categoría, tipo (ingreso/gasto), texto de búsqueda y orden (fecha o monto, ascendente/descendente).
- **Exportar CSV**: descarga los movimientos del mes visible en formato CSV (para abrir en Excel/Sheets).
- **Respaldo completo (JSON)**: exporta todos los movimientos y presupuestos a un archivo `.json`, e impórtalo después (por ejemplo, al cambiar de computador) desde "Importar respaldo".
- **Borrar mes**: elimina todos los movimientos del mes actualmente visible.
- **Tema claro/oscuro**: botón ◐ en el encabezado; respeta también la preferencia del sistema operativo.

## Estructura del proyecto

```
gastos-app/
├── index.html              Aplicación completa (HTML + CSS + JavaScript)
├── manifest.json            Manifiesto PWA (nombre, íconos, colores)
├── sw.js                     Service worker (funcionamiento sin conexión)
├── icons/                    Íconos de la app (192px, 512px, maskable)
├── package.json               Configuración de Capacitor (para generar el .apk)
├── capacitor.config.json      Configuración de Capacitor
├── COMO-GENERAR-APK.md        Instrucciones paso a paso para obtener el .apk
└── README.md                  Este documento
```

## App instalable (PWA)

Además de usarla como página web, `index.html` ahora es una **PWA**: si la abres desde Chrome en un celular Android (sirviéndola desde un hosting, no como archivo local) aparece la opción "Agregar a pantalla de inicio" / "Instalar app", y queda con ícono propio y funciona sin conexión gracias al service worker.

## Generar el .apk

Ver **`COMO-GENERAR-APK.md`** para las instrucciones completas (dos opciones: sin instalar nada usando PWABuilder, o con Android Studio usando el proyecto Capacitor ya configurado).

## Tecnologías

- HTML5, CSS3 y JavaScript vanilla (sin frameworks ni dependencias de build).
- Tipografías: Lora (encabezados), IBM Plex Mono (cifras) e Inter (texto), cargadas desde Google Fonts.
- Persistencia: `localStorage` del navegador (los datos son locales a cada navegador/dispositivo).

## Notas

- Los montos se muestran en pesos chilenos (CLP), sin decimales.
- Las categorías vienen predefinidas (Alimentación, Transporte, Vivienda, Salud, Educación, Entretenimiento, Ropa, Servicios, Ahorro, Otros); si necesitas cambiarlas, edita el arreglo `CATEGORIES` al inicio del `<script>` en `index.html`.
- Como no hay servidor, los datos no se sincronizan entre dispositivos; usa el respaldo JSON para moverlos manualmente.
