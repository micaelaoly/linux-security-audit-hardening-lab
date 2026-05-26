# PATH Hijacking y configuraciones inseguras

# Introducción

Durante el laboratorio se analizaron riesgos relacionados con configuraciones inseguras de la variable PATH dentro del sistema Linux.

El PATH es una variable de entorno utilizada para indicar al sistema en qué rutas debe buscar ejecutables cuando se lanza un comando desde terminal o scripts.

Si esta variable contiene directorios inseguros o modificables por usuarios no privilegiados, puede facilitar ataques relacionados con ejecución de binarios maliciosos.

---

# Funcionamiento de PATH

La variable PATH puede visualizarse mediante:

```bash
echo $PATH
```

El sistema revisa las rutas indicadas de izquierda a derecha hasta encontrar el ejecutable solicitado.

Por ello, si existe un binario malicioso con el mismo nombre que un comando legítimo dentro de un directorio inseguro incluido en PATH, podría ejecutarse contenido no autorizado.

---

# Riesgos detectados

Los principales riesgos relacionados con PATH Hijacking incluyen:

- ejecución de binarios maliciosos
- escalada de privilegios
- abuso de scripts privilegiados
- sustitución de comandos legítimos

Estos riesgos aumentan especialmente cuando:

- existen rutas world writable
- scripts usan comandos sin ruta absoluta
- PATH contiene directorios inseguros

---

# Auditoría realizada

Durante el laboratorio se revisaron:

- rutas incluidas en PATH
- permisos de directorios
- scripts privilegiados
- posibles ubicaciones inseguras

También se analizaron escenarios donde un atacante podría introducir ejecutables maliciosos dentro de rutas utilizadas por procesos privilegiados.

---

# Medidas aplicadas

Las principales mitigaciones implementadas fueron:

- restringir permisos sobre directorios
- evitar rutas inseguras
- utilizar rutas absolutas en scripts
- revisar variables de entorno
- aplicar mínimos privilegios

---

# Conclusiones

El análisis de PATH Hijacking permitió comprender cómo configuraciones aparentemente simples pueden facilitar ejecución arbitraria de comandos y escenarios reales de escalada de privilegios dentro de sistemas Linux.
