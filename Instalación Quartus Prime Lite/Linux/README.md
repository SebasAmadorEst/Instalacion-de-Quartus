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
ls -lh
```

**Comprueba primero el nombre real del instalador.** Si coincide con el de esta guía, ejecuta:

```bash
chmod +x ./qinst-lite-linux-25.1std-1129.run
./qinst-lite-linux-25.1std-1129.run
```

Si `xdg-user-dir` no está disponible, usa `cd ~/Descargas` o `cd ~/Downloads` según corresponda.

### 3.1. Error: «No existe el archivo o el directorio» al ejecutar el instalador

Si `ls`, `chmod` y `./qinst...run` responden que el archivo no existe, **no significa necesariamente que Quartus esté dañado**: el nombre escrito puede no coincidir, la descarga puede estar en otra carpeta o puede no haber terminado.

1. Confirma la ubicación actual y lista los archivos:

   ```bash
   cd "$(xdg-user-dir DOWNLOAD)"
   pwd
   ls -lh
   ```

2. Busca instaladores `.run` en Descargas y sus subcarpetas inmediatas:

   ```bash
   find "$(xdg-user-dir DOWNLOAD)" -maxdepth 2 -type f -iname '*.run'
   ```

3. Copia **el nombre exacto** del archivo que aparezca y úsalo en `chmod +x` y `./nombre-real.run`. Si no aparece, revisa las descargas del navegador y vuelve a descargarlo desde la web oficial si hace falta. No cambies el nombre a ciegas.

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

**Atención: la carpeta de la versión puede llamarse `25.1std`, no `25.1`.** En una instalación real de Quartus Prime Lite 25.1, la carpeta encontrada fue `~/altera_lite/25.1std`.

### 4.1. Error: «No existe el archivo o el directorio» al abrir Quartus

Si ejecutas:

```bash
"$HOME/altera_lite/25.1/quartus/bin/quartus"
```

y obtienes `No existe el archivo o el directorio`, **comprueba primero el nombre de la carpeta de instalación**:

```bash
ls -lah "$HOME/altera_lite"
```

Por ejemplo, si la salida muestra `25.1std`, la ruta correcta para esa instalación es:

```bash
"$HOME/altera_lite/25.1std/quartus/bin/quartus"
```

Si tampoco funciona, localiza el ejecutable real sin asumir la ruta:

```bash
find "$HOME" -type f -path '*/quartus/bin/quartus' 2>/dev/null
```

Comprueba el archivo encontrado con `ls -lh RUTA_ENCONTRADA` y ejecútalo con su ruta absoluta entre comillas. Si el archivo **sí existe** pero Bash sigue mostrando un error similar, podría tratarse de bibliotecas o del intérprete de ejecución; conserva el mensaje exacto para diagnosticarlo. No reinstales antes de comprobarlo.

### 4.2. Primera ejecución

Al iniciar correctamente Quartus Prime Lite 25.1, puede aparecer una ventana de bienvenida con el botón **Launch Quartus Lite**. Haz clic para entrar al entorno principal. **Esa ventana confirma que el programa se inicia**, pero todavía debes realizar la prueba de síntesis de la sección 5 para verificar el flujo de trabajo.

### 4.3. Abrir Quartus desde cualquier terminal (opcional)

Añade a tu `~/.bashrc` el directorio **real** `quartus/bin` (en el ejemplo, `25.1std`):

```bash
export PATH="$HOME/altera_lite/25.1std/quartus/bin:$PATH"
```

Cierra y vuelve a abrir la terminal o ejecuta `source ~/.bashrc`. Después prueba `quartus`. **Este cambio no crea un icono en el menú de aplicaciones**; para ello sigue la sección 4.4.

### 4.4. Hacer que Quartus aparezca como aplicación en Ubuntu

Es posible que Quartus abra desde la terminal, pero **no aparezca al buscarlo en el menú de aplicaciones**. Esto se resuelve creando un lanzador `.desktop` para tu usuario.

**Paso 1.** Comprueba que el ejecutable existe:

```bash
test -f "$HOME/altera_lite/25.1std/quartus/bin/quartus" && echo "Ejecutable encontrado"
```

Si no aparece el mensaje, vuelve a la sección 4.1 y utiliza la ruta real.

**Paso 2.** Crea la carpeta de lanzadores y el archivo:

```bash
mkdir -p "$HOME/.local/share/applications"
nano "$HOME/.local/share/applications/quartus-lite.desktop"
```

**Paso 3.** Pega este contenido, **sustituyendo `/home/lover` por tu propia ruta personal** y ajustando `25.1std` si tu instalación está en otro lugar:

```ini
[Desktop Entry]
Version=1.0
Type=Application
Name=Quartus Prime Lite 25.1
Comment=Software de diseño y desarrollo FPGA
Exec=/home/lover/altera_lite/25.1std/quartus/bin/quartus
Icon=applications-engineering
Terminal=false
Categories=Development;Education;Electronics;
StartupNotify=true
```

**Importante:** en un archivo `.desktop`, no confíes en que `~` o `$HOME` se expandan dentro de `Exec=`. Utiliza la ruta absoluta. El icono indicado es genérico.

**Paso 4.** Guarda en Nano con `Ctrl + O`, `Enter` y sal con `Ctrl + X`.

**Paso 5.** Opcionalmente, actualiza la base de datos de aplicaciones:

```bash
update-desktop-database "$HOME/.local/share/applications"
```

Si `update-desktop-database` no está disponible, puedes omitirlo. Abre el menú de aplicaciones y busca **Quartus Prime Lite 25.1**. Si no aparece inmediatamente, cierra sesión y vuelve a iniciarla.

**Paso 6.** Cuando aparezca, puedes abrirlo y hacer clic derecho en su icono del Dock para seleccionar **Añadir a favoritos**.

#### Alternativa: crear el lanzador automáticamente

Si tu instalación está en `~/altera_lite/25.1std`, este bloque evita editar manualmente tu nombre de usuario:

```bash
QUARTUS_EXE="$HOME/altera_lite/25.1std/quartus/bin/quartus"
if [ ! -f "$QUARTUS_EXE" ]; then
  echo "No se encontró Quartus en: $QUARTUS_EXE"
