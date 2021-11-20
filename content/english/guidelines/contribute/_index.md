---
title: Cómo colaborar en un proyecto en GitHub de SALSA
sidebar: auto
tags:
  - contribuir
  - salsa
author: Daniel Cortés Pichardo
---

::: informacion
Si esta es primera vez realizando una colaboración en la comunidad de código abierto, te invitamos a colaborar en el proyecto [Salsa First Contribution](https://github.com/salsa-community/salsa-first-contribution), el cual está pensado para aquellos desarrolladores de software que quieren dar sus primeros pasos en la colaboración de iniciativas de proyectos de código abierto, te esperamos!!!
:::

La colaboración en cualquiera de los repositorios de SALSA, se lleva a cabo a través de un `Pull Request` y siguiendo el flujo de trabajo que se detalla en esta sección:

```flowchart
st=>start: Crear Fork
e=>end: Hacer Pull Request
stage2=>operation: Clonar repositorio
stage3=>operation: Actualizar rama master
stage4=>operation: Crear una rama
stage5=>operation: Hacer cambios

st->stage2->stage3->stage4->stage5->e
```

## Crear Fork del repositorio

El primer paso es hacer un "Fork" del repositorio en el que se quiere participar. Para saber más sobre los Forks, puedes consultar la documentación en [Fork a repo](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

## Clonar el repositorio

Después de tener el repositorio en tu cuenta, debes seleccionar la dirección del repositorio "SSH o HTTP" y clonar:

```shell
$ git clone https://github.com/[tu-usuario]/[nombre-repositorio].git
```

Una vez clonado el repositorio, siempre es recomendable comprobar la URL del repositorio a través del siguiente comando:

```shell
$ git remote -v
```

Antes de realizar cualquier modificación, debes agregar la URL del repositorio original como `upstream`:

```shell
$ git remote add upstream https://github.com/[usuario-original]/[nombre-repositorio-original].git`
```
Comprobar

```shell
$ git remote -v
```

## Actualizar la rama Master

Antes de empezar a trabajar, debes obtener los últimos cambios realizados en el repositorio original:

```shell
$ git pull -r upstream master
```

## Crear una Rama a partir de master para trabajar

Para crear una rama usar la opción "checkout" de git:

```shell
$ git checkout -b feature/nombre-rama
```

## Hacer cambios

Realizar todos los cambios que se desea hacer al proyecto.

Agregar los archivos y hacer un commit

Después de realizar el commit hacer el push hacia tu repositorio, indicando la rama que has creado.

```shell
$ git push origin feature/nombre-rama
```

::: informacion
No olvides agregar tu nombre en el README del proyecto, en la sección de Contribuidores 
:::

## Hacer un Pull Request

Hacer click en `Compare & Pull Request`

Escribir cambios del `Pull Request`.

Si todo está bien, enviar con el botón `Send Pull Request`

Esperar a que el equipo de SALSA lo revise, acepte y una tus cambios en la rama correspondiente.

Para mayor información sobre Pull Request, puedes consultar la documentación oficial de Gihub [Pull Request](https://docs.github.com/es/github/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

