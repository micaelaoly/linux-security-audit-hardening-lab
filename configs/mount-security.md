# Seguridad en particiones y montaje

# Introducción

Durante el laboratorio también se revisaron configuraciones relacionadas con particiones montadas y opciones de seguridad aplicadas dentro del sistema Linux.

Las opciones de montaje permiten controlar comportamientos relacionados con ejecución de binarios, uso de dispositivos y permisos especiales dentro de determinadas rutas del sistema.

Una configuración incorrecta puede facilitar ejecución de código no autorizado o abuso de permisos especiales.

---

# Revisión de particiones

Para revisar sistemas montados se utilizó:

```bash
mount
```

También se analizaron configuraciones persistentes dentro de:

```bash
/etc/fstab
```

---

# Opciones de seguridad

Las principales opciones revisadas durante el laboratorio fueron:

| Opción | Función |
|---|---|
| noexec | Impide ejecución de binarios |
| nosuid | Bloquea permisos SUID |
| nodev | Impide uso de dispositivos |

Estas opciones son especialmente importantes en directorios temporales o particiones compartidas.

---

# Riesgos detectados

La ausencia de restricciones puede facilitar:

- ejecución de malware
- abuso de binarios SUID
- ejecución arbitraria
- interacción insegura con dispositivos

---

# Medidas aplicadas

Durante el laboratorio se revisaron configuraciones de montaje y se añadieron opciones de seguridad sobre determinadas rutas sensibles.

Esto ayudó a reducir superficie de ataque y limitar posibilidades de abuso dentro del sistema.

---

# Conclusiones

El análisis de particiones permitió comprender cómo configuraciones relacionadas con montaje también forman parte importante del hardening defensivo dentro de Linux.
