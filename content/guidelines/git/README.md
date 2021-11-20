---
subSidebar: true
tags:
  - vista
  - paradigma
  - enfoque
  - perspectiva
author: Daniel Cortés Pichardo
---

# Introducción

Los lineamietos aquí expuestos son una extensión de [A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model)

Explicar el modelo de desarrollo y control de versión de código para los desarrollos en el **CONACYT**

El modelo de desarrollo explicado aquí puede variar de acuerdo a las necesidades específicas de cada proyecto, sin embargo el modelo general de desarrollo considera diferentes flujos trabajo que pueden adaptarse a las necesidades específicas. El modelo de trabajo, sólo para equipos que se encuentren gestionando su código con la herramienta **Git**.

## Roles y actividades

El flujo de trabajo consta de la definición de los siguientes elementos:

1. Roles
2. Actividades

### Roles

El modelo de desarrollo involucra dos roles; **master** y **develop**, mismos que se describen a continuación:

**Master**

> Principalmente, este rol será el encargo de llevar a cabo la integración del sistema, además de las siguientes responsabilidades:
>
> 1. Llevar a cabo las operaciones de integración entre la rama origin/develop y origin/master.
> 2. Verificar que los números de versiones en la rama master respetan el versionamiento [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).
> 3. Identificar inconsistencias entre la nueva versión y anteriores.

**Developer**

> En cada proyecto se puede contar con 1 o más roles de este tipo y sus principales actividades son:
>
> 1. Participar en la construcción de nuevas funcionalidades sobre un sistema de software.
>
> 2. Construir software de calidad de acuerdo a los estándares definidos en la organización.
>
> 3. Participar en las tareas de integración cuando estas sean solicitadas por el rol master.

### Actividades

Las actividades que se llevan a cabo en el modelo de desarrollo se ilustran en la siguiente gráfica:

![](/assets/img/git/diagram.png)


## Descripción de una rama

::: informacion
En *Git* las ramas son espacios o entornos independientes para que un Desarrollador sea Back-end, Front-end, Tester, etc. pueda usar y así trabajar sobre un mismo proyecto sin cambiar o borrar el conjunto de archivos originales del proyecto, dándonos flexibilidad para desarrollar nuestro proyecto de manera mas organizada.
:::


### Metadatos

Con la finalidad de comprender de manera precisa el estudio de las diferentes ramas de trabajo utilizados en el **CONACYT**, a continuación se presenta la descripción de la meta-información que define a cada una de las ramas y que será utilizado a lo largo de este documento:

| Metadato | Descripción |
| --- | --- |
| Descripción | Descripción básica de la rama en cuestión. |
| Rama de la que bifurca | Nombre de la rama que bifurcó. |
| Rama con la que se une | Nombre de la rama a la que se une cuando se ejecuta una operación de tipo merge. |
| Convención de nombrado | Convención de nombrado que aplica para la rama. |
| Lineamiento | Consideraciones para el buen uso de la Rama. |
| Diagrama | Diagrama explicativo sobre el uso de la rama. |
| Comandos | Comandos sugeridos para la creación, modificación, unión y eliminación de la rama. |


## Rama Master

### Descripción

La rama **master**, por convención, será la rama principal del proyecto. En esta rama se encuentran las versiones productivas del sistema y que se han liberado a producción.

### Rama de la que bifurca

`Ninguna`

### Rama con la que se une

`Ninguna`

### Convención de nombrado

Esta rama **siempre** se llama `master`

### Lineamientos

1. No está permitido subir “código roto” a la rama master.
2. El código que se suba a master deberá de ser cuidadosamente probado antes de ser integrado; se sugiere utilizar el branch _release_ antes de que una nueva liberación se lleve a cabo a la rama **master**.
3. Sólo el **rol master** puede ejecutar la operación de `push/merge` a esta rama.
4. Esta rama **nunca** se deberá de borrar.

### Diagrama

![](/assets/img/git/branch-develop.png)

### Comandos

`[NO APLICA]`


## Rama Develop

### Descripción

La rama **develop**, por convención, será la rama secundaria del proyecto. En esta rama, el equipo de desarrollo se encuentra trabajando día con día una nueva versión del sistema.

