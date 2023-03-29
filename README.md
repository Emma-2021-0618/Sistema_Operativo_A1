# UCATECI
- Sistemas operativo 2
- Lizandro jose Ramirez
- Encuentro 7 Teoria

# Tema
- Semáforo y Sincronizacion

# Autores
- Enmanuel Sanchez Rodriguez 2021-0618
- Albert Francisco Hernandez Sanchez 2019-0126

# Problemas de concurrencia

Procesamiento concurrente: base de los sistemas
operativos modernos (multiprogramados):
- Un conjunto de procesos que potencialmente pueden ejecutarse
concurrentemente (a la vez).
### Problemática:
– Podemos querer que dos o más procesos cooperen.
– Que accedan a datos comunes.
### Se necesita:
– Mecanismos de sincronización y comunicación entre procesos.
– Ejecución ordenada

### Problema básico:
- Dos o más procesos quieren llevar a cabo una determinada
tarea concurrentemente.
- Pueden llegar a resultados incorrectos.
  1. Debido a que no sabemos el orden de ejecución.
  2. No sabemos cuando serán interrumpidos y su alternancia
en la CPU.


# Concepto básico de semáforo en los sistemas operativos 

Los semáforos son una herramienta de sincronización que ofrece una solución al problema de la sección crítica (porción de código de un programa de computador en la cual se accede a un recurso compartido que no debe ser accedido por mas de un proceso o hilo en ejecución). Un semáforo provee una simple pero útil abstracción para controlar el acceso de múltiples procesos a un recurso común en programación paralela, o entornos multiusuarios.

Los semáforos sólo pueden ser manipulados usando las siguientes operaciones (éste es el código con espera activa):

~~~
Inicia(Semáforo s, Entero v)
{
  s = v;
}
~~~
En el que se iniciará la variable semáforo s a un valor entero v.


~~~
P(Semáforo s)
{
  if(s>0)  
      s = s-1;  
  else
      wait();
}
~~~
La cual mantendrá en espera activa al regido por el semáforo si éste tiene un valor inferior o igual al nulo.
~~~
V(Semáforo s)
{
   if(!procesos_bloqueados)
        s = s+1;  
   else
        signal(); 
}
~~~

### Problemas/Contratiempos
- **DeadLock**: Dos o más procesos están esperando por una condición que solo puede ser causada por un proceso que también esta esperando.
- **Starvation o Espera Indefinida**: Un proceso en la lista de espera de un semáforo de la cual están entrando y saliendo continuamente procesos y listas de espera de semáforo.

# Explicacion

## Existen 2 tipos de semaforos los cuales son:

## Semaforo Binario

Un tipo simple de semáforo es el binario, que puede tomar solamente los valores 0 y 1. Se inicializan en 1 y son usados cuando sólo un proceso puede acceder a un recurso a la vez. Cuando el recurso está disponible, un proceso accede y decrementa el valor del semáforo con la operación P. El valor queda entonces en 0, lo que hace que si otro proceso intenta decrementarlo tenga que esperar. Cuando el proceso que decremento el semáforo realiza una operación V, algún proceso que estaba esperando comienza a utilizar el recurso.

Para hacer que dos procesos se ejecuten en una secuencia predeterminada puede usarse un semáforo inicializado en 0. El proceso que debe ejecutar primero en la secuencia realiza la operación V sobre el semáforo antes del código que debe ser ejecutado después del otro proceso. Éste ejecuta la operación P. Si el segundo proceso en la secuencia es programado para ejecutar antes que el otro, al hacer P dormirá hasta que el primer proceso de la secuencia pase por su operación V. Este modo de uso se denomina señalación (signaling), y se usa para que un proceso o hilo de ejecución le haga saber a otro que algo ha sucedido.

~~~
P(Semaforo s)
{
    if(s>0)
        s -= 1
    else
        wait();
}
~~~
La cual mantendra en espera activa al regido por el semaforo si este tiene un valor inferior o igual a nulo.

~~~
P(Semaforo s)
{
    if(!procesos_bloqueados)
        s += 1
    else
        signal();
}
~~~

## Semaforo Entero
Son semáforos generales a lo contrario del semáforo binario este tipo de semáforo puede tomar cualquier valor  no negativo para poder hacer su proceso de sincronisacion siendo cero la condición de ejecución de un proceso y la espera de otro. En conclusión este tipo de semáforo puede  tomar distintos valores tal ves con la finalidad de realizar conteos.

En este caso el semáforo se inicializa con el número total de recursos disponibles (n) y las operaciones de WAIT y SIGNAL se diseñan de modo que se impida el acceso al recurso protegido por el semáforo cuando el valor de éste es menor o igual que cero.

Cada vez que se solicita y obtiene un recurso, el semáforo se decrementa y se incrementa cuando se libera uno de ellos. Si la operación de espera se ejecuta cuando el semáforo tiene un valor menor que uno, el proceso debe quedar en espera de que la ejecución de una operación señal libere alguno de los recursos.

Al igual que en los semáforos binarios, la ejecución de las operaciones son indivisibles, esto es, una vez que se ha empezado la ejecución de uno de estos procedimientos se continuará hasta que la operación se haya completado.

## Diferencia

- La variable de un semáforo binario solo tiene permitido tomar los valores 0 (ocupado) y 1 (libre) en cambio un semáforo con múltiples variables puede tomar cualquier valor entero, puede variar en un dominio no restringido.
- Semáforos binarios son más fáciles de poner en práctica en comparación con el semáforo con múltiples variables.
- Semáforo binario permite sólo un hilo para acceder al recurso a la vez, pero un semáforo con múltiples variables permite n hilos que acceden a la vez.
- Las 2 operaciones que se definen para los semáforos binarios son TAKE y RELEASE y las 2 operaciones que se definen para los semáforos con múltiples variables son WAIT y SIGNAL.
- El semáforo binario resulta adecuado cuando hay que proteger un recurso que pueden compartir varios procesos, pero cuando lo que hay que proteger es un conjunto de recursos similares, se puede usar un semáforo con múltiples variables para que lleve la cuenta del número de recursos disponibles.
- En los semáforos binarios muchos procesos pueden estar en suspensión en la lista, mientras que en los semáforos con múltiples variables los procesos avanzan sin demora.

# Relacion entre los semáforos y la sincronización 

Los semáforos son una solución, del tipo soporte al sistema operativo para garantizar la exclusión mutua
Un semáforo es una estructura diseñada para sincronizar dos o más threads o procesos, de modo que su ejecución se realice de forma ordenada y sin conflictos entre ellos.

Un semáforo nos sirve para poder permitir o restringir a los procesos o hilos el acceso a algún recurso compartido,Un semáforo básico es una estructura formada por una posición de memoria y dos instrucciones, una para reservarlo y otra para liberarlo. A esto se le puede añadir una cola de threads para recordar el orden en que se hicieron las peticiones. 

Así mismo pasa con la sincronizacion de varios procesos pasando a la misma vez mientra se ejecutan en ambitos diferentes compartiendo lo mismo recursos con relgas que limita el uso de los mismo pero que traer un mayor control de los mismo a la vez un mejor manejo y velocidad del tiempo entre ejecuciones.
