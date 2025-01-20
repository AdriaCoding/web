---
title: "03 - OLAP y el Modelo Multidimensional"
date: 2025-01-15
meta-title: "OLAP y el Modelo Multidimensional en Data Warehousing"
description: "Resumen del tercer tema de la asignatura Data Warehousing"
image: "/images/datawarehouse.jpg"
categories: ["Data Warehousing"]
tags: ["Lecture Notes"]
draft: false
---
Las herramientas de On-Line Analytical Processing (OLAP), focalizadas en servir consultas o *queries* del usuario de forma rápida, segura y concurrente, se basan en el modelo de datos multidimensional.

## Qué es el modelo multidimensional?
El fundamento de el modelo multidimensional es representar la información mediante la  dicotomía *fact* / *dimension*. 
 - El **fact** es el sujeto de análisis, por ejemplo: *Ventas*, *Estado del pedido*, *Ratio*, etc. Cada dato representa una celda en el interior del cubo de la figura más abajo.
 - Las **dimensions** son las diferentes perspectivas de análisis del sujeto, por ejemplo: *Fecha*, *Localidad*, *Categoría*, etc. Cada dimensión es una arista del cubo.  

![Visión multidimensional de datos](/datawarehousing/3-datacube.png)

Las dimensiones suelen tener una jerarquía de niveles, por ejemplo: *Barrio < Ciudad < País < Continente < TODOS*. En el nivel más bajo se encuentran los facts como **datos atómicos**, i.e., con el nivel de granularidad más bajo. Podemos ir subiendo de nivel agregando los facts, hasta alcancar el nivel *TODOS*.

### Comparación con el modelo relacional
Cuando se piensa en cómo es una base de datos, solemos pensar en el modelo relacional aunque de hecho ambos son compatibles. Empecemos viendo las diferencias


|        | Modelo Relacional                                                                 | Modelo Multidimensional                                                                 |
|----------------------|-----------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| **Estructura**       | Tablas relacionadas. | Cubos multidimensionales.               |
| **Normalización**    | Los datos se normalizan para reducir la redundancia y asegurar la integridad.     | Los datos a menudo se desnormalizan para mejorar el rendimiento de las consultas.       |
|**Ejemplo** | ![UML relacional](/datawarehousing/3-relational.png)| ![UML multidimensional](/datawarehousing/3-datacube.png)
| **Operaciones de datos**        | Facilita inserciones y modificaciones, ya que no hay necesidad de tocar muchos registros por una sola modificación. |  Aligera la velocidad de las consultas, ya que que requiere menos JOINs. También és más sencillo para el usuario. |
| **Uso**              | Transaccional (OLTP) | Análisis (OLAP)                   |

Los DBMS usan internamente el modelo relacional, y desdpués se implementa una capa de OLAP intermedia con el modelo multidimensional, para las queries dirigidas hacia el *front-end*.

## Esquemas multidimensionales
El modelo multidimensional se implementa mediante un esquema relacional de datos, con dos restricciones adicionales:
1. Cada tabla contendrá información de tipo *fact* (**F**) o de tipo *dimension* (**D**).
2. Las relaciones entre tablas **D** - **F** son siempre 1-* (*one-to-many*).

Con estas características, se distinguen tres tipos de esquemas multidimensionales:

### Star Schemas
Hay una única tabla *fact* central, y todas las *dimension* se relacionan con ella. Las dimensiones estan **desnormalizadas**, es decir, que todos los niveles jerárquicos se representan en la misma.

![Ejemplo star schema](/datawarehousing/3-star.png)

Por ejemplo, la tabla *Advertising Agency* puede contener columnas *City* y *Country*, que representan estos niveles de jerarquía superiores. Désomonos cuenta de que en estas columnas habrá muchos valores repetidos, algo malo desde la perspectiva transaccional. Sin embargo, esto mejora la velocidad de las consultas, ya que la alternativa sería poner *City* y *Country* en otras tablas, y eso implicaría realizar más *joins*.

### Snowflake Schemas
En este modelo también hay una única *fact* central, con la diferencia de que las *dimension* están **normalizadas**.

![Ejemplo snowflake schema](/datawarehousing/3-Snowflake.png)

En comparación con el *star schema*, aquí se sacrifica rendimiento en las consultas, a cambio de tener menor redundancia de datos y menor coste de mantenimiento.

### Gallaxy Schemas
Este es el caso en que hay varios *fact* con *dimension* compartidas. Esto ofrece la posibilidad de análisis más detallados, mediante la operacion de *drill-across* que veremos más adelante.

![Ejemplo gallaxy schema](/datawarehousing/3-gallaxy.png)