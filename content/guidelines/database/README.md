---
sidebar: auto
tags:
  - guidelines
  - postgresql
author: Daniel Cortés Pichardo
---

# Lineamientos para PostgreSQL

![Arquitectura Salsa](/assets/img/salsa-database.png)

Los lineamientos descritos en este documento se centran principalmente en la plataforma :SALSA: y las bases de datos de [PostgreSQL] 12 y [Oracle]


## Utilizar minúsculas

Todos los nombres deben ser escritos en minúsculas; esto incluye, nombre de tablas, vistas, columnas, y procedimientos almacenados.

::: ejemplo
Utilizar `primer_apellido`, en lugar de `PRIMER_APELLIDO` o `Primer_Apellido`.
:::

## No utilizar el tipo de dato como nombre.

Los tipos de datos no son nombres. Los nombres de objetos particularmente columnas, deberán de ser nombrados por un sustantivo, evitando utilizar palabras que son únicamente para el uso de la definición de un tipos de datos: por ejemplo, no se pueden llamar `text` or `timestamp`.

::: ejemplo
Utilizar `create_by`, en lugar de `create_timestamp` o `timestamp`.
:::

## Utilizar guión bajo (_) para separar nombres que tengan más de una palabra.

Los nombres de objetos que se componen de varias palabras, deben estar separados por `guiones bajos`; siguiendo el estilo [snake case](https://en.wikipedia.org/wiki/Snake_case).

::: ejemplo
Utilizar `primer_apellido`, en lugar de `primerApellido` o `primerapellido` .
:::

## Utilizar nombres en singular para tablas.

Los nombres de las tablas deben escribirse en singular, por ejemplo, `proyecto` en lugar de `proyectos`. 

Esta regla es aplicable porque las tablas son patrones para almacenar una entidad como un registro; son análogos a las clases que se definen en un lenguaje de programación orientado a objetos.

## Utilizar palabras completas para los nombres de elementos.

Utilizar palabras completas en lugar de abreviaturas; a menos que la palabra se pueda representar a través de alguna [Abreviatura común](#utilizar-abreviaturas-comunes). Los nombres para describir objetos de negocio deben ser escritos en Español. 

En general, se debe evitar el uso de abreviaturas. [PostgreSQL] soporta hasta [63 caracteres para identificadores](https://www.postgresql.org/message-id/005001c39897%243937fcc0%243e00a8c0%40venus).

::: ejemplo
Utilizar `segundo_apellido`, en lugar de `seg_apellido` o `seg_ap` .
:::


## Utilizar abreviaturas comunes para nombres.

Utilizar abreviaturas comunes en lugar de la palabra completa. Para algunas palabras, es más común ver la abreviatura que la palabra. 

::: ejemplo
Utilizar `i18n`, en lugar de `internationalization`.
Utilizar `l10n`, en lugar de `localization`.
Utilizar `descripcion_en`, en lugar de `descripcion_english` para denotar el lenguaje.
:::

Si existe duda, entonces se deberá de utilizar la palabra completa en español. Debería de ser obvio cuando la abreviatura tiene sentido.


## Utilizar palabras en inglés para campos especiales.

Para nombrar elementos que tengan que ver con aspectos de arquitectura (seguridad, bitácora,mantenibilidad, etc) se deberán de utilizar palabras en inglés, permitiendo diferenciar los elementos de negocio de los que pertenecen a aspectos más técnicos.

::: ejemplo
Utilizar `last_modified_by` en lugar de `modificado_por`.
Utilizar `create_date` en lugar de `fecha_de_creacion` o `fecha_creacion`.
:::

Para nombrar columnas que sean de tipo `boolean`, se deberá de utilizar el prefijo `is_`.

## No utilizar palabras reservadas para nombres.

Se deberá de evitar el uso de palabras reservadas en la base de datos.

::: ejemplo
Evita utilizar palabras como `user`, `lock` o `table`.
:::

(Palabras reservadas para PostgreSQL)[https://www.postgresql.org/docs/9.3/sql-keywords-appendix.html]

(Palabras reservadas para Oracle)[https://docs.oracle.com/database/121/SQLRF/ap_keywd.htm#SQLRF022]

## Nombrar llaves primarias de una columna con `id`.

Todas las tablas que tengan una única llave primaria, deberá de llamarse `id`.

::: ejemplo

utilizar:
```sql
CREATE TABLE proyecto (id bigint PRIMARY KEY);
```

en lugar de 

```sql
CREATE TABLE proyecto (proyecto_id bigint PRIMARY KEY);
```
:::


## Nombrar llaves foráneas por su referencia.

Las llaves foráneas deberán de ser una combinación del nombre de la tabla a la que se hace referencia y el nombre de la columna referida. `[TABLA_REFERIDA]_[COLUMNA_REFERIDA]`

Para el caso de llaves foráneas que hacen referencia a una tabla con llave primaria simple, el nombre deberá de ser siempre `[TABLA_REFERIDA]_id`.

El nombre del `CONSTRAINT` deberá de cumplir con fk_[TABLA_BASE]_[TABLA_REFERIDA]_id.

::: ejemplo

Utilizar

```sql
CREATE TABLE proyecto (
  id            bigint PRIMARY KEY,
  modalidad_id  bigint NOT NULL,
  CONSTRAINT fk_proyecto_modalidad_id FOREIGN KEY (modalidad_id) REFERENCES modalidad(id));
```

En lugar de 

```sql
CREATE TABLE proyecto (
  id            bigint PRIMARY KEY,
  id_modalidad  bigint NOT NULL,
  CONSTRAINT fk_proyecto_modalidad_id FOREIGN KEY (id_modalidad) REFERENCES modalidad(id));
```
:::

## Evitar el uso de prefijos y sufijos.

No se debe utilizar `prefijos` o `sufijos` para nombrar elementos dentro la base de datos, a menos que se consideren necesarios para ayudar a organizar tablas en grupos relacionados o distinguirlos de otras tablas no relacionadas. Generalmente hablando, los prefijos harán que se tenga que escribir caracteres innecesarios.

Entre los ejemplos típicos en donde no se debe utilizar prefijos, se encuentran los siguientes:

* Para distinguir tipos de elementos: tabla (`TB_`), vista (`VW_`), procedimientos almacenados (`SP_`), catálogos (`CAT_`), entre otros.
* Para identificar aplicaciones: `registro_usuario`, `evaluacion_usuario`.
* Para identificar tipos de datos: `descripcion_tx`, `monto_aprobado_dbl`, `fecha_ministracion_dt`.

::: nota
Esta regla no aplica, para los componentes de seguridad que se utilizan dentro de un microservicio, en donde se debe de distinguir la base de datos que se utiliza para dar acceso a usuarios y que no forman parte del negocio. Para estos elementos se utiliza el  sufijo `core_`
:::

Los únicos prefijos que están permitidos, son los siguientes:


## Nombrar índices de manera explícita.

Se deberá describir explícitamente la tabla y las columnas que está haciendo referencia y seguir la nomenclatura de 
`[TABLA_BASE]_ix_[COLUMNA_1]_[COLUMNA_2]...`


## Utilizar columnas para auditoría.

Todas las tablas que son altamente transaccionales, deberán de contar con cuatro columnas para el registro de cambios en sus registros:


| Columna              | Tipo de dato   | Descripción                               |
|----------------------|:--------------:| ------------------------------------------|
| create by            |   [varchar]    | usuario que creó el registro            |
| create date          |   [timestamp]  | fecha de creación del registro          |
| last_modified_by     |   [varchar]    | último usuario que modificó el registro |
| last_modified_date   |   [timestamp]  | fecha de última modificación            |


[varchar]:https://www.postgresql.org/docs/12/datatype-character.html
[timestamp]:https://www.postgresql.org/docs/12/datatype-datetime.html
[PostgreSQL]:https://www.postgresql.org/docs/12/index.html
[Oracle]:https://www.oracle.com/technetwork/es/database/enterprise-edition/documentation/database-091505-esa.html
