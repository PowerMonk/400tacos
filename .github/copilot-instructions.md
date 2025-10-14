# 400tacos - Instrucciones para GitHub Copilot

## Contexto del Proyecto

Este es un sitio web para organizar un convivio de tacos llamado "400tacos". Es un proyecto simple hecho con **Astro** y **TailwindCSS**.

## Propósito

- Organizar la compra de 400 tacos para toda la clase
- Cada taco cuesta $10 pesos
- Los estudiantes pagan por sus tacos (cantidad exacta)
- Los profesores cooperan con montos variables (sin cantidad fija)
- El objetivo total es recaudar $4,000 pesos

## Estructura del Proyecto

```
src/
├── components/
│   ├── ProgressBar.astro       # Barra de progreso del dinero recaudado
│   ├── ParticipanteCard.astro  # Tarjeta individual de cada participante
│   └── StatCard.astro          # Tarjetas de estadísticas generales
├── data/
│   └── participantes.json      # Base de datos de participantes
├── pages/
│   └── index.astro            # Página principal
└── styles/
    └── global.css             # Estilos globales
```

## Datos de Participantes

El archivo `src/data/participantes.json` contiene:

- **Estudiantes**: tienen `tacos`, `debe`, `pagado`, `pagoCompleto`
- **Profesores**: tienen `cooperacion`, `pagado`, `pagoCompleto` (sin monto fijo)

### Estructura de Participante:

```json
{
  "id": number,
  "nombre": string,
  "tipo": "estudiante" | "profesor",
  "tacos"?: number,          // Solo estudiantes
  "debe": number,
  "pagado": number,
  "pagoCompleto": boolean,
  "cooperacion"?: number     // Solo profesores
}
```

## Funcionalidades Implementadas

1. **Banner principal** con título y descripción
2. **Barra de progreso** visual del dinero recaudado
3. **Grid de participantes** con tarjetas individuales
4. **Búsqueda en tiempo real** de participantes
5. **Estadísticas** resumidas (total participantes, pagos completos, faltante)
6. **Diseño responsivo** con TailwindCSS

## Reglas para Modificaciones

### Al agregar nuevos participantes:

- Asignar ID único incrementalmente
- Especificar el `tipo` correctamente
- Para estudiantes: calcular `debe = tacos * 10`
- Para profesores: solo `cooperacion` y `pagado`

### Al actualizar pagos:

- Modificar el campo `pagado`
- Actualizar `pagoCompleto` si `pagado >= debe`
- Para profesores, `pagoCompleto = true` cuando confirmen su cooperación

### Colores y Estilos:

- **Verde**: pagos completos, progreso positivo
- **Naranja/Rojo**: tema principal (tacos)
- **Gris**: información neutral
- **Rojo**: faltantes o pendientes

### Componentes Reutilizables:

- `ProgressBar`: para mostrar cualquier progreso
- `ParticipanteCard`: adaptable a estudiantes y profesores
- `StatCard`: para mostrar cualquier estadística numérica

## Consideraciones Técnicas

- **Framework**: Astro 5.x con TailwindCSS 4.x
- **Datos**: JSON estático (se actualiza manualmente)
- **Búsqueda**: JavaScript vanilla en el cliente
- **Responsivo**: Mobile-first con breakpoints de Tailwind
- **Iconos**: Emojis y SVGs inline para simplicidad

## Comandos Útiles

- `pnpm dev`: Servidor de desarrollo
- `pnpm build`: Build de producción
- `pnpm preview`: Preview del build

---

**Nota**: Este es un proyecto simple sin backend. Todos los datos se manejan estáticamente en el JSON y se actualizan manualmente cuando hay nuevos pagos o participantes.
