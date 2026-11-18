# Prompt para Claude Code: reporte imprimible del laboratorio

> Ya quedó implementado en el laboratorio (botón «Ver reporte para imprimir» en la sección 15, Exportar). Este archivo queda como referencia por si se quiere rehacer o ajustar.

Copia todo lo que está debajo de la línea y pégalo en Claude Code, abierto en la carpeta del repo (`Downloads\expo`).

---

En esta carpeta están `index.html` (presentación de 33 láminas) y `Laboratorio_Perceptron_Simple.html` (una app que recibe una base de datos y aplica todo el proceso del perceptrón). Además, la lámina 33 del index lleva ese mismo laboratorio embebido en base64, dentro de `<script id="laboratorio-b64" type="text/plain">`.

Quiero que, en el laboratorio, el reporte salga como un documento bonito y bien organizado, listo para imprimir o guardar como PDF, en blanco y negro y con tablas. Lee primero el laboratorio completo, sobre todo la sección «15 Exportar» y las funciones `reporte()`, `textoGerencia()`, `resumenCV()`, `datosDuda()`, `csvPred()` y la variable `R`.

## Qué cambiar

1. En la sección «Exportar», agrega un botón principal **«Ver reporte para imprimir»**. Deja los botones que ya existen («Copiar reporte», descargas).
2. Al pulsarlo, se abre el documento del reporte en una ventana nueva (`window.open`) o, si el navegador la bloquea, dentro de la misma página en una capa a pantalla completa con un botón «Cerrar». El documento tiene arriba dos botones que no salen al imprimir: «Imprimir o guardar como PDF» (llama a `print()`) y «Cerrar».
3. El documento se arma con los MISMOS datos que ya calcula la app (`R`, `S`, `textoGerencia()`, etc.). No recalcules nada ni cambies cifras: el reporte debe decir exactamente lo mismo que la página.

## Contenido del documento, en este orden

1. **Portada corta**: título «Reporte del Perceptrón Simple», nombre del archivo de datos, columna objetivo, clase positiva y negativa, fecha de hoy y la línea «Grupo 4, Inteligencia de Negocios». Si la corrida es igual a la del Colab, una nota en recuadro: «Igual que el Colab: misma partición, escalado y entrenamiento de scikit-learn».
2. **Resumen en una mirada**: una fila de 4 cajas con Accuracy, Precision, Recall y F1-score (número grande), y debajo una línea con VN, FP, FN, VP y épocas.
3. **Diccionario de datos**: tabla con Variable, Tipo, Rol, Valores, Media, Vacíos y Descripción.
4. **Partición**: tabla con registros usados, entrenamiento y prueba, cada uno con cuántos hay de cada clase.
5. **Entrenamiento**: η, épocas, motivo de parada y una tabla compacta de errores por época (en varias columnas si son muchas).
6. **Modelo**: la ecuación completa en letra monoespaciada y una tabla de pesos ordenada por tamaño (Variable, Peso, Hacia qué clase empuja). Debajo, la tabla de estandarización (media, desviación, mediana).
7. **Matriz de confusión**: tabla de 2 × 2 con encabezados «Dijo …» / «Era …», con VN, FP, FN y VP.
8. **Métricas**: tabla con Métrica, Valor y Cálculo (por ejemplo «121 / 122»), y la línea base del modelo que siempre dice la clase mayoritaria.
9. **Validación cruzada**: tabla por pliegue (Accuracy, Precision, Recall, F1, Épocas) con filas finales de Promedio, Mínimo y Máximo en negrita.
10. **Zona de duda**: umbral, cuántos registros irían a revisión manual y cuántos errores caen ahí.
11. **Lectura para la gerencia**: las cinco preguntas, cada una con Evidencia, Interpretación y Conclusión.
12. **Pie**: «Generado con el Laboratorio del Perceptrón Simple. Todo se calculó en el navegador.»

## Diseño

- Solo blanco, negro y grises. Sin colores, ni siquiera en el tema «Luz UV»: el reporte siempre sale en blanco y negro.
- Tipografía: títulos con serif (la misma familia Bodoni de la app, con Georgia de respaldo) y texto con una sans legible; números en tabla con cifras de ancho fijo (`font-variant-numeric: tabular-nums`) y alineados a la derecha.
- Tablas sobrias: borde fino gris, encabezado con fondo gris muy claro y texto en negrita, filas con rayado muy suave, sin bordes verticales gruesos.
- Secciones numeradas con títulos claros y una línea fina debajo de cada título.
- Números con coma decimal y punto de miles, como en la app (usa sus funciones `fmt`, `pct` y `ent`).
- Para imprimir: tamaño carta, márgenes de unos 18 mm, `@page` con número de página abajo si el navegador lo soporta, ninguna tabla ni caja partida a la mitad entre páginas (`break-inside: avoid`), y cada sección grande que empiece donde quepa completa.
- Todo en el mismo archivo, sin librerías nuevas ni imágenes externas. Debe funcionar sin internet (si la fuente no carga, que se vea bien con la de respaldo).

## Reglas

- No cambies cómo calcula la app ni ningún otro texto o sección del laboratorio.
- Después de modificar `Laboratorio_Perceptron_Simple.html`, vuelve a generar su base64 y reemplaza el contenido del bloque `<script id="laboratorio-b64" type="text/plain">` en `index.html`, para que la lámina 33 use la versión nueva. No toques nada más del index.

## Al terminar

- Abre el laboratorio, pulsa «Usar la base de billetes» y «Entrenar el perceptrón», y genera el reporte. Comprueba que salga con 98,55 % de accuracy, VN 150, FP 3, FN 1, VP 121, 9 épocas y la nota «Igual que el Colab».
- Haz lo mismo con «Probar con soportes de pago» y con un CSV propio.
- Revisa la vista de impresión (o un PDF de prueba): que no haya tablas cortadas ni colores, y que se lea bien.
- Comprueba que la lámina 33 del index muestre la versión nueva y que no haya errores en la consola.
- Sube los cambios a git con un commit que explique qué cambió.
