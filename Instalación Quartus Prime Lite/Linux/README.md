# 🐧 Instalación de Quartus Prime Lite Edition 25.1 en Linux

[← Volver al inicio](../README.md) · [Ver guía de Windows](../Windows/README.md)

> **Guía principal: Ubuntu.** Se incluyen orientaciones para Linux Mint, Debian, Fedora y otras distribuciones. **No significa que todas estén certificadas por Altera.**

## 1. Compatibilidad y requisitos

La matriz oficial de **Quartus Prime Lite 25.1** incluye **Ubuntu 18.04 LTS, 20.04 LTS y 22.04 LTS**, además de versiones específicas de Red Hat Enterprise Linux y SUSE Linux Enterprise. **Ubuntu 24.04 LTS, 26.04, Debian, Linux Mint y Fedora no figuran expresamente como soportados en la tabla de Lite 25.1.** Que una distribución no figure no demuestra que sea imposible ejecutarlo, pero su funcionamiento no está garantizado.

Para el paquete completo de Linux 25.1, Altera indica aproximadamente **40,10 GB** para descarga, extracción e instalación. Reserva espacio adicional para proyectos. Comprueba memoria y CPU en las notas de versión y según la complejidad de tus diseños.

### Identificar tu Ubuntu

```bash
cat /etc/os-release
uname -m
df -h ~
free -h
```

- `VERSION_ID`: versión del sistema.
- `uname -m`: normalmente `x86_64` para un equipo compatible de 64 bits.
- `df -h`: espacio libre.
- `free -h`: memoria disponible.

**Si utilizas Ubuntu 24.04 o posterior:** consulta la matriz oficial y las notas de versión; considera un entorno Ubuntu 22.04 LTS compatible (equipo independiente o máquina virtual con recursos suficientes) para una demostración reproducible. No mezcles paquetes de versiones anteriores de Ubuntu sin comprobar dependencias.

## 2. Descargar Quartus Prime Lite

