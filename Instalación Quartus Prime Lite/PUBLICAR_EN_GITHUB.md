# Cómo publicar este proyecto en GitHub

1. Crea un repositorio público en GitHub, por ejemplo `quartus-prime-lite`.
2. Descomprime el ZIP y abre una terminal en la carpeta `quartus-prime-lite`.
3. Ejecuta:

```bash
git init
git add .
git commit -m "Documentación de instalación de Quartus Prime Lite 25.1"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/quartus-prime-lite.git
git push -u origin main
```

Reemplaza `TU_USUARIO` por tu usuario. Si GitHub solicita autenticación, utiliza su flujo de inicio de sesión o credenciales adecuadas (no una contraseña de cuenta en la terminal). Si el repositorio remoto ya tiene commits, integra los cambios antes de subirlos.

## Capturas reales opcionales

Puedes añadir `Windows/imagenes/` y `Linux/imagenes/` para capturas verificadas. Enlázalas así:

```markdown
![Instalador de Quartus en Windows](imagenes/instalador.png)
```

**No incluyas capturas inventadas como evidencia de una instalación real.**
