# Borrado seguro de información

# Introducción

Durante el laboratorio se trabajó el borrado seguro de archivos utilizando herramientas orientadas a dificultar la recuperación posterior de información sensible.

En Linux, eliminar un archivo normalmente no destruye realmente su contenido, sino únicamente las referencias utilizadas por el sistema de archivos. Esto puede permitir recuperación forense utilizando herramientas especializadas.

Por ello se analizaron técnicas básicas de borrado seguro.

---

# Uso de shred

La principal herramienta utilizada fue:

```bash
shred
```

Ejemplo:

```bash
shred -u archivo.txt
```

Este comando sobrescribe varias veces el contenido del archivo antes de eliminarlo.

---

# Objetivo del borrado seguro

El objetivo principal fue dificultar la recuperación posterior de:

- información sensible
- credenciales
- logs
- documentos
- archivos temporales

---

# Riesgos del borrado tradicional

Un borrado tradicional mediante:

```bash
rm archivo.txt
```

no elimina completamente el contenido físico del archivo, por lo que determinadas herramientas podrían recuperar parte de la información.

---

# Medidas aplicadas

Durante el laboratorio se realizaron pruebas utilizando:

- shred
- secure-delete
- eliminación segura manual

Esto permitió comprender diferencias entre borrado lógico y destrucción orientada a dificultar recuperación forense.

---

# Conclusiones

El análisis relacionado con borrado seguro ayudó a comprender la importancia de proteger correctamente información sensible incluso después de eliminar archivos aparentemente del sistema.
