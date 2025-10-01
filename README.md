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

## 📝 Respuestas Taller
1. A, B y D
2. False True ya que la función hasattr() revisa si el objeto tiene o no un atributo con ese nombre y el nombre del atributo se vuelve el segundo por name mangling.
3. a.) Falso: el prefijo “_” solo es una convención dentro de python que no impide el acceso. 
   b.)Falso: el prefijo “__” activa el name mangling, cambiando el nombre del atributo para hacerlo más difícil de acceder pero no imposible. 
   c.)Verdadero: Ya que como el name mangling utiliza el nombre de la clase antes del atributo, cambia dependiendo del nombre de la clase.
4. Se imprime “abc” ya que el prefijo _ en el atributo self._token solo es una convención y no impide el acceso.
5. (2, 1)
6. "y" nunca fue definido en __slots__ de la clase Caja
7. El nombre correcto del atributo es self._numero
8. True, False, True siguiendo la lógica del punto 2, _step si se puede acceder ya que solo está protegido, mientras que __tick al ser privado pasa por name mangling, por lo que se convierte en _M__tick
9. print(‘s._S__data’)
10. _D__a es el más probable ya que __a pasa por name mangling, por lo cual no se va a encontrar y el atributo a es privado+
11. 
```
 class Cuenta:  
       def __init__(self, saldo):  
           self._saldo = 0  
           self.saldo = saldo  
       @property  
       def saldo(self):  
         return self._saldo 
       @saldo.setter  
       def saldo(self, value):  
       # Validar no-negativo  
          if value < 0:  
           raise ValueError("El saldo no puede ser negativo")  
          self._saldo = value
```
12.
```
 @property  
 def temperatura_f(self):  
   return self._c * 9/5 + 32
```
13.
```
class Usuario:  
 def __init__(self, nombre):  
 self.nombre = nombre  
 # Implementa property para nombre 
 @property 
 def nombre(self): 
     return self._nombre 
 
 @nombre.setter 
 def nombre(self, value): 
     if not isinstance(value, str): 
         raise TypeError("El nombre debe ser una cadena (str)") 
     self._nombre = value
```
14.
```
@property 
def items(self): 
    return tuple(self.__items)
```
15.
```
@property 
def velocidad(self): 
    return self._velocidad 
 
@velocidad.setter 
def velocidad(self, value): 
    if not (0 <= value <= 200): 
        raise ValueError("La velocidad debe estar entre 0 y 200") 
    self._velocidad = value
```
16. _atributo lo utilizaría para definir que el atributo es interno, pero para no esconderlo completamente, y permitiendo que sea utilizado por cualquiera bajo su propio riesgo. En cambio __atributo lo usaria para reducir el riesgo de que otra subclase defina un atributo con el mismo nombre y se dañe el código sin querer.
17. El método get_data devuelve la lista interna directamente. Eso significa que desde fuera alguien puede modificarla y alterar el estado interno del objeto sin pasar por ningún control
```
class Buffer:  
    def __init__(self, data):  
        self._data = list(data)  
 
    def get_data(self):  
        return tuple(self._data)
```
18. self.__x = 1 se guarda como self._A__x, y en B.get, al pedir self.__x python aplica el name mangling para B, y busca self._B__x que no existe. 
Para arreglarlo, como se piensa heredar el atributo, es mejor usar la convención self._x para proteger el atributo, pero que pueda ser heredado.
19.
```
def guardar(self, k, v): 
  self.__repo.guardar(k, v)
```
20.
```
class ContadorSeguro: 
    def __init__(self): 
        self._n = 0   #atributo “protegido” 
    def inc(self): 
        self._n += 1  #suma 1 
        self.__log() 
 
    @property      #propiedad de solo lectura 
    def n(self): 
        return self._n 
 
    def __log(self):  #metodo “privado”  
        print("tick") 
 
 
# Uso básico 
c = ContadorSeguro() 
c.inc()   # tick 
c.inc()   # tick 
 
print("Valor final:", c.n)
```
---

## 📄 Licencia  
Este proyecto se distribuye bajo la licencia MIT. Puedes usarlo y adaptarlo libremente citando la fuente.  
