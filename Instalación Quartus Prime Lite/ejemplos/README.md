
---

## Configuración del archivo .qsf

Durante la compilación, Quartus Prime Lite puede mostrar la siguiente advertencia:

```text
Warning (18236): Number of processors has not been specified
which may cause overloading on shared machines.
```

Esta advertencia aparece porque no se ha especificado cuántos procesadores lógicos puede utilizar Quartus.

### Solución

**1. Localizar el archivo de configuración**

Abre una terminal en Ubuntu y ejecuta:

```bash
find "$HOME" -type f -name "and_gate.qsf" 2>/dev/null
```

El archivo `.qsf` se genera automáticamente al crear el proyecto y contiene sus configuraciones.

**2. Abrir el archivo**

Utiliza Nano, reemplazando la ruta por la ubicación real de tu proyecto:

```bash
nano ~/Descargas/compuerta_and/and_gate.qsf
```

**3. Agregar la configuración**

Al final del archivo, agrega:

```tcl
set_global_assignment -name NUM_PARALLEL_PROCESSORS 4
```

Esta instrucción establece un máximo de cuatro procesadores lógicos para la compilación.

El número puede modificarse dependiendo de los recursos del equipo.

**Importante:** no elimines las demás líneas del archivo `.qsf`.

**4. Guardar los cambios**

En Nano:

1. Presiona `Ctrl + O`.
2. Presiona `Enter`.
3. Presiona `Ctrl + X`.

**5. Volver a compilar**

Regresa a Quartus y ejecuta:

**Processing → Start → Start Analysis & Synthesis**

La advertencia `18236` debería desaparecer.

---

## Compilación completa del proyecto

Después de comprobar que el análisis y la síntesis funcionan correctamente, podemos ejecutar una compilación completa.

### Procedimiento

1. Abre el proyecto `and_gate` en Quartus.
2. Selecciona **Processing → Start Compilation**.
3. Espera a que finalicen las etapas del proceso.
4. Comprueba los resultados en el panel **Tasks**.

Las etapas principales son:

| Etapa | Función |
|---|---|
| Analysis & Synthesis | Analiza el VHDL y genera la lógica del circuito. |
| Fitter (Place & Route) | Distribuye y conecta los recursos dentro de la FPGA. |
| Assembler | Genera el archivo de programación del dispositivo. |
| Timing Analysis | Analiza los tiempos del diseño. |
| EDA Netlist Writer | Genera archivos para herramientas externas de diseño o simulación. |

### Resultado obtenido

Durante las pruebas realizadas con **Quartus Prime Lite Edition 25.1 en Ubuntu**, el proyecto `and_gate` completó las etapas de compilación correctamente.

El panel de tareas mostró marcas verdes en las etapas principales.

Esto permite comprobar que Quartus puede procesar el diseño VHDL y generar los resultados de implementación para el dispositivo seleccionado.

### Advertencias adicionales

Durante la compilación pueden aparecer advertencias como:

**Warning (292013) — LogicLock**

Indica que la funcionalidad LogicLock requiere una licencia de suscripción.

No es necesario adquirirla para desarrollar y compilar este ejemplo en Quartus Prime Lite.

**Warning (15714) — Incomplete I/O Assignments**

Indica que algunos pines no tienen asignaciones completas.

Para implementar el circuito en una FPGA física es necesario configurar los pines y estándares eléctricos correspondientes a la placa.

Estas advertencias no necesariamente impiden que la compilación finalice correctamente.

---

## Visualización gráfica del circuito con RTL Viewer

Quartus Prime Lite incluye una herramienta llamada **RTL Viewer**, que permite visualizar gráficamente la estructura lógica generada a partir del código VHDL.

Esto resulta útil para comprobar que el programa interpretó correctamente nuestro diseño.

### ¿Cómo abrir RTL Viewer?

**1.** Abre el proyecto `and_gate` en Quartus Prime Lite.

**2.** Comprueba que el análisis y la síntesis hayan finalizado correctamente.

**3.** En la barra superior, selecciona:

**Tools → Netlist Viewers → RTL Viewer**

**4.** Se abrirá una ventana con el diagrama lógico del circuito.

### Resultado esperado

Para nuestro archivo `and_gate.vhd`, RTL Viewer muestra:

- Entrada `a`.
- Entrada `b`.
- Una compuerta lógica AND.
- Salida `y`.

La operación representada es:

```text
y = a AND b
```

El diagrama confirma que Quartus interpretó el código VHDL como una compuerta AND de dos entradas y una salida.

### ¿Se pueden modificar las entradas desde RTL Viewer?

No. RTL Viewer es una herramienta de visualización estructural, no un simulador interactivo.

Para introducir valores de entrada y observar cómo cambia la salida durante el tiempo, se necesita una herramienta de simulación compatible, como Questa-Altera FPGA Starter Edition.

La simulación no es necesaria para esta prueba básica de instalación.

---

## Conclusión de la prueba

Se comprobó el funcionamiento de **Quartus Prime Lite Edition 25.1 en Ubuntu** mediante el desarrollo y la compilación de una compuerta AND en VHDL.

Las pruebas permitieron verificar que:

- Quartus Prime Lite se ejecuta correctamente.
- El programa reconoce el código VHDL.
- El análisis y la síntesis finalizan sin errores.
- La configuración del archivo `.qsf` permite controlar los procesadores utilizados.
- Las etapas de compilación completa se ejecutan correctamente.
- RTL Viewer representa gráficamente el circuito diseñado.

**Resultado final:** la instalación y configuración de Quartus Prime Lite Edition 25.1 se verificó satisfactoriamente mediante un proyecto funcional de lógica digital.

No fue necesario disponer de una FPGA física para realizar estas comprobaciones.
