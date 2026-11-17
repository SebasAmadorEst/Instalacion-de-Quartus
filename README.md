# Intel / Altera Quartus Prime Lite Edition 25.1

![Versión](https://img.shields.io/badge/Quartus_Prime_Lite-25.1-blue) ![Licencia](https://img.shields.io/badge/Edici%C3%B3n-gratuita-green) ![Documentación](https://img.shields.io/badge/Idioma-Espa%C3%B1ol-orange)

> Guía educativa de instalación, configuración y verificación de Quartus Prime Lite Edition en **Windows** y **Linux**. Actualizada documentalmente: **16 de noviembre de 2026**.

## 📚 Elige tu sistema operativo

| 🪟 Windows | 🐧 Linux |
|---|---|
| [**Instalación en Windows 10/11 →**](Instalacion-Quartus-Prime-Lite/Windows/README.md) | [**Instalación en Ubuntu y otras distribuciones →**](Linux/README.md) |

## ¿Qué es Quartus Prime?

Quartus Prime es un entorno de diseño digital para desarrollar proyectos destinados a dispositivos FPGA de Altera (anteriormente Intel FPGA). Permite crear proyectos en VHDL o Verilog, analizar y sintetizar diseños, asignar pines, compilar y, con el hardware adecuado, programar una FPGA.

**Lite Edition** es la edición gratuita; no debe confundirse con Standard o Pro. La compatibilidad de familias FPGA depende de la versión y de los paquetes de dispositivos instalados.

## 🎯 Objetivo de esta documentación

1. Descargar la versión correcta desde la fuente oficial.
2. Instalar Quartus Prime Lite Edition y los paquetes de dispositivos necesarios.
3. Abrir la aplicación y crear un proyecto VHDL.
4. Ejecutar una compilación básica para comprobar el funcionamiento.
5. Diferenciar la compilación del diseño de la programación de una FPGA física.

## 🧪 Prueba incluida

El repositorio incluye un ejemplo mínimo: [compuerta AND de dos entradas](ejemplos/compuerta_and/and_gate.vhd), además de una [guía de verificación](ejemplos/README.md). **No es necesario disponer de una placa FPGA para comprobar el análisis y la síntesis**; para una compilación completa hay que elegir un dispositivo instalado y compatible. La programación real sí necesita hardware y, normalmente, un programador USB-Blaster.

## 📌 Antes de comenzar

- Verifica la versión de tu sistema operativo y el espacio disponible.
- Identifica la FPGA o placa de tu asignatura para instalar el paquete de dispositivos correcto.
- Descarga el software únicamente desde la web oficial de Altera.
- Las pantallas y nombres exactos pueden cambiar según el instalador.
- Esta documentación se basa en fuentes oficiales; **no certifica que la instalación se haya ejecutado y probado en todos los sistemas mencionados**.

## 🔗 Enlaces oficiales

- [Descarga Lite 25.1 para Windows](https://www.altera.com/downloads/fpga-development-tools/quartus-prime-lite-edition-design-software-version-25-1-windows)
- [Descarga Lite 25.1 para Linux](https://www.altera.com/downloads/fpga-development-tools/quartus-prime-lite-edition-design-software-version-25-1-linux)
- [Sistemas operativos compatibles](https://www.altera.com/developers/software/os-support)
- [Manual de instalación y licenciamiento](https://www.intel.com/programmable/technical-pdfs/683472.pdf)

**Nota de transparencia:** si presentas Windows desde Ubuntu, muestra la guía documentada y aclara que los pasos de Windows proceden de las instrucciones oficiales, no de una instalación realizada en ese equipo.

## 📄 Uso

Material educativo no oficial. Quartus y los nombres comerciales asociados pertenecen a sus respectivos titulares. Los instaladores no se redistribuyen en este repositorio.
