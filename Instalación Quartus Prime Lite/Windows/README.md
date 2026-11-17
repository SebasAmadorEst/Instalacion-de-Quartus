# 🪟 Instalación de Quartus Prime Lite Edition 25.1 en Windows

[← Volver al inicio](../README.md) · [Ver guía de Linux](../Linux/README.md)

> **Alcance:** Windows 10 y Windows 11 de 64 bits, según la matriz oficial de compatibilidad de Lite 25.1. Esta guía describe un procedimiento documentado; las pantallas deben verificarse en un equipo Windows antes de afirmar que se ejecutaron personalmente.

## 1. Requisitos previos

- Equipo Windows compatible, cuenta con permisos de administrador y conexión a Internet.
- Espacio suficiente para descargar, extraer e instalar los componentes. Como referencia, Altera indica **31,37 GB** para el paquete completo de Windows 25.1, incluyendo archivo comprimido, extracción e instalación; deja margen adicional para proyectos.
- RAM y procesador adecuados para el tamaño del diseño: consulta los requisitos oficiales y notas de versión de la familia FPGA que usarás, pues no existe un único valor válido para todos los diseños.
- Conocer el modelo de FPGA o la placa (por ejemplo, para escoger su familia de dispositivos).

**Comprobar Windows:** `Configuración → Sistema → Información` (versión, RAM y arquitectura). Comprueba el espacio en `Este equipo`.

## 2. Descarga oficial