### Rama de la que bifurca

`master`

### Rama con la que se une

`master`

### Convención de nombrado

Siempre se llamará `develop`

### Lineamientos

### Diagrama

![](/assets/img/git/branch-develop.png)

### Comandos

`[NO APLICA]`


## Rama Feature

### Descripción

La rama de características “**feature**” es utilizada para desarrollar nuevas características o funcionalidades que vendrán en las próximas o futuras entregas. Esta rama se crea cuando se comienza a desarrollar una nueva característica de la cual se desconoce la fecha de entrega. La esencia de esta rama es que exista durante el periodo de tiempo en que tome desarrollar la nueva característica. Eventualmente, esta rama se unirá a la rama de desarrollo **develop** \(para agregar de manera definitiva la nueva característica en la próxima entrega\) o se eliminará \(en caso de que la nueva característica no cumpla con los objetivos deseados\).

### Rama de la que bifurca

`develop`

### Rama con la que se une

`develop`

### Convención de nombrado

El nombrado de esta rama se deberá de apegar a lo establecido en \[AGIS\] y la propuesta en esta sección:

Nomenclatura Adicional:`feature-*`

Ejemplo:

* feature-seguridad
* feature-carrusel

### Lineamientos

1. Sólo existe en el repositorio local, nunca en el remoto **origin**

### Diagrama

![](/assets/img/git/branch-features.png)

### Comandos

Crear una rama `feature` a partir de la rama `develop` se deberá de hacer lo siguiente:

```bash
git checkout -b feature-seguridad develop
```

Una vez que se a trabajo en la nueva rama, para actualizar los cambios en la rama `develop` primero tenemos que regresar a la rama `develop` y partir de allí llevar a cabo la operación `merge`:

```bash
git checkout develop
```

Unir las modificaciones hechas en la rama `feature` dentro de la rama `develop`:

```bash
git merge --no-ff feature-seguridad
```

A continuación, se deberá de borrar la rama `feature-seguridad`:

```bash
git branch -d feature-seguridad
```

Finalmente, se envian los cambios a la rama remota `develop`

```bash
git push origin develop
```
## Rama Release

### Descripción

La rama “**release**” se debe utilizar para la preparación de una nueva entrega en el ambiente de producción. Esta rama es útil para corregir pequeños defectos y preparar los metadatos que deberá llevar la próxima entrega \(número de versión, fecha de compilación, etc.\). El beneficio de tener una rama de entrega **release** radica en el hecho de que podemos conservar la rama **develop** limpia y lista para recibir nuevas versiones que se tendrán que integrar a la rama **master**. Adicionalmente, la rama **release** será utilizada por el equipo de **QA** para probar la entrega antes de que esta llegue a producción.

### Rama de la que bifurca

`develop`

### Rama con la que se une

* `develop`
* `master`

### Convención de nombrado

El nombrado de esta rama se deberá de apegar a lo establecido en \[AGIS\] y la propuesta en esta sección:

Nomenclatura obligatoria: `release-*`

Ejemplo:

* `release-seguridad`
* `release-carrusel`

### Lineamientos

1. El mejor momento para crear una ramificación de develop es cuando el desarrollo refleja el estado deseado de una nueva entrega.

2. Todas las funcionalidades o características que se esperan mostrar en la próxima entrega deberán de unirse a la rama de develop.

3. Es exactamente al comienzo de la creación de esta rama en que se asigna una versión. Es hasta ese momento que la rama develop refleja los cambios para la siguiente entrega, pero no es claro si esa nueva entrega eventualmente se convertirá en la versión 0.3 o 1.0. La notación para el versionamiento de código es la descrita en [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html)

### Diagrama

![](/assets/img/git/branch-hotfixes.png)

### Comandos

Creación de la rama de entrega `release-1.2`

```bash
git checkout -b release-1.2 develop
```

Una vez que se a trabajo en la nueva rama, para actualizar los cambios en la rama develop primero tenemos que regresar a la rama develop y partir de allí llevar a cabo una unión \(merge\):

```bash
./bump-version.sh 1.2
```

