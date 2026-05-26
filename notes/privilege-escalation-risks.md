# Riesgos relacionados con escalada de privilegios

# Introducción

Uno de los principales objetivos del laboratorio fue comprender cómo determinadas configuraciones inseguras dentro de sistemas Linux pueden facilitar escenarios de escalada de privilegios.

La escalada de privilegios consiste en conseguir permisos superiores a los inicialmente disponibles mediante abuso de configuraciones incorrectas, permisos inseguros, binarios vulnerables o malas prácticas de administración.

Aunque muchas veces estos riesgos pasan desapercibidos en sistemas pequeños o mal mantenidos, en entornos reales pueden convertirse en una vía directa para comprometer completamente un servidor.

Durante el laboratorio se analizaron diferentes configuraciones que podían facilitar este tipo de situaciones y posteriormente se aplicaron medidas básicas de mitigación y hardening.

---

# Directorios world writable

Uno de los riesgos más importantes detectados estuvo relacionado con directorios configurados con permisos world writable.

Este tipo de directorios permiten que cualquier usuario del sistema pueda escribir contenido dentro de ellos, lo que puede facilitar:

- modificación de scripts
- reemplazo de archivos
- persistencia
- ejecución de binarios maliciosos
- abuso de aplicaciones del sistema

Especialmente peligrosos son los directorios world writable que además permiten ejecución de archivos o forman parte de rutas utilizadas por servicios privilegiados.

Durante el laboratorio se localizaron utilizando:

```bash
find / -type d -perm -0002 2>/dev/null
```

---

# Riesgos relacionados con SUID

Otra parte importante del análisis estuvo relacionada con binarios SUID.

Los archivos con permisos SUID se ejecutan con privilegios del propietario del archivo, normalmente root, aunque sean lanzados por usuarios normales.

Esto puede ser necesario en determinados binarios legítimos del sistema, pero también representa uno de los vectores clásicos de escalada de privilegios en Linux.

El principal riesgo aparece cuando:

- el binario es vulnerable
- ejecuta comandos inseguros
- utiliza PATH incorrectamente
- permite interacción con shell
- puede ser manipulado indirectamente

Durante el laboratorio se revisaron especialmente binarios poco habituales o innecesarios con este tipo de permisos.

---

# PATH Hijacking

El PATH Hijacking fue uno de los conceptos más importantes trabajados durante el laboratorio.

Este ataque consiste en aprovechar configuraciones inseguras dentro de la variable PATH para conseguir que el sistema ejecute un binario malicioso en lugar del comando legítimo esperado.

El riesgo aparece especialmente cuando:

- existen directorios inseguros dentro de PATH
- hay rutas modificables por usuarios normales
- scripts privilegiados llaman comandos sin ruta absoluta

En este tipo de escenarios un atacante puede introducir un ejecutable malicioso con el mismo nombre que un comando legítimo y conseguir ejecución con privilegios elevados.

Durante las pruebas se analizó la configuración actual mediante:

```bash
echo $PATH
```

---

# Permisos excesivos

También se detectaron riesgos relacionados con permisos demasiado permisivos sobre archivos y scripts del sistema.

El uso incorrecto de permisos `777` o configuraciones similares puede facilitar:

- modificación de scripts críticos
- abuso de configuraciones
- alteración de servicios
- ejecución de contenido no autorizado

Aunque este tipo de errores parecen básicos, siguen siendo bastante frecuentes en entornos mal administrados o configurados rápidamente sin aplicar medidas de seguridad.

---

# Particiones inseguras

Otra parte importante del laboratorio estuvo relacionada con particiones montadas sin medidas básicas de protección.

La ausencia de opciones como:

- noexec
- nosuid
- nodev

puede facilitar ejecución de binarios no autorizados, abuso de permisos especiales o interacción indebida con dispositivos dentro del sistema.

Estas configuraciones resultan especialmente importantes en:

- `/tmp`
- directorios compartidos
- particiones externas
- entornos multiusuario

---

# Variables de entorno inseguras

También se analizaron riesgos relacionados con variables de entorno mal configuradas.

En determinados escenarios, variables manipulables pueden provocar:

- ejecución de comandos no previstos
- carga de librerías maliciosas
- comportamiento inesperado de aplicaciones privilegiadas

Aunque no siempre generan explotación directa, representan una superficie de ataque adicional que debe revisarse dentro de tareas de hardening.

---

# Importancia del principio de mínimo privilegio

Gran parte de los riesgos detectados durante el laboratorio podrían mitigarse aplicando correctamente el principio de mínimo privilegio.

Este principio consiste en conceder únicamente los permisos estrictamente necesarios para realizar una tarea concreta, evitando configuraciones excesivamente permisivas.

Aplicar correctamente este enfoque ayuda a reducir:

- superficie de ataque
- impacto de compromisos
- movimiento lateral
- escalada de privilegios

---

> [!IMPORTANT]
> En muchos ataques reales no es necesario explotar vulnerabilidades extremadamente complejas.  
> Configuraciones inseguras, permisos incorrectos o errores básicos de administración pueden ser suficientes para comprometer completamente un sistema Linux.

---

# Conclusiones

El análisis realizado durante el laboratorio permitió comprender mejor cómo determinadas configuraciones inseguras dentro de Linux pueden facilitar escenarios reales de escalada de privilegios.

Además de aprender técnicas concretas de auditoría, la parte más importante fue entender la importancia del hardening, control de permisos y correcta administración del sistema para reducir riesgos relacionados con abuso de privilegios y ejecución no autorizada.
