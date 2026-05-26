# Problemas encontrados durante el laboratorio

# Introducción

Durante el desarrollo del laboratorio aparecieron diferentes problemas relacionados principalmente con permisos, configuraciones del sistema y análisis de archivos sensibles dentro del entorno Linux.

Una parte importante del aprendizaje consistió precisamente en identificar estos problemas, entender por qué ocurrían y buscar formas correctas de solucionarlos sin comprometer el funcionamiento general del sistema.

Además, muchos errores encontrados reflejan situaciones bastante habituales dentro de entornos Linux mal configurados o administrados sin medidas básicas de hardening.

---

# Problemas relacionados con permisos

Uno de los problemas más frecuentes estuvo relacionado con permisos excesivos en archivos y directorios.

Durante la auditoría aparecieron directorios con permisos world writable, lo que permitía que cualquier usuario del sistema pudiera modificar contenido dentro de determinadas rutas.

Esto representa un riesgo importante porque facilita:

- modificación no autorizada de archivos
- ejecución de binarios maliciosos
- persistencia
- escalada de privilegios

La solución aplicada consistió en restringir permisos utilizando `chmod` y revisar propietarios mediante `chown`.

---

# Problemas relacionados con SUID

Otra parte especialmente delicada del laboratorio fue el análisis de binarios con permisos SUID activos.

Aunque algunos binarios necesitan este tipo de permisos para funcionar correctamente, otros pueden convertirse en un riesgo si permiten ejecución insegura o interacción con comandos del sistema.

Uno de los principales problemas encontrados fue distinguir qué binarios eran legítimos y cuáles podían representar una exposición innecesaria.

Esto obligó a revisar documentación y analizar el comportamiento real de determinados archivos antes de eliminar permisos SUID de forma incorrecta.

---

# Problemas con PATH Hijacking

Durante las pruebas relacionadas con la variable PATH se observaron configuraciones inseguras que podían facilitar ejecución de comandos maliciosos.

El principal problema consistía en incluir directorios inseguros o rutas modificables por usuarios sin privilegios dentro de la variable PATH.

Esto puede provocar que un usuario ejecute accidentalmente un binario malicioso creyendo que se trata de un comando legítimo del sistema.

La solución consistió en revisar cuidadosamente las rutas configuradas y restringir permisos sobre directorios sensibles.

---

# Problemas de montaje y particiones

También aparecieron problemas relacionados con configuraciones inseguras de particiones y sistemas montados.

En algunos casos determinadas rutas no utilizaban opciones de seguridad como:

- noexec
- nosuid
- nodev

La ausencia de estas opciones puede facilitar ejecución de binarios no autorizados o abuso de dispositivos dentro del sistema.

Durante el laboratorio se revisaron especialmente directorios temporales y particiones compartidas.

---

# Problemas durante auditorías automáticas

La utilización de herramientas como Lynis también generó algunos problemas relacionados con falsos positivos o recomendaciones demasiado genéricas.

No todas las advertencias detectadas implicaban necesariamente un riesgo crítico real, por lo que fue necesario interpretar correctamente los resultados y comprender el contexto de cada recomendación.

Esto ayudó a entender que las herramientas automáticas son útiles como apoyo, pero no sustituyen el análisis manual ni el criterio técnico.

---

# Problemas relacionados con permisos de ejecución

Otro problema frecuente apareció al modificar permisos de archivos ejecutables.

En algunos casos, al restringir permisos de forma excesiva, determinados scripts o comandos dejaron de funcionar correctamente.

Esto permitió comprender la importancia de aplicar hardening sin romper funcionalidades necesarias del sistema.

---

# Conclusiones

Los problemas encontrados durante el laboratorio ayudaron a comprender mejor cómo funcionan los sistemas Linux desde una perspectiva defensiva y cómo pequeñas configuraciones inseguras pueden convertirse en riesgos importantes si no se revisan correctamente.

Además, el proceso de diagnóstico y resolución permitió reforzar conocimientos relacionados con permisos, privilegios, administración Linux y hardening de sistemas.