Unir las modificaciones hechas en la rama feature dentro de la rama develop:

```bash
git commit -a -m "Bumped version number to 1.2"
```

Cambiarnos a la rama de master:

```bash
git checkout master
```

Unir los cambios de la rama release1.2 con master:

```bash
git merge –no-ff release-1.2
```

Enviar los cambios a la rama develop

```bash
git tag –a 1.2
```

## Rama Hotfixes

### Descripción

Una vez que se ha llevado a cabo una liberación a la rama `master` y esta versión forma parte del ambiente productivo del cliente, es posible que exista el reporte de nuevos `bugs` encontrados por los usuarios finales. Para corregir estos `bugs` y desplegar una nueva versión en el ambiente productivo, es que se utilizará la rama `hotfixe`, que ayudará a corregir errores que surgan en el ambiente de producción.

### Rama de la que bifurca

`master`

### Rama con la que se une

`master`
`develop`

### Convención de nombrado

hotfix-\[modulo-version\]

Ejemplo:

* `hotfix-seguridad-v1.1.1`
* `hotfix-carrusel-v1.1.1`

### Lineamientos

1. La rama `hotfixes` sólo existe mientras se está corriguiendo errores.
2. La rama `hotfixes` existe en el repositorio remoto.
3. La rama `hotfixes` es creada y eliminada por el rol master.
4. La operación **merge** con la rama `master` y la rama`develop` sólo la pude llevar a cabo el **rol master**.

Si existe una rama release cuando ocurre un bug en producción, entonces:

1. Los **bugs** corregidos en la rama `hotfix` se deberán de unir a la rama `release` y no a `develop`; la unión con `develop` ocurre cuando la rama `release` está lista para producción. Si el trabajo en la rama `develop` requiere de manera inmediata el cambio realizado en la rama `hotfix`, entonces se puede lleva a cabo la operación **merge** dentro de la rama `develop`;

### Diagrama

![](/assets/img/git/branch-hotfixes.png)

### Comandos

### Crear una rama `hotfix`

Las ramas hotfix son creados desde la rama master. Por ejemplo, si la versión que se liberó a producción fue la `1.2.0`, y se detectan errores durante el uso del sistema y los cambios en la rama `develop` no son estables, entonces se pude crear una rama `hotfix` para atender los bugs y volver a liberar a producción.

```bash
git checkout -b hotfix-1.2.1 master
./bum-version.sh 1.2.1
git commit -a -m "Versión modificada a 1.2.1"
```

Durante este paso se deberán de corregir los `bugs` en uno o varios `commits`:

```bash
git commit -m "Resolviendo bugs de producción"
```

Finalmente, se lleva a cabo un `merge` tanto a la rama `master` como a la rama `develop`,

Operación `merge` en la rama `master`:

```bash
git checkout master
git merge --no-ff hotfix-1.2.1
```

**Nota** Se puden utilizar las opciones`-s` o `-u` para firmar nuestro tag.

Operación `merge` en la rama `develop`:

```bash
git checkout develop
git merge --no-ff hotfix-1.2.1
```

**Nota** en caso que exista una rama de `release` los cambios en la rama `hotfix` deberán de unirse también en la rama `release`, en lugar de `develop`.

Eliminación de la rama temporal:

```bash
git branch -d hotfix-1.2.1
```

## Lineamientos para mensajes de _Commits_


