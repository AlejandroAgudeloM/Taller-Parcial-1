# Taller: POO y Modificadores de Acceso en Python  

Este repositorio contiene un taller práctico sobre **Programación Orientada a Objetos (POO)** en Python, enfocado en el uso de convenciones de acceso (`público`, `protegido`, `privado`) y la encapsulación con `@property`.  

El material incluye ejercicios resueltos que muestran cómo funcionan las convenciones de Python frente a otros lenguajes como Java o C++, así como buenas prácticas de diseño orientado a objetos.  

---

## 📚 Contenido  

### Parte A. Conceptos y lectura de código
1. Atributos públicos, protegidos y privados (name mangling).  
2. Uso de `hasattr` para detectar atributos.  
3. Preguntas de verdadero/falso sobre convenciones de acceso.  
4. Lectura de código con herencia y atributos protegidos.  
5. Name mangling en herencia.  
6. Restricciones con `__slots__`.  
7. Atributos protegidos por convención (`_atributo`).  
8. Métodos privados y `hasattr`.  
9. Acceso a atributos privados con name mangling.  
10. Uso de `dir()` para detectar atributos mangled.  

### Parte B. Encapsulación con `@property` y validación
11. Validación de saldos no negativos.  
12. Propiedades de solo lectura (ej. conversión Celsius a Fahrenheit).  
13. Validación de tipos en atributos (`str`).  
14. Exposición de colecciones en solo lectura (listas → tuplas).  

### Parte C. Diseño y refactor
15. Validación de rango en atributos (ej. `velocidad`).  
16. Cuándo usar `_atributo` vs `__atributo` en APIs públicas.  
17. Corrección de fuga de encapsulación en métodos que exponen listas.  
18. Problemas de name mangling en herencia y cómo solucionarlos.  
19. Uso de composición y fachada para exponer solo métodos seguros.  
20. Mini-kata: `ContadorSeguro` con atributo protegido, propiedad de solo lectura y método privado de logging.  

---

## 🛠️ Tecnologías utilizadas  
- **Python 3.10+** (compatible con cualquier versión moderna de Python 3).  
- Ejecuciones recomendadas en:  
  - **Jupyter Notebook** para pruebas rápidas.  
  - **VS Code** o **PyCharm** para edición y depuración.  

---

## 🚀 Uso  
1. Clona el repositorio:  
   ```bash
   git clone https://github.com/tu_usuario/taller-poo-python.git
   cd taller-poo-python
   ```

2. Abre los archivos `.py` o el PDF con enunciados y soluciones.  

3. Ejecuta ejemplos:  
   ```bash
   python ejercicios.py
   ```

---

## 🎯 Objetivos de aprendizaje  
- Comprender cómo Python maneja el encapsulamiento mediante **convenciones** y **name mangling**.  
- Aplicar `@property` para crear atributos seguros y controlados.  
- Diseñar clases siguiendo buenas prácticas de **POO**.  
- Reconocer las diferencias con otros lenguajes (Java, C++).  

---

## 📄 Licencia  
Este proyecto se distribuye bajo la licencia MIT. Puedes usarlo y adaptarlo libremente citando la fuente.  