else
  mkdir -p "$HOME/.local/share/applications"
  cat > "$HOME/.local/share/applications/quartus-lite.desktop" <<EOF_DESKTOP
[Desktop Entry]
Version=1.0
Type=Application
Name=Quartus Prime Lite 25.1
Comment=Software de diseño FPGA
Exec=$QUARTUS_EXE
Icon=applications-engineering
Terminal=false
Categories=Development;Education;Electronics;
StartupNotify=true
EOF_DESKTOP
  echo "Acceso directo creado. Busca Quartus en el menú de aplicaciones."
fi
```

**Nota:** si la ruta contiene espacios, es preferible editar y validar el campo `Exec` del lanzador manualmente, siguiendo la especificación de archivos `.desktop`.

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
| `ls`, `chmod` o `./qinst...run`: `No existe el archivo o el directorio` | Verifica `pwd`, `ls -lh` y el nombre real del archivo. Sigue la **sección 3.1**. |
| `.../25.1/quartus/bin/quartus`: `No existe el archivo o el directorio` | La carpeta podría llamarse **`25.1std`**. Ejecuta `ls -lah ~/altera_lite` y sigue la **sección 4.1**. |
| Quartus abre desde terminal pero no aparece en Aplicaciones | Crea un archivo `.desktop` siguiendo la **sección 4.4**. |
| No abre la ventana | Revisa sesión gráfica, bibliotecas faltantes y compatibilidad del SO; consulta la salida de terminal. |
| Error de bibliotecas compartidas | Revisa el mensaje exacto y la compatibilidad de la versión; instala únicamente paquetes apropiados para tu distribución. |
| No aparece la FPGA | Falta el paquete de dispositivos o esa familia no es compatible con la versión. |
| No encuentra `quartus` como comando | Usa la ruta absoluta al ejecutable o ajusta `PATH` según la **sección 4.3**. |
| Error de licencia | Comprueba que instalaste **Lite** y que el aviso no pertenece a una herramienta adicional. |
| USB-Blaster no detectado | Revisa cable, alimentación, `lsusb`, permisos udev y documentación de la placa. |
| Falló la compilación | Lee **Messages**: sintaxis, top-level, archivos, familia FPGA y restricciones. |

## 9. Lista de verificación

- [ ] Versión y arquitectura de Linux identificadas
- [ ] Compatibilidad comprobada en la matriz oficial
- [ ] Espacio libre suficiente
- [ ] Instalador Lite 25.1 descargado de Altera
- [ ] Nombre y ubicación del `.run` verificados
- [ ] Permisos de ejecución configurados
- [ ] Dispositivos FPGA instalados
- [ ] Ruta de instalación identificada (`25.1std` u otra)
- [ ] Quartus abre y muestra su versión
- [ ] Acceso directo creado y visible en Aplicaciones (opcional)
- [ ] VHDL analizado y sintetizado sin errores
- [ ] Compilación completa probada, si aplica
- [ ] Programador comprobado, solo si hay placa física

## 10. Referencias oficiales

- [Descarga Linux 25.1](https://www.altera.com/downloads/fpga-development-tools/quartus-prime-lite-edition-design-software-version-25-1-linux)
- [Matriz de sistemas operativos](https://www.altera.com/developers/software/os-support)
- [Manual de instalación y licencias](https://www.intel.com/programmable/technical-pdfs/683472.pdf)
- [Soporte de instalación](https://www.intel.com/content/www/us/en/support/programmable/licensing/installation-and-licensing.html)

[← Inicio](../README.md)
