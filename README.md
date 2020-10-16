# Minions

![Minions cover](assets/minions.jpg)

Una importante científica local nos pide que desarrollemos un programa que modele el comportamiento habitual de sus empleados, con el fin de organizar mejor la asignación de trabajo. Estos empleados, lejos de ser trabajadores normales, son unas criaturas genéticamente diseñadas por ella para adecuarse mejor a las distintas tareas que deben realizarse en su laboratorio.

Según nos cuentan, existen dos razas de empleados: Bíclopes y Cíclopes.

**Los Bíclopes** tienen dos ojos, no tienen problemas para realizar ninguna tarea y su estamina está limitada a un máximo de 10 puntos.

**Los Cíclopes** tienen un solo ojo, lo cual hace que les cueste bastante apuntar un arma: sólo aciertan la mitad de los disparos. No tienen límite a la estamina que pueden tener.

También sabemos que, en el laboratorio, cada empleado tiene asignado un rol. Este rol se elige arbitrariamente, podría cambiar de un día para el otro y no depende de la raza del empleado (cualquier empleado podría tener cualquier rol). 

Los roles que existen son:

* **Soldado** están equipados con un arma que les facilita la defensa del laboratorio. Cada vez que un soldado usa su arma para defender un sector, gana práctica y se vuelve un poquito mejor con ella, incrementando en 2 el daño que causa. Si por algún motivo el soldado cambia de rol, toda la práctica ganada se pierde.
* **Obrero** tienen un cinturón con varias herramientas (cada uno puede tener herramientas distintas).
* **Limpiador** prefieren tener las manos limpias, así que van a negarse a defender sectores.

En cualquier momento, la científica podría ordenarle a cualquiera de sus empleados que realice una tarea en el laboratorio. Enumeramos debajo las tareas posibles.

### Arreglar una máquina 

Las máquinas tienen cierta complejidad asociada (puede ser desde un candado hasta un reactor nuclear) y cada una podría requerir distintas herramientas para arreglarla.

Para poder arreglar una máquina hay dos requerimientos:
* tener tanta estamina como complejidad tenga la máquina, 
* tener las herramientas necesarias para arreglarla (nótese que si la máquina no requiere de ninguna herramienta, cualquier empleado con estamina suficiente puede arreglarla).

Trabajar en una máquina es agotador, así que los empleados pierden tantos puntos de estamina como complejidad de la máquina al arreglarla. La dificultad para este tipo de tareas es el doble de la complejidad de la máquina.

### Defender un sector

El laboratorio está dividido en sectores, los cuales ocasionalmente pueden estar a la merced de alguna amenaza. Cuando eso ocurre, se indica cuál es el grado de amenaza que está sufriendo (un número entero).

Defender un sector requiere que el empleado pueda aplicar una fuerza igual o mayor al grado de amenaza, excepto para los limpiadores, que _nunca_ pueden defender un sector. La fuerza de un empleado es `la mitad de su estamina + 2`, salvo para los Soldados, que suman a eso el daño extra por práctica.

Los Bíclopes pueden aplicar toda su fuerza, mientras que los Ciclopes, por eso de que sólo impactan la mitad de los ataques, pueden aplicar solamente la mitad de su fuerza para defender un sector.

Algunos ejemplos:
* un Bíclope Soldado con 20 de estamina y 4 de daño extra tendrá una fuerza de 16 (`20 / 2 + 2 + 4`);
* un Cíclope Soldado con los mismos valores tendrá una fuerza de 8;
* un Cíclope Obrero con 20 de estamina tendrá una fuerza de 12 (`20 / 2 + 2`).

Al defender un sector, los obreros pierden la mitad de su estamina y los soldados incrementan su daño extra en 2.

La dificultad de esta tarea es el grado de amenaza para los Bíclopes y el doble para los Cíclopes.

### Limpiar un sector

Ocasionalmente el laboratorio se ensucia y depende de los empleados mantenerlo en orden. La dificultad de este tipo de tareas es 10, pero el sistema tiene que contemplar la posibilidad de cambiar este valor para _todas_ las tareas a la vez.

Para cada sector se indica si es grande o no. Para limpiarlo se requiere tener al menos 4 puntos de estamina si el sector es grande y 1 si no lo es. Al limpiar se pierde la estamina requerida para limpiar el sector, a menos que el empleado tenga rol de limpiador. Los limpiadores siempre pueden limpiar (se saltean el chequeo de los puntos de estamina) y no pierden estamina al hacerlo.

A cualquier empleado puede ordenársele que realice **cualquier** tarea, independientemente de su raza o rol. En caso de cumplir con los requerimientos el empleado la realiza en el momento; de lo contrario debe lanzar un error ya que no puede hacer lo pedido.

Finalmente, para recuperar la estamina perdida, los empleados pueden comer una fruta. Las bananas recuperan 10 puntos, las manzanas 5 y las uvas 1.

## Requerimientos

Se pide implementar un programa en Kotlin, junto con tests donde se muestre el punto de entrada de cada requerimiento, que refleje el modelo descrito y permita:

1. Que un empleado pueda comer una fruta para recuperar estamina.
2. Conocer la experiencia de un empleado, que se obtiene a partir de la cantidad de tareas realizadas multiplicada por la sumatoria de sus dificultades.
3. Hacer que un empleado realice una tarea (que arregle una máquina, defienda o limpie un sector del laboratorio), teniendo en cuenta las restricciones descritas anteriormente. Si no puede hacerla, debe lanzarse un error.
4. Agregar un nuevo rol: el Capataz. Los capataces tienen a cargo a otros empleados. Cuando se le pide a un capataz que haga algo, él se lo delega a su subordinado más experimentado de los que puedan realizar la tarea. Si no hay ninguno que pueda hacerla, debe hacerla él. Si él tampoco puede hacer la tarea por sí mismo, se arroja el error correspondiente.

## Créditos

Enunciado original creado por Mariana Matos y Nicolás Scarcella para UTN - FRBA. Modificado por Carlos Lombardi para UNQ - locación General Belgrano y transformado a Markdown por Federico Aloi para UNaHur.
