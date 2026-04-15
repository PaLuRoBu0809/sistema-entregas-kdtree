**KD-Tree: Optimización de Búsqueda Espacial para Logística**

Este proyecto consiste en la implementacion desde cero de un **Arbol KD (K dimensional)** para la gestion eficiente de puntos de entrega en un espacio bidimensional. A través de este trabajo, comparamos la eficiencia de estructuras de datos espaciales avanzadas frente a la búsqueda por fuerza bruta, demostrando cómo el algoritmo optimiza procesos logísticos masivos.

El desarrollo fue guiado mediante IA e investigación técnica para la construccion de las diferentes implementaciones que tiene el proyecto.

**Objetivo del Proyecto**
Implementar una estructura KD-Tree robusta capaz de superar las limitaciones de las listas tradicionales fuerza bruta en tareas de:

- Range Search (Búsqueda por Radio): Localizar todos los puntos dentro de una distancia $r$.
- Busqueda de vecinos cercanos (k-NN): Identificar los $k$ vecinos más cercanos de forma eficiente.
- Análisis de Rendimiento: Determinar el umbral de eficiencia donde el árbol KD supera a la búsqueda lineal.

**Estructura del Repositorio**
Aunque la recomendacion fue seguir la estructura dada en el enuciado del laboratorio, se decidio optar por otro tipo de organizacion todo esta en el archivo KDtrees_laboratorio.ipynb pero de manera lineal bien organizada 
y bien documentada donde se explica cada implementacion y pruebas que se solicitan en el laboratorio 
**Se divide en:**
-   Parte 1: Implementacion del arbol KD hecho para K dimensiones y usando coordenadas aleatorias
  
-   Parte 2: Implementacion del Range Search y de la busqueda de vecinos cercanos con ejemplos determinando un centro de busqueda y una cantidad de vecinos mas cercanos
  
-   Parte 3: Creacion de vistas para ver el funcionamiento del arbol en un entorno visual primero en la general solo teniendo una vista general de los datos en el plano y los que estan dentro del rango de busqueda y otra vista para ver los vecinos cercanos.
  
-   Parte 4: Estadisticas donde primero creamos un algoritmo de fuerza bruta para compararlo con el KD-Tree implementando dos pruebas de rendimiento la primera de comparacion de tiempos en numeros de datos grandes para busquedas dentro del rango del radio y para la busqueda de vecinos cercanos, el otro ya es para ver el punto de cruce entre el arbol KD y la Fuerza Bruta

**Implementación Técnica**

**Construcción del Árbol**
El árbol se construye de manera recursiva utilizando un enfoque de mediana de datos para asegurar un balance óptimo:

- Eje de corte: Alterna dinámicamente entre dimensiones ($x, y$) según la profundidad del nivel (profundidad % k).
  
- Punto de división: Se utiliza la mediana (median_low) de los puntos ordenados en el eje actual para particionar el espacio en dos sub-árboles (Izquierda/Derecha).
  
- Complejidad de construcción: $O(n \log n)$.

**Algoritmos de Búsqueda**
#**Búsqueda por Radio**
En lugar de calcular la distancia a cada punto, el algoritmo:

- Evalúa el nodo actual con la distancia euclidiana: $d = \sqrt{(p_x - q_x)^2 + (p_y - q_y)^2} \leq r$.

- Prioriza la rama más cercana al centro de búsqueda.
  
- Poda de ramas: Solo explora la "rama lejana" si existe la posibilidad de que contenga puntos (si la distancia perpendicular al eje de corte es menor al radio).

**Vecino mas cercanos**
Mantiene una lista de los $k$ mejores candidatos. Utiliza la lógica de descarte masivo para ignorar regiones enteras del espacio que están más lejos que el peor candidato actual.

**Análisis de Rendimiento**
Se realizaron pruebas de estrés con hasta 200,000 puntos generados aleatoriamente.

Fuerza Bruta: teniendo una complejidad de $O(n)$ para calculo de range search y calculo del vecino mas cercano, para su construccion tiene uno de $O(1)$

Arbol KD: teniendo una complejidad de $O(n log n)$ para su construccion y para el calculo de vecino mas cercano de $O(log n)$

**El Punto de Cruce**
Tras un análisis exhaustivo en escalas pequeñas (10 a 1,000 puntos), se identificó que:
- N < 100: La Fuerza Bruta es ligeramente más rápida debido a la baja sobrecarga operativa (no hay recursividad ni navegación de nodos).
  
- N > 100: El Árbol KD se vuelve indiscutiblemente superior. A medida que $N$ crece, el tiempo de la fuerza bruta aumenta linealmente, mientras que el KD-Tree se mantiene casi constante (logarítmico).

**Visualización y Verificación**
El proyecto genera visualizaciones clave para validar la lógica espacial:

**Vista general**
Muestra los 10,000 puntos en gris, resaltando en verde los encontrados dentro del radio y delimitando el área de búsqueda con un círculo rojo. Esto confirma que no hay "falsos positivos".

**Zoom de Proximidad**
Un acercamiento al área de interés que traza líneas azules desde el centro hacia los vecinos más cercanos, incluyendo etiquetas de distancia real en metros. Esto valida que la selección de vecinos es matemáticamente exacta.

**Conclusiones**
- La eficiencia escala con los datos para una empresa de logística con 10,000 puntos, usar KD-Tree reduce los cálculos de búsqueda de 10,000 operaciones a aproximadamente 14, generando eficiencia a la hora de buscar datos.
- La estructura importa no siempre el algoritmo KD Trees es el mejor para datos pequeños (menos de 100 puntos) se vio que el Fuerza Bruta dio mejores resultados, pero es vital para la escalabilidad.
- El desarrollo integró investigación técnica autónoma y el uso estratégico de IA para refinar las visualizaciones y optimizar las pruebas de estrés, asegurando un código eficiente y modular.
