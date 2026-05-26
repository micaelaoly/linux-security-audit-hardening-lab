# Análisis de binarios SUID

# Introducción

Durante el laboratorio se revisaron archivos y binarios configurados con permisos SUID dentro del sistema Linux.

Los permisos SUID permiten que determinados programas se ejecuten con privilegios del propietario del archivo, normalmente root, aunque sean ejecutados por usuarios normales.

Aunque este comportamiento es necesario en algunos binarios legítimos del sistema, también representa uno de los vectores más habituales relacionados con escalada de privilegios.

---

# Funcionamiento del bit SUID

Cuando un archivo tiene activo el bit SUID, el proceso se ejecuta con los privilegios del propietario del archivo y no con los permisos del usuario que lo ejecuta.

Ejemplo de permisos SUID:

```bash
-rwsr-xr-x
```

La letra `s` indica que el bit SUID se encuentra activo.

---

# Auditoría realizada

Para localizar binarios SUID dentro del sistema se utilizó:

```bash
find / -perm -4000 2>/dev/null
```

Esto permitió identificar archivos ejecutables con privilegios elevados.

Posteriormente se revisaron especialmente:

- binarios poco habituales
- scripts inseguros
- herramientas innecesarias
- permisos excesivos

---

# Riesgos relacionados con SUID

Los principales riesgos asociados a SUID incluyen:

- escalada de privilegios
- ejecución de comandos privilegiados
- abuso de binarios vulnerables
- ejecución de shells
- bypass de restricciones

Si un binario SUID ejecuta comandos inseguros o utiliza configuraciones incorrectas, puede convertirse en una vía directa para comprometer el sistema.

---

# Mitigaciones aplicadas

Durante el laboratorio se revisaron y eliminaron permisos SUID innecesarios utilizando:

```bash
chmod u-s archivo
```

El objetivo fue reducir superficie de ataque y limitar privilegios únicamente a binarios realmente necesarios.

---

# Conclusiones

El análisis de binarios SUID permitió comprender mejor cómo determinados permisos especiales dentro de Linux pueden facilitar escenarios de escalada de privilegios si no se revisan correctamente.

Además, ayudó a reforzar conocimientos relacionados con auditoría defensiva y hardening de sistemas Linux.
