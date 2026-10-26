# Kit de Herramientas de Estimaciones de Organización Industrial

![Spatial Competition Map](Los_Angeles_Map.jfif)
*(Leyenda: Visualización de la concentración espacial del mercado generada por `spatial_competition.py`)*

## 📊 Resumen Ejecutivo (Valor de Negocio)

Este repositorio proporciona un kit de herramientas basado en Python para automatizar y escalar análisis económicos utilizados en **estrategias de precios, consultoría antimonopolio y competencia de mercado**.

Lleva los análisis que comúnmente se realizan en hojas de cálculo a Python, de modo que sean replicables y rápidos de volver a ejecutar cuando cambian los supuestos o los datos. Los scripts abordan problemas típicos de organización industrial: sensibilidad de la demanda y del precio, concentración de mercado, impacto de fusiones y competencia espacial.

## 💻 Estructura del Repositorio

* `segmented_elasticities_blp.py`: Estima las elasticidades precio propio por segmento de ingresos con un logit de coeficientes aleatorios BLP (`pyblp`), un logit base de Mínimos Cuadrados en Dos Etapas (2SLS) y rangos de bootstrap.
* `NEIO/`: Contiene conjuntos de datos y scripts para estimar y graficar funciones de demanda y costo marginal bajo varias formas funcionales. NEIO significa *Nueva Organización Industrial Empírica* (por sus siglas en inglés), un enfoque que estima la demanda y los costos marginales a partir de los precios y cantidades observadas en el mercado (el conjunto de datos aquí es puramente ficticio, generado para una descripción general inicial).
* `concentration.py`: Evalúa la concentración del mercado utilizando métricas estándar de la industria (p. ej., HHI).
* `mergers_and_acquisitions.py`: Simula escenarios de fusiones y adquisiciones (M&A) para proyectar cambios en la participación y estructura del mercado.
* `spatial_competition.py`: Modela la competencia espacial utilizando la obtención automatizada de conjuntos de datos y herramientas de visualización geoespacial (ver mapa arriba).
* `network_effects.py`: Evalúa las externalidades de red (utilizando datos de ventas de videojuegos) para comprender la dinámica de adopción de productos.
* `rejoinder_to_graddy_1995.py`: Analiza los datos del mercado de pescado de Fulton (Graddy, 1995) utilizando variables instrumentales (VI / IV) para estimar las curvas de demanda.

## 🎯 Del Código a las Preguntas de Negocio

| Pregunta de negocio | Script | Aplicación típica |
| --- | --- | --- |
| ¿Cuánto reaccionan los clientes a un cambio de precio y difiere por grupo de clientes? | `segmented_elasticities_blp.py` | Estrategia de precios, diseño de descuentos |
| ¿Cómo responde la demanda al precio y cuánto cuesta abastecerla? | `NEIO/` | Fijación de precios, análisis de márgenes |
| ¿Qué tan concentrado o competitivo es un mercado? | `concentration.py` | Evaluación de mercado, benchmarking competitivo |
| ¿Una fusión le daría a la empresa combinada margen para subir los precios? | `mergers_and_acquisitions.py` | Due diligence de fusiones y adquisiciones, consultoría antimonopolio |
| ¿Dónde se ubican las tiendas de la competencia y quién domina cada área? | `spatial_competition.py` | Ubicación de tiendas, planificación de expansión |
| ¿Un producto se vuelve más valioso a medida que más personas lo usan? | `network_effects.py` | Estrategia de adopción de productos y plataformas |
| ¿Es confiable una estimación de la demanda cuando los precios y las ventas se influyen mutuamente? | `rejoinder_to_graddy_1995.py` | Cualquier estimación de demanda a partir de datos de ventas |

## 📈 Resultados de Ejemplo

### Precios por segmento de clientes (`segmented_elasticities_blp.py`)

Utilizando datos del mercado de cereales de EE. UU. (Nevo, 2000), el script estima qué tan sensible al precio es cada segmento de ingresos:

|  | Elasticidad precio propio | Intervalo del 90% (200 muestras de bootstrap) |
| --- | --- | --- |
| Ingresos más altos | -2.87 | 2.52 a 3.10 |
| Ingresos más bajos | -4.50 | 3.73 a 4.97 |

**Qué significa:** un aumento de precio del 1% reduce la demanda en un 4.50% en el segmento de ingresos más bajos, frente a un 2.87% en el de mayores ingresos. El segmento de ingresos más bajos resultó ser el más sensible al precio en el 100% de las simulaciones. Cobrar a cada segmento su propio precio mejora las ganancias entre un 0.7% y un 7.4% (percentil 5 al 95 de las simulaciones).

### Evaluación de fusiones (`mergers_and_acquisitions.py`)

En el mismo conjunto de datos, la demanda se estima con variables instrumentales (2SLS): elasticidad precio propio promedio de -4.49 y elasticidad precio cruzada de 0.09. Para una fusión hipotética entre dos empresas en los datos, el GUPPI (un indicador de cuánto desearía subir los precios la empresa fusionada) resulta ser del 0.51%, muy por debajo del umbral de alerta del 5%. En términos sencillos, este modelo simple encuentra pocos incentivos para que la empresa fusionada aumente los precios.

*Ejercicios estilizados sobre datos de EE. UU., no estimaciones para Argentina. El ejemplo de la fusión utiliza un logit simple por diseño, el cual asume la independencia de alternativas irrelevantes; un modelo BLP completo relaja esa suposición.*

## Requisitos

El proyecto se basa en bibliotecas estándar de ciencia de datos y econometría en Python, incluyendo `pandas`, `statsmodels`, `linearmodels`, `scipy` y `pyblp`.

Para instalar las dependencias exactas, ejecuta el siguiente comando en la terminal:

```bash
pip install -r requirements.txt

```
