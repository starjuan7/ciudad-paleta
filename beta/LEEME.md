# Ciudad Paleta · Plazas independientes + esquemas editables (versión de prueba)

Esta carpeta (`/beta`) contiene la versión nueva **sin tocar** la actual (`/index.html`).
Mientras no hagas el cambio final, tu sistema de hoy sigue funcionando igual con los datos de siempre.

## Qué cambia
- **Puebla y Acapulco quedan totalmente separadas**: sabores y precios, inventario, pedidos, clientes, historial y bitácora. Todo vive en `plazas/puebla/...` y `plazas/acapulco/...`.
- **Esquemas de mayoreo editables** (pestaña ⚙️ Esquemas, solo administrador): cambiar mínimos, agregar o quitar esquemas, por plaza. Los pedidos ya hechos no cambian.
- **Control de existencias** al tomar pedidos: se puede activar/desactivar por plaza (hoy Puebla sí y Acapulco no, igual que antes).
- El formulario de sabor pide un precio por cada esquema de la plaza.
- Guardado seguro: ya no se reescriben colecciones completas; solo se guarda lo que cambió, y se cancela si algo intentara borrar muchos registros de golpe.
- "Eliminar todo el inventario" ahora pide **tu contraseña de acceso** (antes había una contraseña escrita en el código).
- Arreglado: "🗑 Limpiar" stock de un sabor (antes marcaba error).

## Qué NO cambia / queda pendiente
- `recetas.html` y `usuarios.html` siguen igual y comparten los mismos datos de siempre.
- Portal de clientes (ciudadpaleta.mx) y puntos: no se tocaron. Los pedidos que lleguen del portal seguirán escribiéndose en el lugar antiguo y **no aparecerán** en esta versión hasta que se conecte el portal (se hará después).

## Pasos
1. **Reglas de seguridad**: agrega el bloque de `firebase-rules-plazas.json` dentro de `"rules"` (junto a lo que ya tienes) y publica.
2. **Respaldo**: Firebase → Realtime Database → ⋮ → Exportar JSON.
3. **Probar la copia**: abre `/beta/migrar.html` → Analizar → Descargar respaldo → Copiar → Verificar. Luego usa `/beta/` para revisar. Lo que hagas en `/beta/` solo afecta la copia.
4. **Cambio final** (fuera de horario de pedidos): en `/beta/migrar.html` elimina la copia de prueba y vuelve a copiar para traer los datos más recientes; verifica; entonces se publica la nueva versión como `index.html` (la actual queda como `index-anterior.html`). Después recarga el sistema en todos los dispositivos.
5. **Volver atrás** si algo no convence: restaurar `index-anterior.html` como `index.html`. Los datos originales siguen intactos; solo los registros hechos después del cambio quedan en `plazas/`.

## Reglas del reparto de datos
- Inventarios: ya estaban separados (`inv_puebla`, `inv_acapulco`).
- Pedidos: por su campo plaza (los que no tengan, a Puebla, y se avisa).
- Clientes: a la plaza donde tienen pedidos; en las dos si tienen en ambas; los que no tienen pedidos, a las dos (se limpian después).
- Sabores: ambas plazas reciben el catálogo con sus propios precios (Puebla p1–p3, Acapulco a1–a2).
- Historial de inventario y bitácora: a la plaza de su pedido o de su campo plaza; el resto se copia a las dos.
- Esquemas iniciales idénticos a los de hoy: Puebla 30/100/200, Acapulco 50/200.