1. Abre la [página oficial Lite 25.1 para Linux](https://www.altera.com/downloads/fpga-development-tools/quartus-prime-lite-edition-design-software-version-25-1-linux).
2. Confirma que seleccionaste **Lite Edition 25.1 — Linux**.
3. En **Quartus Prime Installer (Recommended)** descarga `qinst-lite-linux-25.1std-1129.run` (~67,7 MB). **Es un instalador inicial que descarga los componentes seleccionados**, no el paquete completo.
4. Alternativamente, **Complete Download** ofrece `Quartus-lite-25.1std.0.1129-linux.tar` (~8,9 GB) con paquetes de dispositivos; es más apropiado cuando se necesita una descarga completa.
5. Guarda el instalador en `~/Descargas` (o en la carpeta que uses).

## 3. Instalar en Ubuntu (método recomendado)

Abre una terminal y entra en la carpeta de descargas. En una instalación de Ubuntu en español suele ser `~/Descargas`, pero puede ser `~/Downloads`:

```bash
cd "$(xdg-user-dir DOWNLOAD)"
ls -lh qinst-lite-linux-25.1std-1129.run
chmod +x qinst-lite-linux-25.1std-1129.run
./qinst-lite-linux-25.1std-1129.run
```

Si `xdg-user-dir` no está disponible, usa `cd ~/Descargas` o `cd ~/Downloads` según corresponda.

El `.run` extrae los archivos temporales y abre el instalador gráfico cuando hay un entorno de escritorio disponible.

1. Lee y acepta las condiciones de uso.
2. Selecciona **Quartus Prime Lite Edition**.
3. Selecciona la **familia FPGA** que necesitas (paquetes de dispositivos). Comprueba la placa de tu curso.
4. Opcional: instala **Questa-Altera FPGA Starter Edition** si necesitas simulación; sus requisitos de licencia y ejecución son independientes.
5. Elige una carpeta de instalación con espacio suficiente, preferentemente dentro de tu directorio personal si el instalador lo permite.
6. Inicia descarga e instalación; espera a que termine y revisa el resumen.

**Evita `sudo` para lanzar el instalador completo salvo que la documentación o la ruta de destino realmente requieran permisos elevados.** No es necesario ejecutar la aplicación de diseño como root.

### Instalación en modo consola

Si el equipo no tiene interfaz gráfica o el instalador no muestra ventanas, el instalador oficial también admite un flujo CLI. Para extraer sus archivos:

```bash
./qinst-lite-linux-25.1std-1129.run -- --target /tmp/quartus_installer
```

Después, desde el directorio extraído que contiene `qinst.sh`:

```bash
./qinst.sh --help
./qinst.sh --cli
```

La sintaxis exacta y las opciones se consultan con `--help`; no se debe asumir que un comando genérico instala automáticamente todos los componentes.

## 4. Abrir Quartus en Ubuntu

Altera documenta el ejecutable Linux en la ruta relativa:

```text
<directorio-de-instalación>/quartus/bin/quartus
```

Si, por ejemplo, elegiste `~/altera_lite/25.1` como directorio base, prueba:

```bash
"$HOME/altera_lite/25.1/quartus/bin/quartus"
```

La ruta es un **ejemplo**, no una garantía de dónde quedó instalado. Comprueba la ubicación que seleccionaste en el instalador. Si necesitas localizarlo:

```bash
find "$HOME" -type f -path '*/quartus/bin/quartus' 2>/dev/null
```

Para abrirlo desde cualquier carpeta, puedes añadir el directorio `quartus/bin` a tu `PATH` en `~/.bashrc`, sustituyendo la ruta por la real:

```bash
export PATH="$HOME/altera_lite/25.1/quartus/bin:$PATH"
```

Cierra y vuelve a abrir la terminal o ejecuta `source ~/.bashrc`. Después prueba `quartus`.

## 5. Comprobar que funciona

1. Abre Quartus y verifica edición y versión en **Help → About**.
2. Descarga [`and_gate.vhd`](../ejemplos/compuerta_and/and_gate.vhd).
3. Crea un proyecto nuevo con **File → New Project Wizard**.
4. Elige una carpeta de trabajo, por ejemplo `~/FPGA/and_gate`.
5. Define `and_gate` como nombre del proyecto y entidad superior.
6. Añade el archivo VHDL y selecciona un dispositivo **soportado e instalado**.
7. Ejecuta **Processing → Start → Start Analysis & Synthesis** y revisa **Messages**.
8. Si tienes los paquetes y el dispositivo adecuados, ejecuta **Start Compilation** y revisa el informe.

**Criterio de éxito:** el proyecto pasa el análisis y la síntesis sin errores. No necesitas una FPGA física para esta prueba. Para programar hardware sí se requiere una placa compatible.

## 6. Programador USB-Blaster en Linux (opcional)

El programador USB-Blaster puede requerir reglas **udev**, permisos de acceso USB y/o instalación de herramientas de programación adicionales. **No existe una regla universal segura para todas las variantes de USB-Blaster y placas.** Identifica el dispositivo con `lsusb`, consulta la documentación oficial de tu modelo, instala el controlador o las reglas correspondientes y vuelve a conectar el hardware. Evita dar permisos indiscriminados a todos los dispositivos USB.

Si la placa está conectada, comprueba la detección en **Tools → Programmer → Hardware Setup**. La ausencia de una placa no impide usar Quartus para síntesis.

## 7. Otras distribuciones Linux

| Distribución | Recomendación |
|---|---|
| **Linux Mint** | Basada habitualmente en Ubuntu; verifica primero la versión base. Usa el instalador `.run`, pero la compatibilidad no está certificada explícitamente. |
| **Debian** | Usa el instalador `.run` de Linux, comprueba bibliotecas y compatibilidad. No asumas que paquetes de Ubuntu tienen idénticos nombres o versiones. |
| **Fedora** | Usa el instalador `.run` si deseas probarlo, pero Fedora no aparece en la matriz oficial de Lite 25.1. Consulta dependencias y versiones; no apliques instrucciones de `apt`. |
| **Red Hat Enterprise Linux** | Altera enumera versiones específicas de RHEL 8.6, 8.7, 9.0 y 9.1 para Lite 25.1. Verifica tu versión exacta. |
| **SUSE Linux Enterprise** | Altera enumera SLE 12.5, 15.3 y 15.4 para Lite 25.1. Verifica tu versión exacta. |
| **Arch / Manjaro / otras** | Instalación experimental, no oficialmente certificada en la matriz citada. Consulta dependencias de tu distribución. |

**El procedimiento general** (descargar `.run`, `chmod +x`, ejecutar, elegir componentes, iniciar Quartus y sintetizar) es parecido, pero **las dependencias, bibliotecas y compatibilidad varían**. No existe un comando `apt`, `dnf` o `pacman` oficial y universal que sustituya al instalador de Altera.

## 8. Solución de problemas

| Síntoma | Qué revisar |
|---|---|
| `Permission denied` al abrir `.run` | `chmod +x archivo.run`; permisos de carpeta y montaje `noexec`. |
| `No such file or directory` | Comprueba nombre y ubicación con `pwd` y `ls`; verifica arquitectura y dependencias si el archivo existe. |
| No abre la ventana | Revisa sesión gráfica, bibliotecas faltantes y compatibilidad del SO; consulta la salida de terminal. |
| Error de bibliotecas compartidas | Revisa el mensaje exacto y la compatibilidad de la versión; instala únicamente paquetes apropiados para tu distribución. |
| No aparece la FPGA | Falta el paquete de dispositivos o esa familia no es compatible con la versión. |
| No encuentra `quartus` | Usa la ruta absoluta al ejecutable o ajusta `PATH`. |
| Error de licencia | Comprueba que instalaste **Lite** y que el aviso no pertenece a una herramienta adicional. |
| USB-Blaster no detectado | Revisa cable, alimentación, `lsusb`, permisos udev y documentación de la placa. |
| Falló la compilación | Lee **Messages**: sintaxis, top-level, archivos, familia FPGA y restricciones. |

## 9. Lista de verificación

- [ ] Versión y arquitectura de Linux identificadas
- [ ] Compatibilidad comprobada en la matriz oficial
- [ ] Espacio libre suficiente
- [ ] Instalador Lite 25.1 descargado de Altera
- [ ] Permisos de ejecución configurados
- [ ] Dispositivos FPGA instalados
- [ ] Quartus abre y muestra su versión
- [ ] VHDL analizado y sintetizado sin errores
- [ ] Compilación completa probada, si aplica
- [ ] Programador comprobado, solo si hay placa física

## 10. Referencias oficiales

- [Descarga Linux 25.1](https://www.altera.com/downloads/fpga-development-tools/quartus-prime-lite-edition-design-software-version-25-1-linux)
- [Matriz de sistemas operativos](https://www.altera.com/developers/software/os-support)
- [Manual de instalación y licencias](https://www.intel.com/programmable/technical-pdfs/683472.pdf)
- [Soporte de instalación](https://www.intel.com/content/www/us/en/support/programmable/licensing/installation-and-licensing.html)

[← Inicio](../README.md)
