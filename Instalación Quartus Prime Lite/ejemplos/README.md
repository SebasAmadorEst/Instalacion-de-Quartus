# Prueba mínima: compuerta AND

[← Inicio](../README.md)

Archivo: [`compuerta_and/and_gate.vhd`](compuerta_and/and_gate.vhd).

## Tabla de verdad

| a | b | y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

## Pasos

1. En Quartus abre **File → New Project Wizard**.
2. Elige carpeta y nombre `and_gate`; establece `and_gate` como entidad superior.
3. Agrega el archivo VHDL al proyecto.
4. Selecciona un dispositivo disponible e instalado, adecuado para tu placa o curso.
5. Ejecuta **Processing → Start → Start Analysis & Synthesis**.
6. Comprueba que la tarea finalice sin errores y revisa el informe de síntesis.
7. Opcional: ejecuta **Start Compilation** con un dispositivo válido y sus paquetes instalados.

**Atención:** síntesis no equivale a simulación de la tabla de verdad. Para observar formas de onda se necesita un simulador configurado (por ejemplo Questa) y un banco de pruebas. Para comprobar físicamente la salida se requiere placa, asignación de pines y programación.