1. Abre [Quartus Prime Lite 25.1 para Windows](https://www.altera.com/downloads/fpga-development-tools/quartus-prime-lite-edition-design-software-version-25-1-windows).
2. Comprueba que el encabezado indique **Lite Edition**, **25.1** y **Windows**.
3. En **Quartus Prime Installer (Recommended)**, descarga `qinst-lite-windows-25.1std-1129.exe` (instalador inicial de aproximadamente 32,8 MB). **No es el programa completo:** descarga componentes durante la instalación.
4. Si necesitas instalación sin conexión, utiliza **Complete Download**, archivo `Quartus-lite-25.1std.0.1129-windows.tar` (~6,5 GB), y sigue las instrucciones de extracción e instalación de los paquetes incluidos. No confundas el archivo `.tar` con un ejecutable.
5. Puede requerirse aceptar condiciones o iniciar sesión, dependiendo del portal.

> Los nombres y tamaños corresponden a la página oficial consultada en noviembre de 2026. Verifica siempre el nombre mostrado en el portal antes de descargar.

## 3. Instalación con el instalador recomendado

1. Busca el archivo `.exe` en Descargas.
2. Ejecútalo con una cuenta autorizada; acepta el aviso de Windows si corresponde.
3. El instalador extrae sus archivos temporales y abre el asistente de Quartus.
4. Acepta los términos de licencia después de leerlos.
5. Selecciona **Quartus Prime Lite Edition** y los **device support files** de la familia FPGA de tu curso. No instales todas las familias si no las necesitas.
6. Opcionalmente selecciona **Questa-Altera FPGA Starter Edition** si tu curso requiere simulación; es un componente separado y puede tener requisitos de licencia propios.
7. Elige una ruta de instalación con suficiente espacio. La ubicación puede variar; conserva la ruta final para ejecutar y localizar herramientas.
8. Inicia la descarga e instalación y espera a que termine. Si aparecen opciones como **Auto install after download**, verifica que estén activadas si deseas instalación automática.
9. Revisa el resumen final y los mensajes de error; finaliza el asistente.

**Importante:** los nombres y el orden de las pantallas pueden variar. No marques como instalado un componente que no hayas comprobado.

## 4. Primer inicio

- Abre el menú Inicio y busca **Quartus** o **Altera FPGA 25.1 Lite Edition**.
- También puedes localizar el ejecutable `quartus.exe` dentro del directorio de instalación correspondiente, normalmente bajo `quartus/bin64`.
- Confirma en **Help → About** (o en la pantalla de inicio) que se trata de la edición Lite y versión esperada.
- La edición Lite es gratuita para las funciones y dispositivos admitidos. Si aparece una solicitud de licencia, comprueba que no hayas abierto Standard/Pro u otro componente que requiera licencia.

## 5. Verificación con un diseño VHDL

1. Descarga o copia [`and_gate.vhd`](../ejemplos/compuerta_and/and_gate.vhd).
2. Abre Quartus y selecciona **File → New Project Wizard**.
3. Crea una carpeta de proyecto sin espacios problemáticos, por ejemplo `C:\FPGA\and_gate`.
4. Define `and_gate` como nombre del proyecto y como entidad de nivel superior (*top-level entity*).
5. Agrega `and_gate.vhd` al proyecto.
6. Selecciona una **familia y dispositivo FPGA realmente instalados**. Si no aparece el dispositivo, instala su paquete desde las herramientas de mantenimiento/instalación.
7. Finaliza el asistente y comprueba que el archivo VHDL figure en el proyecto.
8. Ejecuta **Processing → Start → Start Analysis & Synthesis** (el texto puede variar). Comprueba que el proceso termine sin errores.
9. Si hay un dispositivo de destino válido y todos los componentes requeridos, ejecuta **Processing → Start Compilation** para la compilación completa.
10. Examina **Compilation Report** y **Messages**. Guarda una captura real de la versión y del resultado.

**Resultado esperado:** síntesis sin errores de una función `Y = A AND B`. La compilación completa puede generar un archivo de programación según la familia y configuración. **Esto no demuestra que una FPGA física haya sido programada.**

## 6. Programación de una placa (opcional)

1. Conecta una placa FPGA compatible y su programador, normalmente USB-Blaster.
2. Instala el controlador de programación correspondiente desde las herramientas oficiales, si Windows lo requiere.
3. Abre **Tools → Programmer** y selecciona el hardware detectado en **Hardware Setup**.
4. Carga el archivo de programación generado para **ese dispositivo específico**.
5. Comprueba el modo de programación, las opciones y el dispositivo antes de pulsar **Start**.

**No intentes cargar un archivo destinado a otra FPGA.** Las asignaciones de pines requieren el manual de la placa.

## 7. Problemas frecuentes

| Problema | Comprobación o solución |
|---|---|
| Instalador no inicia | Comprueba descarga completa, permisos y compatibilidad del SO; vuelve a descargar desde Altera. |
| Falta espacio | Libera espacio para descarga, extracción, instalación y proyectos. |
| No aparece mi FPGA | Instala el paquete de dispositivos de la familia correcta y revisa soporte de la versión. |
| No encuentro Quartus | Busca en Inicio o en el directorio elegido durante la instalación. |
| Error de licencia | Confirma que abriste **Lite**, no Standard/Pro ni una herramienta separada con licencia. |
| Error de VHDL | Revisa nombre de entidad, sintaxis y archivo top-level. |
| No se detecta USB-Blaster | Revisa cable, alimentación, drivers, Administrador de dispositivos y Hardware Setup. |
| Síntesis correcta, programación fallida | Verifica placa, pines, dispositivo y archivo de programación. |

## 8. Lista de verificación

- [ ] Windows y recursos compatibles
- [ ] Descarga oficial Lite 25.1
- [ ] Instalador y dispositivos correctos
- [ ] Quartus abre y muestra la versión esperada
- [ ] Proyecto VHDL creado
- [ ] Analysis & Synthesis sin errores
- [ ] Compilación completa comprobada, si aplica
- [ ] Programación física comprobada, solo si hay placa

## 9. Referencias

- [Descarga Windows 25.1](https://www.altera.com/downloads/fpga-development-tools/quartus-prime-lite-edition-design-software-version-25-1-windows)
- [Compatibilidad de sistemas operativos](https://www.altera.com/developers/software/os-support)
- [Soporte de instalación de Intel FPGA](https://www.intel.com/content/www/us/en/support/programmable/licensing/installation-and-licensing.html)
- [Manual de instalación y licencias](https://www.intel.com/programmable/technical-pdfs/683472.pdf)

[← Inicio](../README.md)
