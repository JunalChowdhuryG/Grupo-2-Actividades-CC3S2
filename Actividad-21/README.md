# **Actividad 21: Patrones para módulos de infraestructura**

| Integrante                         | Codigo    | GitHub                                                                  |
| ---------------------------------- | --------- | ----------------------------------------------------------------------- |
| Chowdhury Gomez, Junal Johir       | 20200092K | [JunalChowdhuryG](https://github.com/JunalChowdhuryG/Actividades-CC3S2) |
| La Torre Vasquez, Andres Sebastian | 20212100C | [Jun1el](https://github.com/Jun1el/Desarrollo-de-Software-25-1)         |
| Zapata Inga, Janio Adolfo          | 20212636K | [Janiopi](https://github.com/Janiopi/Actividades-CC3S2)                 |


## **Fase 1: Exploración y análisis**

### **1. Singleton**
#### Tarea: Explica cómo `SingletonMeta` garantiza una sola instancia y el rol del `lock`.

* `_instances` es un diccionario que utiliza `SingletonMeta` que lo utiliza para guardar la unica instancia de cada clase:
    ```python
    _instances: Dict[type, "ConfigSingleton"] = {}
    _lock: threading.Lock = threading.Lock()  # Controla acceso concurrente
    ```
* `__call__` comprueba si la clase tiene una instancia en el 
diccionario `_instances`. En el caso que existiera lo devuelve y en el caso de que no existiera lo crea y lo guarda
    ```python
    def __call__(cls, *args, **kwargs):
        with cls._lock:
            if cls not in cls._instances:
                cls._instances[cls] = super().__call__(*args, **kwargs)
            return cls._instances[cls]
    ```
* el `_lock` asegura que en entornos multihilo no se creen multiples instancias por condiciones de carrera 
Ya que sin `lock` dos hilos podrian verificar `cls not in cls._instances` a la vez y crear dos instancias pero si se utiliza `with cls._lock:` solo un hilo ejecuta el bloque a la vez y esto garantiza que el segundo hilo espere y utilice la instancia creada por el primero

### **2. Factory**


### **3. Prototype**


### **4. Composite**


### **5. Builder**


## **Fase 2: Ejercicios prácticos**