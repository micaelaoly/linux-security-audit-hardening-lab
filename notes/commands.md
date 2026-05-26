# Comandos utilizados durante el laboratorio

# Introducción

Durante el desarrollo del laboratorio se utilizaron diferentes comandos orientados a auditoría de seguridad, análisis de permisos, revisión de configuraciones inseguras y aplicación de medidas básicas de hardening sobre sistemas Linux.

La mayoría de herramientas utilizadas forman parte del propio sistema operativo, lo que demuestra que muchas tareas relacionadas con seguridad defensiva y auditoría pueden realizarse sin necesidad de instalar software complejo o herramientas externas avanzadas.

Además de ejecutar los comandos, una de las partes más importantes fue comprender realmente qué información proporciona cada uno y cómo interpretar correctamente los resultados obtenidos.

---

# Auditoría de permisos inseguros

Uno de los primeros análisis realizados estuvo relacionado con la búsqueda de archivos y directorios con permisos excesivos.

Para localizar directorios world writable se utilizó:

```bash
find / -type d -perm -0002 2>/dev/null
```

Este comando permite buscar directorios donde cualquier usuario del sistema tenga permisos de escritura, algo que puede representar un riesgo importante si no está correctamente controlado.

También se realizaron búsquedas de archivos con permisos inseguros:

```bash
find / -type f -perm 777 2>/dev/null
```

La utilización de permisos `777` implica lectura, escritura y ejecución para cualquier usuario del sistema, algo que normalmente no debería existir en entornos seguros salvo casos muy concretos.

---

# Análisis de binarios SUID

Otra parte importante del laboratorio consistió en revisar archivos con permisos SUID activos.

Para ello se utilizó:

```bash
find / -perm -4000 2>/dev/null
```

Los binarios SUID pueden ejecutarse con privilegios elevados aunque sean lanzados por usuarios normales. Esto puede ser legítimo en determinados binarios del sistema, pero también representa un vector clásico de escalada de privilegios si existe una mala configuración o un binario vulnerable.

Durante el análisis se revisaron especialmente binarios poco habituales o que no deberían tener este tipo de permisos.

---

# Revisión de la variable PATH

También se analizó la configuración de la variable PATH para detectar posibles riesgos relacionados con PATH Hijacking.

La comprobación se realizó mediante:

```bash
echo $PATH
```

El objetivo fue revisar si existían rutas inseguras, directorios compartidos o ubicaciones donde usuarios sin privilegios pudieran introducir binarios maliciosos que posteriormente fueran ejecutados por otros usuarios o procesos privilegiados.

Este tipo de configuraciones puede facilitar ataques relacionados con ejecución arbitraria de comandos y escalada de privilegios.

---

# Análisis de particiones y montaje

Otra parte importante del laboratorio estuvo relacionada con la revisión de particiones montadas y opciones de seguridad asociadas.

Para visualizar sistemas montados se utilizó:

```bash
mount
```

También se revisó el archivo:

```bash
/etc/fstab
```

El objetivo fue analizar si determinadas particiones utilizaban opciones de seguridad como:

- noexec
- nosuid
- nodev

Estas opciones ayudan a reducir riesgos relacionados con ejecución de binarios no autorizados, uso indebido de dispositivos o abuso de permisos SUID.

---

# Borrado seguro de archivos

Durante el laboratorio también se trabajó el borrado seguro de información utilizando herramientas como `shred`.

Ejemplo utilizado:

```bash
shred -u archivo.txt
```

La finalidad de este comando es sobrescribir varias veces el contenido de un archivo antes de eliminarlo para dificultar su recuperación posterior.

Esto permitió comprender diferencias entre un borrado tradicional y un borrado orientado a reducir posibilidades de recuperación forense.

---

# Auditoría con Lynis

También se realizaron auditorías básicas del sistema utilizando Lynis.

```bash
sudo lynis audit system
```

Lynis permitió generar recomendaciones relacionadas con:

- hardening
- permisos
- servicios inseguros
- configuraciones del sistema
- exposición innecesaria

Además ayudó a comprender cómo herramientas automáticas pueden detectar configuraciones inseguras y proponer medidas defensivas.

---

# Gestión de permisos

Durante el laboratorio se modificaron permisos y propietarios de archivos utilizando comandos como:

```bash
chmod
```

```bash
chown
```

Estos comandos resultaron fundamentales para aplicar medidas de hardening y restringir accesos innecesarios dentro del sistema.

---

# Comprobación de procesos y archivos abiertos

También se utilizaron herramientas para analizar procesos y archivos utilizados por el sistema.

```bash
lsof
```

El objetivo fue comprender cómo determinados servicios interactúan con archivos, sockets y recursos internos del sistema.

---

# Visualización de estructuras

Para visualizar directorios y estructuras del sistema de forma más clara se utilizó:

```bash
tree
```

Esto ayudó especialmente a analizar directorios inseguros y comprender mejor la organización de archivos dentro del laboratorio.

---

# Conclusiones

Los comandos utilizados durante el laboratorio permitieron comprender cómo realizar auditorías básicas de seguridad en Linux utilizando herramientas nativas del sistema.

Además de aprender sintaxis concreta, la parte más importante fue entender qué riesgos puede representar cada configuración insegura y cómo aplicar medidas defensivas orientadas a reducir superficie de ataque y mejorar la seguridad general del entorno Linux.
