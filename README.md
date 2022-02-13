# score_rnx
Implementación de métrica de calidad rnx de John A. Lee, Michel Verleysen.
Mediante la comparación de un conjunto de datos de alta dimensión y un conjunto de datos de baja dimensión
obtenido por cualquier tipo de algoritmo de reducción de dimensión RD, score_rnx permite obtener la curva rnx

- [Instalación](#instalación)
- [Instrucciones de uso](#instrucciones-de-uso)
- [Créditos](#créditos)
- [Otras referencias sobre Markdown](#otras-referencias-sobre-markdown)


### Instalación
```bash
pip install score_rnx
```

### Instrucciones de uso
La librería está compuesta por diversos módulos como [Coranking](#coranking), [PairwiseDistances](#pairwisedistances), [NXTrusion](#nxtrusion) y [ScoreRnx](#ccorernx)

__ScoreRnx__ es la clase que utiliza los demás módulos para obtener la curva Rnx y un puntaje de calidad del incrustamiento puedes importar e implementar la clase de la siguiente manera

```python
from score_rnx import ScoreRnx

score = ScoreRnx()
```

Puedes obtener la evaluación de ScoreRnx ingresando por contructor los datos de alta y baja dimensión y ejecutando el método __run()__ para realizar el proceso

```python
from score_rnx import ScoreRnx
  
score = ScoreRnx(HD, LD)

score.run()
```
Una vez se haya ejecutado el método tendrá a disponibilidad un lista en el cual se encuentran los resultados de la evaluación
el método __get_rnx()__ permite obtener la lista de evaluaciones disponibles

Cada evaluación tiene dos atributos score y rnx que son el puntaje y la curva generada respectivamente

```python
from score_rnx import ScoreRnx
  
score = ScoreRnx(HD, LD)

score.run()

score_rnx.get_rnx()[0].score  #Puntaje de evaluación
score_rnx.get_rnx()[0].rnx  #Curva de calidad
```

El objeto ScoreRnx permite realizar la evaluación de diversos métodos de reducción y graficarlas

```python
from score_rnx import ScoreRnx
  
score = ScoreRnx()

#Se añaden los datos de alta dimensión
score.add_high_data(HD)

# Se añaden los datos de los métodos de reducción de dimensión 
score_rnx.add_method('CMDS', LD_CMDS)
score_rnx.add_method('LLE', LD_LLE)

# De esta manera __get_rnx()__ tendrá en la posición 0 el resultado de evaluación del 
# método CMDS y en la posición 1 el resultado de evaluación del metodo LLE


score.run()

score_rnx.generate_graph() 
```
El código anterior carga los datos de alta dimensión con el método  add_high_data para luego ingresar los datos generados por los métodos de RD una vez se ejecuta __run()__ puede usarse la función generate_graph() para obtener la gráfica de la curva rnx

