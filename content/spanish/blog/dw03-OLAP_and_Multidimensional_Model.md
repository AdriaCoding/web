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
El *fact* es el sujeto del análisis. En geeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee

![Visión multidimensional de datos](/datawarehousing/3-datacube.png)

Distingámoslo del modelo relacional:


|        | Modelo Relacional                                                                 | Modelo Multidimensional                                                                 |
|----------------------|-----------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| **Estructura**       | Tablas relacionadas. | Cubos multidimensionales.               |
| **Normalización**    | Los datos se normalizan para reducir la redundancia y asegurar la integridad.     | Los datos a menudo se desnormalizan para mejorar el rendimiento de las consultas.       |
|**Ejemplo** | ![UML relacional](/datawarehousing/3-relational.png)| ![UML multidimensional](/datawarehousing/3-datacube.png)
| **Operaciones de datos**        | Facilita inserciones y modificaciones, ya que no hay necesidad de tocar muchos registros por una sola modificación. |  Aligera la velocidad de las consultas, ya que que requiere menos JOINs. También és más sencillo para el usuario. |
| **Uso**              | Transaccional (OLTP) | Análisis (OLAP)                   |

