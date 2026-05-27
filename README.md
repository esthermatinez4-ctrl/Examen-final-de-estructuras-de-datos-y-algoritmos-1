# Examen-final-de-estructuras-de-datos-y-algoritmos-1
# Planificador de Rutas en una Red de Transporte

# 1. Descripción general

Este proyecto implementa un planificador de rutas basado en una red de transporte modelada como un grafo ponderado.  
El sistema permite:

- Añadir estaciones y conexiones.
- Consultar conexiones directas.
- Calcular la ruta más rápida entre dos estaciones mediante Dijkstra.
- Comprobar si dos estaciones están conectadas mediante BFS.
- Cargar la red desde un archivo TXT.
- Guardar y cargar la red en formato JSON.
- BONUS: Calcular la ruta más rápida pasando por una estación intermedia obligatoria.


# 2. Estructuras de datos utilizadas

# 2.1 Grafo ponderado (lista de adyacencia con diccionarios)

El grafo se almacena como:
```python
{
    "A": {"B": 5.0, "C": 10.0},
    "B": {"A": 5.0},
    ...
}
```

Justificación técnica:
- Representación eficiente para grafos dispersos.
- Acceso a vecinos en O(1) promedio.
- Adecuado para algoritmos como Dijkstra y BFS.
- Permite almacenar pesos (tiempos) de forma natural.


# 2.2 Conjuntos (`set`)

Usados para almacenar nodos visitados en:

- Dijkstra  
- BFS  

Justificación:
- Operación de pertenencia en O(1).
- Evita procesar nodos repetidos.
- Reduce el coste total de los algoritmos.

# 2.3 Cola de prioridad (`heapq`)

Usada en Dijkstra:
```python
heapq.heappush(cola, (distancia, nodo))
```

Justificación:
- Permite extraer el nodo con menor distancia en **O(log V)**.
- Es la implementación estándar de Dijkstra eficiente.

# 2.4 Cola FIFO (`deque`)

Usada en BFS:
```python
cola = deque([origen])
```

Justificación:
- Inserciones y extracciones en **O(1)**.
- Ideal para recorridos en anchura.

# 2.5 Archivos JSON y TXT

- JSON → persistencia de la red entre ejecuciones.  
- TXT → carga inicial de conexiones en formato `origen,destino,tiempo`.

Justificación:
- JSON permite almacenar estructuras complejas (diccionarios).
- TXT facilita la edición manual de la red.

# 3. Complejidad temporal

# 3.1 Añadir conexión

Operaciones:
- Validaciones → O(1)
- Inserción en diccionarios → O(1)

Complejidad total:  
O(1)

# 3.2 Dijkstra (ruta más rápida)
Usando lista de adyacencia + `heapq`:

- Extracción del mínimo → O(log V)
- Relajación de aristas → O(log V)
- Procesa todos los nodos y aristas

Complejidad total:
O((V + E) · log V)

# 3.3 BFS (comprobar conectividad)

Recorre:
- Cada nodo una vez  
- Cada arista una vez  

Complejidad total: 
O(V + E)

# 4. Complejidad espacial

# Grafo (lista de adyacencia)

En un grafo no dirigido:

- Cada nodo ocupa espacio constante.
- Cada arista se almacena dos veces (A→B y B→A).

Complejidad espacial: 
O(V + E)

# 5. Mejoras implementadas

# 5.1 Validación de nombres de estaciones

Evita:
- nombres vacíos  
- nombres con comas  
- espacios innecesarios  

Mejora la robustez del sistema.
# 5.2 Prevención de ciclos triviales

No permite conexiones del tipo:
```
A → A
```

Evita errores lógicos y rutas absurdas.
# 5.3 Dijkstra modular reutilizable

Se creó una función interna:
```python
_dijkstra_camino()
```

que devuelve:
- el camino completo  
- el tiempo total  

Esto evita duplicación de código y permite implementar el bonus.

# 6. BONUS: Ruta más rápida pasando por una estación intermedia

Se añadió una funcionalidad que permite calcular la ruta más rápida:


```
origen → intermedia → destino
```

#  Implementación técnica

Se ejecuta Dijkstra dos veces:

1. `origen → intermedia`  
2. `intermedia → destino`

Luego se concatenan ambos caminos.

# Complejidad temporal

Dijkstra =  


\[
O((V + E)\log V)
\]



Dos ejecuciones =  


\[
O((V + E)\log V)
\]



No aumenta el orden de complejidad.

# Justificación:
- Reutiliza código existente.  
- Es una mejora realista en redes de transporte.  
- Demuestra dominio de algoritmos de caminos mínimos.  
- Es más elegante y algorítmica que la alternativa del “hub”.

# 7. Conclusión
Este proyecto implementa un sistema completo de gestión y análisis de una red de transporte utilizando:

- Diccionarios  
- Sets  
- heapq  
- deque  
- Dijkstra  
- BFS  
- Persistencia en JSON  
- Carga desde TXT  
- Bonus algorítmico  
