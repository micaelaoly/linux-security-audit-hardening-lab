# Análisis de permisos en Linux

# Introducción

Durante el laboratorio se realizó una revisión de permisos sobre diferentes archivos y directorios del sistema con el objetivo de identificar configuraciones inseguras que pudieran facilitar accesos no autorizados, modificación de contenido sensible o posibles escenarios de escalada de privilegios.

La gestión de permisos en Linux es una de las bases más importantes de seguridad dentro del sistema operativo, ya que controla qué usuarios pueden leer, modificar o ejecutar archivos y directorios.

Una configuración incorrecta puede provocar que usuarios sin privilegios accedan a información sensible o alteren componentes importantes del sistema.

---

# Permisos básicos en Linux

Linux utiliza un sistema de permisos basado en:

- lectura (`r`)
- escritura (`w`)
- ejecución (`x`)

Estos permisos se aplican sobre:

- propietario
- grupo
- otros usuarios

Ejemplo:

```bash
-rwxr-xr-x
```

Esto indica:

| Usuario | Permisos |
|---|---|
| Propietario | lectura, escritura y ejecución |
| Grupo | lectura y ejecución |
| Otros | lectura y ejecución |

---

# Permisos inseguros

Durante el laboratorio se revisaron especialmente permisos excesivamente permisivos como:

```bash
777
```

Este tipo de permisos permite lectura, escritura y ejecución para cualquier usuario del sistema.

Aunque pueden utilizarse temporalmente durante pruebas, en entornos reales representan un riesgo importante porque facilitan:

- modificación de archivos
- ejecución de contenido malicioso
- alteración de scripts
- persistencia
- escalada de privilegios

---

# Auditoría de permisos

Para localizar archivos inseguros se utilizaron comandos como:

```bash
find / -type f -perm 777 2>/dev/null
```

También se revisaron directorios world writable:

```bash
find / -type d -perm -0002 2>/dev/null
```

El objetivo fue identificar rutas donde cualquier usuario pudiera modificar contenido dentro del sistema.

---

# Gestión de permisos

Durante el laboratorio se modificaron permisos utilizando:

```bash
chmod
```

Ejemplo:

```bash
chmod 644 archivo.txt
```

También se revisaron propietarios mediante:

```bash
chown usuario:grupo archivo.txt
```

Esto permitió aplicar configuraciones más seguras siguiendo el principio de mínimo privilegio.

---

# Principio de mínimo privilegio

Gran parte del hardening realizado se basó en reducir permisos innecesarios y limitar accesos únicamente a los usuarios que realmente necesitaban interactuar con determinados archivos o directorios.

Aplicar correctamente este principio ayuda a reducir:

- superficie de ataque
- accesos indebidos
- modificación accidental
- abuso de privilegios

---

# Conclusiones

El análisis de permisos realizado durante el laboratorio permitió comprender cómo configuraciones aparentemente simples pueden convertirse en riesgos importantes dentro de un sistema Linux.

Además, ayudó a reforzar conocimientos relacionados con administración segura, control de accesos y hardening defensivo.