Todo desarrollardor de software en el CONACYT, deberá de utilizar el [Conventional Commit](https://www.conventionalcommits.org/en/v1.0.0/) cada vez que tenga que crear un _commit_, de tal manera que otros desarrolladores puedan enteder los campos que se están subiendo y sea más fácil conocer lo que se está versionando.

De manera general, el mensaje de un _commit_ deberá de tenera la siguiente estructura:

```
<type>([optional scope]): <description>

[optional body]

[optional footer(s)]
```

en dónde `<type>` puede ser alguno de los siguientes:

* `feat`:  Introduce nuevas funcionalidades en el sistema (se correlaciona con `MINOR` en el versionado semántico).
* `fix`: Corrige un bug en el código fuente (se correlaciona con `PATCH` en el versionado semántico).
* `build`: Afectan la construcción del proyecto o de dependencias externas (ejemplo de scopes: gulp, broccoli, npm)
* `ci`: Cambios en los archivos de configuración de CI (ejemplo de scopes: Travis, Circle, BrowserStack, SauceLabs)
* `docs`: Cambios en la documentación del proyecto (ejemplo de scopes: Readme)
* `perf`: Cambio en el código para mejorar el desempeño del sistema
* `refactor`: Cambio en el código que no sea para corregir un bug ni para agregar una nueva funcionalidad
* `style`: Cambios que sólo afectan el significado del código (espacios en blanco, formato, semi-colons faltantes, etc)
* `test`: Agregar pruebas o corregir las existentes

en dónde `<scope>` hace referencia a un componente, o elemento que es afectado:

## Lineamientos para versionar

La notación para **versionamiento** se ocupa en tres lugares: **(1)** Descriptor del Projecto _(ej. package.json, pom.xml)_, **(2)** Tag del commit que se está liberando _(ej. tag en commit the rama master)_, **(3)** Build del código fuente _(ej. .jar, .dll, etc)_
{: .note}

El estándar para versionamiento, está basado en [Semantic 2.0.0](https://semver.org/)


1. Un número normal de versión **DEBE** tomar la forma `X.Y.Z` donde `X`, `Y`, y `Z` son enteros no negativos. `X` es la versión **“major”**, `Y` es la versión **“minor”**, y `Z` es la versión **“patch”**. Cada elemento **DEBE** incrementarse numéricamente en incrementos de 1. Por ejemplo: `1.9.0` -> `1.10.0` -> `1.11.0`

2. Una vez que un paquete versionado ha sido liberado **(release)**, los contenidos de esa versión **NO DEBEN** ser modificadas. Cualquier modificación **DEBE** ser liberada como una nueva versión

3. La versión `major` en cero `(0.y.z)` es para desarrollo inicial. Cualquier cosa puede cambiar en cualquier momento. El API pública no debiera ser considerada estable

4. La versión `1.0.0` define el API pública. La forma en que el número de versión es incrementado después de este release depende de esta API pública y de cómo esta cambia

5. La versión `patch` `Z` `(x.y.Z | x > 0)` **DEBE** incrementarse cuando se introducen solo arreglos compatibles con la versión anterior. Un arreglo de bug se define como un cambio interno que corrige un comportamiento erróneo

6. La versión `minor` `Y` `(x.Y.z | x > 0)` **DEBE** ser incrementada si se introduce nueva funcionalidad compatible con la versión anterior. Se **DEBE** incrementar si cualquier funcionalidad de la API es marcada como deprecada. **PUEDE** ser incrementada si se agrega funcionalidad o arreglos considerables al código privado. Puede incluir cambios de nivel `patch`. La versión `patch` **DEBE** ser reseteada a 0 cuando la versión `minor` es incrementada

7. La versión `major` `X` `(X.y.z | X > 0)` **DEBE** ser incrementada si cualquier cambio no compatible con la versión anterior es introducida a la API pública. **PUEDE** incluir cambios de nivel `minor` y/o `patch`. Las versiones `patch` y `minor` **DEBEN** ser reseteadas a 0 cuando se incrementa la versión `major`

8. Una versión `pre-release` **PUEDE** ser representada por adjuntar un guión y una serie de identificadores separados por puntos inmediatamente después de la versión `patch`. Los identificadores **DEBEN** consistir solo de caracteres **ASCII** alfanuméricos y el guión `[0-9A-Za-z-]`. Las versiones `pre-release` satisfacen pero tienen una menor precedencia que la versión normal asociada.Ejemplos: `1.0.0-alpha`, `1.0.0-alpha.1`, `1.0.0-0.3.7`, `1.0.0-x.7.z.92`

9. Los `meta-datos` del `build` **PUEDE** ser representada adjuntando un signo más y una serie de identificadores separados por puntos inmediatamente después de la versión `patch` o la `pre-release`. Los identificadores **DEBEN** consistir sólo de caracteres **ASCII** alfanuméricos y el guión `[0-9A-Za-z-]`. Los `meta-datos` del `build` **DEBIERAN** ser ignorados cuando se intenta determinar precedencia de versiones. Luego, dos paquetes con la misma versión pero distinta metadata de build se consideran la misma versión. Ejemplos: `1.0.0-alpha+001`, `1.0.0+20130313144700`, `1.0.0-beta+exp.sha.5114f85`

10. La precedencia se refiere a como son comparadas dos versiones una con la otra cuando son ordeandas. La precedencia **DEBE** ser calculada separando la _versión en major_, _minor_, _patch_ e identificadores `pre-release` en ese orden (La `meta-data` del `build` no figura en la precedencia). Las versiones `major`, `minor`, y `patch` son siempre comparadas numéricamente. La precedencia de `pre-release` **DEBE** ser determinada comparando cada identificador separado por puntos de la siguiente manera: los identificadores que solo consisten de números son comparados numéricamente y los identificadores con letras o guiones son comparados de acuerdo al orden establecido por **ASCII**. Los identificadores numéricos siempre tienen una precedencia menor que los no-numéricos. Ejemplo: `1.0.0-alpha` `<` `1.0.0-alpha.1` `<` `1.0.0-beta.2` `<` `1.0.0-beta.11` `<` `1.0.0-rc.1` `<` `1.0.0`

## Ciclo de versionamiento

Los lineamientos de versionamiento, se deberán de utilizar en momentos diferentes; dependiendo del tipo de proyecto, tamaño del equipo y el plan de iteración. De manera general, se identifican dos grandes fases que gobiernan a cualquier tipo de proyecto: **fase de inicio** y **fase de desarrollo**.

### Fase de  Inicio

#### 1. inicialización

```bash
crearRama('from=empty', 'master')
```

##### individual

```bash
clonar(master)
version('0.0.1-SNAPSHOT', pom.xml )-commit-publish
```

#### 2. flujo **increment** (arquitectura):

```bash
[update-]develop-commit[-publish]
```

#### 3. flujo **release** (release-arquitectura):

##### 3.1 Inicialización

```bash
create('branch', 'release-arquitectura')
version('0.0.z-RC')-commit[-publish]
build('0.0.z-RC+dev#hash')
build('0.0.z-RC+qa#hash')
build('0.0.z-RC+prod#hash')
```

##### 3.1 SubFlujo Pruebas (release-arquitectura) :

```bash
foreach(enviroment = {'qa'})
    until enviroment is stable:
         test-report-solve-version('0.0.(z+1)-RC', pom.xml)-commit-publish]
          build('0.0.z-RC+enviroment #hash')
```

##### 3.2 SubFlujo Pruebas Finalización (release-arquitectura) :

```bash
version('0.0.z-RELEASE', pom.xml)-commit[-publish]
merge('release-arquitectura', 'master')-tag('0.0.z')
```

##### 3.3. Publicación

```bash
build('0.0.z-RELEASE+dev#hash')-publish(dev)
build('0.0.z-RELEASE+qa#hash')-publish(qa)
build('0.0.z-RELEASE+prod#hash')-publish(prod)
crearRama('from=master', 'develop')
version('0.0.z-SNAPSHOT', pom.xml)-commit[-publish]
publish('develop')
```

#### 4. Terminación

##### individual

```bash
usarRama('develop')
```

---

## Fase de Desarrollo

### 1. Inicialización

```bash
crearRama(from='develop', 'feature-[nombre]')
version('0.(y+1).0-SNAPSHOT', pom.xml )-commit-publish
```

#### individual

```bash
clonar('feature-[nombre]')
```

### 2. Flujo increment (feature-[nombre]):

```bash
<ciclo>[update-]develop-commit[-publish]
```

### 3. Flujo Release (release-[nombre]):

#### 3.1 Inicialización

```bash
merge('feature-[nombre]', 'develop')-publish
crearRama('from=develop', 'release-[nombre]')
version('0.y.0-RC')-commit[-publish]
build('0.y.0-RC+dev#hash')
build('0.y.0-RC+qa#hash')
build('0.y.0-RC+prod#hash')
```

#### 3.2 SubFlujo Pruebas (release-[nombre]) :

```bash
<ciclo> test-report-solve-version('0.y.(z+1)-RC', pom.xml)-commit-publish]
```

#### 3.3 SubFlujo Pruebas Finalización (release-[nombre]) :

```bash
version('0.y.z-RELEASE', pom.xml)-commit[-publish]
merge('release-[nombre]', 'master')-tag('0.y.z')
```

#### 3.4 Publicar

```bash
merge('release-[nombre]', 'develop')-publish
build('0.y.z-RELEASE+dev#hash')-publish(dev)
build('0.y.z-RELEASE+qa#hash')-publish(qa)
build('0.y.z-RELEASE+prod#hash')-publish(prod)
eliminarRama('release-[nombre]')
```

preparar el siguiente incremento

```bash
version('0.y.z-SNAPSHOT', pom.xml)-commit[-publish]
publish('develop')
```

### 4. Terminación

#### individual

```bash
usarRama('develop')
```

## Lineamientos generales

Los siguiente lineamientos aplican a todas la ramas:

* Tanto el nombre de los directorios, como el de los productos de trabajo que están contenidos en ellos no incluirán acentos, ni caracteres especiales, ni espacios.
* El código contenido en cualquier rama deberá ser versionado haciendo uso del juego de caracteres **UTF-8**.
* Salvo imágenes, las ramas sólo podrán contener código fuente. Ningún otro archivo de tipo binario deberá ser considerado para versionamiento en la rama de código. En caso que sea necesario subir imágenes, estas deberán de ser codificadas en **base64**.
* Efectuar el **push** sólo para las unidades funcionales completas.
* Efectuar **push** de manera frecuente. De ser posible, cada día, siempre y cuando esto no entre en conflicto con la regla anterior.
* Para **push** deberá generarse un comentario amplio y descriptivo que incluya el detalle de aquello que se está subiendo en el repositorio **Git**.
* Generar respaldos de la base de datos **Git** en una base mensual.
* No estará permitido efectuar bloqueos, a menos que esto sea justificado plenamente.

Los siguiente lineamientos deberá de ser considerados por los desarrolladores:

* Para comenzar a trabajar siempre hay que crear un branch a partir de origin develop.
* Probar el software antes de hacer un push al repositorio remoto **origin develp**.
* En caso que esté trabajando en una nueva funcionalidad y decides que no formará parte de la rama develop, entonces, para comenzar a trabajar sobre otra nueva funcionalidad siempre deberás de hacer un rebase a **develop**.
* Llevar a cabo la operación checkout a develop, para asegurarte que te encuentras trabajando con la última versión del proyecto en fase de desarrollo.
* Siempre prueba tu código una y otra vez.
* Los proyectos no deberán de ser creados por los integrantes del repositorio gitlab, únicamente el administrador será el único facultado en llevar a cabo este tipo de acciones.


## Notas importantes

Existen dos cosas que nunca se deberá de llevar a cabo en **Git**:

1. **NUNCA** forzar una operación **push**: Si te encuentras en una situación donde tus cambios no puedas ser enviados al upstream, debido a que algo está mal.

2. **NUNCA** ejecutes la operación **rebase** a una rama a la que le has aplicado la operación **push** o **pull**. Esto puede generar la duplicidad de **_commits_** a un repositorio compartido.

## Convención de Commits

### Resumen

La especificación de Commit Convencionales es una convención liviana que se aplica a los mensajes de los commits.
Esta especificación proporciona un conjunto fácil de reglas para crear un historial de commits explícito;
Esta convención se ajusta a [SemVer](http://semver.org), al describir las características, correcciones y cambios que rompen la compatibilidad en los mensajes de los commits.

El mensaje del commit debe estar estructurado de la siguiente forma:

---

```
<tipo>[ámbito opcional]: <descripción>

[cuerpo opcional]

[nota de pie opcional]
```

---

<br />
El commit contiene los siguientes elementos estructurales para comunicar la
intención al consumidor de la librería:

1. **fix:** un commit de _tipo_ `fix` corrige un error en la base del código
   (se correlaciona con [`PATCH`](http://semver.org/#summary) en el versionado
   semántico).
1. **feat:** un commit de _tipo_ `feat` introduce nuevas características en la
   base del código (se correlaciona con [`MINOR`](http://semver.org/#summary)
   en el versionado semántico).
1. **BREAKING CHANGE:** un commit que contiene el texto `BREAKING CHANGE:` al
   inicio de su cuerpo opcional o la sección de nota de pie introduce un cambio
   que rompe la compatibilidad en el uso de la API (se correlaciona con [`MAJOR`](http://semver.org/#summary)
   en el versionado semántico). Un cambio en el uso de la API puede ser parte
   de commits de _tipo_. e.g., a `fix:`, `feat:` & `chore:` todos tipos
   válidos, adicional a cualquier otro _tipo_.
1. Otros: _tipos_ de commits distintos a `fix:` y `feat:` están permitidos, por
   ejemplo [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)
   (basado en [the Angular convention](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines))
   recomienda `chore:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:` y
   otros. También recomendamos `improvement` para commits que mejorar una
   implementación actual sin añadir nuevas características ni corregir errores.
   Tenga presente que estos tipos no son impuestos por la especificación de
   commits convencionales y no tienen efecto implícito en el versionado
   semántico (a menos que incluyan el texto BREAKING CHANGE, lo cual NO es
   recomendado).
   <br />
   Se puede agregar un ámbito al _tipo_ de commit para proveer información
   contextual adicional y se escribe entre paréntesis, e.g., `feat(parser): add ability to parse arrays`.

### Ejemplos

#### Mensaje de commit con descripción y cambio que rompe la compatibilidad en el cuerpo

```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

#### Mensaje de commit sin cuerpo

```
docs: correct spelling of CHANGELOG
```

#### Mensaje de commit con ámbito

```
feat(lang): added polish language
```

#### Mensaje de commit para una corrección usando un número de problema (opcional)

```
fix: minor typos in code

see the issue for details on the typos fixed

fixes issue #12
```

#### Especificación

Las palabras “DEBE” (“MUST”), “NO DEBE” (“MUST NOT”), “REQUIERE” (“REQUIRED”),
“DEBERÁ” (“SHALL”), “NO DEBERÁ” (“SHALL NOT”), “DEBERÍA” (“SHOULD”),
“NO DEBERÍA” (“SHOULD NOT”), “RECOMIENDA” (“RECOMMENDED”), “PUEDE” (“MAY”) Y
“OPCIONAL” (“OPTIONAL”) en este documento se deben interpretar como se describe
en [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

1. Los commits DEBEN iniciarse con un tipo que consiste en un sustantivo `feat`, `fix`, etc., seguido de dos puntos y un espacio.
1. El tipo `feat` DEBE ser usado cuando un commit agrega una nueva
   característica a la aplicación o librería.
1. El tipo `fix` DEBE ser usado cuando el commit representa una corrección a un
   error en el código de la aplicación.
1. Se PUEDE añadir un ámbito opcional después del tipo. El ámbito es una frase
   que describe una sección de la base del código encerrada en paréntesis,
   e.g., `fix(parser):`
1. Una descripción DEBE ir inmediatamente después del tipo/ámbito inicial y es
   una descripción corta de los cambios realizados en el código, e.g.,
   _fix: array parsing issue when multiple spaces were contained in string._
1. Un cuerpo del commit más extenso PUEDE agregarse después de la descripción,
   dando información contextual adicional acerca de los cambios en el código.
   El cuerpo DEBE iniciar con una línea en blanco después de la descripción.
1. Una nota de pie PUEDE agregarse tras una línea en blanco después del
   cuerpo o después de la descripción en caso de que no se haya dado un cuerpo.
   La nota de pie DEBE contener referencias adicionales a los números de
   problemas registrados sobre el cambio del código (como el número de problema
   que corrige, e.g.,`Fixes #13`).
1. Los cambios que rompen la compatibilidad con la API DEBEN ser indicados al inicio de la nota de pie o el cuerpo del commit. Un cambio que rompe la compatibilidad con la API DEBE contener el texto en mayúsculas `BREAKING CHANGE`, seguido de dos puntos y espacio.
1. Una descripción se DEBE proveer después de `BREAKING CHANGE:`, describiendo
   qué ha cambiado en la API, e.g., _BREAKING CHANGE: environment variables now take precedence over config files._
1. La nota de pie DEBE contener solamente el texto `BREAKING CHANGE`, vínculos
   externos, referencias a problemas u otra metainformación.
1. Otros tipos distintos a `feat` y `fix` PUEDEN ser usados en los mensajes de
   los commits.

## ¿Por qué usar Commits Convencionales?

* Generación automática de CHANGELOGs.
* Determinación automática de los cambios de versión (basado en los tipos de
  commits).
* Comunicar la naturaleza de los cambios a los demás integrantes del equipo, el
  público o cualquier otro interesado.
* Ejecutar procesos de ejecución y publicación.
* Hacer más fácil a otras personas contribuir al proyecto, permitiendo explorar
  una historia de los commits más estructurada.

## FAQ

### ¿Cómo puedo trabajar con los mensajes de los commits en la etapa inicial de desarrollo?

Recomendamos trabajar como si ya hubiera lanzado su producto. Típicamente
_alguien_, incluso si son sus compañeros desarrolladores, están usando su
producto. Ellos querrán saber qué se ha arreglado, qué se ha dañado, etc.

### ¿Se deben escribir los tipos de los commits en mayúscula o minúscula?

Cualquiera está bien, pero es mejor ser consistente.

### ¿Qué debo hacer si un commit encaja en más de un tipo de commit?

Regrese y haga múltiples commits de ser posible. Parte de los beneficios de los
Commits Convencionales es la habilidad para hacer commits más organizados y así
mismo PRs.

### ¿No desalienta esto el desarrollo y la iteración rápida?

Desalienta moverse rápido de una forma desorganizada. Ayuda a moverse rápido a
largo plazo a través de proyectos con una gran variedad de contribuidores.

### ¿Pueden los Commits Convencionales llevar a los desarrolladores a limitar el tipo de commits que hacen ya que estarán pensando en los tipos previstos?

Los Commits Convencionales nos animan a hacer más de cierto tipo de commits como
_fixes_. Adicionalmente, la flexibilidad de los Commits Convencionales permite
a su equipo generar sus propios tipos y cambiarlos a lo largo del tiempo.

### ¿Cómo se relaciona esto con SemVer?

El tipo de commit `fix` se traduce a un cambio de versión `PATCH`. El tipo de
commit `feat` se traduce a un cambio de versión `MINOR`. Commits con el texto
`BREAKING CHANGE`, sin importar su tipo, se traducen a un cambio de versión
`MAJOR`.

### ¿Cómo puedo versionar mis extensiones a la especificación de Commits Convencionales, e.g. `@jameswomack/conventional-commit-spec`?

Recomendamos usar SemVer para liberar su propia extensión a esta especificación
(¡y lo animamos a hacer esta extensión!)

### ¿Qué debo hacer si por accidente uso un tipo de commit equivocado?

#### Cuando utiliza un tipo que es de la especificación pero no es el correcto, e.g. `fix` en lugar de `feat`

Antes de combinar o liberar el error, recomendamos usar `git rebase -i` para
editar el historial de los commits. Después de que se ha liberado, la limpieza
será distinta de acuerdo con las herramientas y procesos que usted use.

#### Cuando se usa un tipo que no está en la especificación, e.g. `feet` instead of `feat`

En el peor de los escenarios, no es el fin del mundo si aparece un commit que no
cumple con las especificaciones de los commits convencionales. Simplemente, el
commit será ignorado por las herramientas que se basen en esta especificación.

### ¿Deben todos los que contribuyen a mi proyecto usar esta especificación?

¡No! Si usa un flujo de trabajo basado en `squash` los líderes del proyecto
pueden limpiar el mensaje en el momento en que se incorpora, sin agregar cargas
adicionales a quienes contribuyen casualmente. Un flujo de trabajo común para
esto es configurar su sistema de git para que haga el `squash` de manera
automática de un pull request y presente al líder del proyecto un formulario
para que ingrese el mensaje de commit correcto al momento de hacer el merge.