# Recomendaciones de hardening aplicadas

# Introducción

Tras finalizar la auditoría de seguridad del sistema Linux se aplicaron diferentes medidas de hardening orientadas a reducir riesgos relacionados con permisos inseguros, escalada de privilegios y configuraciones vulnerables.

El objetivo principal no fue únicamente detectar problemas, sino también comprender cómo mitigarlos mediante configuraciones más seguras y buenas prácticas de administración.

---

# Principales medidas aplicadas

Durante el laboratorio se implementaron diferentes recomendaciones defensivas relacionadas con:

- permisos
- usuarios
- particiones
- SUID
- directorios inseguros
- variables de entorno

---

# Restricción de permisos

Se revisaron archivos y directorios con permisos excesivos aplicando configuraciones más restrictivas mediante:

```bash
chmod
```

y:

```bash
chown
```

El objetivo fue limitar accesos únicamente a usuarios necesarios.

---

# Eliminación de permisos SUID innecesarios

También se eliminaron permisos SUID innecesarios sobre determinados binarios utilizando:

```bash
chmod u-s archivo
```

Esto permitió reducir posibles escenarios relacionados con escalada de privilegios.

---

# Revisión de PATH

Se revisó la variable PATH para evitar directorios inseguros o modificables por usuarios sin privilegios.

Además, se recomendó utilizar rutas absolutas dentro de scripts privilegiados para evitar PATH Hijacking.

---

# Hardening de particiones

Se añadieron opciones de seguridad sobre determinadas particiones utilizando:

- noexec
- nosuid
- nodev

Esto ayudó a reducir riesgos relacionados con ejecución no autorizada y abuso de permisos especiales.

---

# Aplicación del principio de mínimo privilegio

Gran parte de las medidas implementadas se basaron en conceder únicamente los permisos estrictamente necesarios para cada usuario, servicio o aplicación.

Esto permite limitar impacto en caso de compromiso del sistema.

---

# Monitorización y auditoría

También se recomendó realizar:

- revisiones periódicas de permisos
- auditorías automáticas
- monitorización de logs
- revisión de servicios activos

La seguridad del sistema depende no solo de la configuración inicial, sino también del mantenimiento continuo.

---

# Conclusiones

Las medidas aplicadas durante el laboratorio permitieron mejorar considerablemente la seguridad general del sistema Linux y reducir riesgos relacionados con configuraciones inseguras y privilegios excesivos.

Además, ayudaron a comprender cómo el hardening básico representa una parte fundamental dentro de cualquier estrategia de seguridad defensiva.
