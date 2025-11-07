# Heap - Handle

### To do list:
- [X] Actualizar nota;
- [x] Sacar estudiante;
- [x] Sacar peor nota;
- [x] Meter examenes;


### Estructura del heap con un handle;
```java
var heap; // array de estudiantes
var handle; // handle[id] = indice del estudiante en el heap
var size; // cantidad de elementos
```
![alt text](image-25.png)
```java
class Estudiante{
    int id;
    int cantidadDeRespuestasCorrectas; //  necesario para resolver
    Array[int] examen;
}
```

handle -> [donde esta en el heap]

heap -> estudaintes con prioridad en peor nota

Necesito que esta estructura haga:
- Acceder al examen en O(1)
- Actualizar la nota en O(log E)
- Eliminar directamente en O(log E)

### Acceder a examen:

```java
// como el handle me proporciona la ubicación de donde se encuentra el examen en el heap, entonces puedo hacer:
proc obtenerExamen(in idEstudiante){
    var ubicacion = handle[idEstudiante]
    var examen = heap[ubicacion]
}
```
![alt text](image-26.png)


### Meter examenes 
```java
proc insertar(in estudiante:Estudiante){
    heap[size] = estudiante; // insertar el examen al final del heap;
    handle[estudiante.id] = size; // guardar donde esta el examen.
    ordenarHeap(heap);
    size++; //<- Nuevo elemento
}
```
![alt text](image-27.png)
> estamos poniendolo en el final porque en este caso se esta armando el EdR todos tienen la misma nota 0, y deempato por id.
![alt text](image-28.png)

### consultar las peores notas:
> - objetivo: Encontrar los k peores estudiantes.
> - obstaculo: necesito que sea en tiempo O(1).

depende de lo que quiera hacer.
```java
func kPeoresEstudiantes(k){
    var list : listaEnlasada<Examenes> := new listaEnlasada();
    int i = 0;
    while (i < k){
        list.agregarRapido(heap.desencolarPeorNota())
        // desencolar se encarga de actualziar el handle
    }endwhile
    if(quieroQueSemantengaElHeap){
        actual = lista.raiz;
        while(lista.haySiguiente()){
            heap.enconlar(actual.valor);
            actual = actual.siguente();
        }
        return lista;
    }else{
        return lista;
    }
}

```
Esta implementacion toma en cuenta el proceso de k parciales para la darkweb. porque puede ser que quiera los k examenes para modificarlos y despues ponerlos, ahí me sirve que el heap se vaya vaciando.
> Objetivo
![alt text](image-13.png)

> 1°
![alt text](image-14.png)

> 2°
![alt text](image-17.png)

> 3°
![alt text](image-16.png)

> 4°
![alt text](image-18.png)

> 5°
![alt text](image-19.png)

> Para sacar al segundo seguiria el mismo proceso.
### Eliminar estudiante


```java
proc eliminarEstudiante(in idEstudiante:int){// se va del aula
    var indiceDelheap = handle[idEstudiante]
    cambiarElementos(heap[indiceDelHeap], heap[size - 1]) // pongo al estudiante que quiero eliminar al final.
    
    // actualizar el handle luego del intercambio;
    actualizarHandles()
    // seria cambiar la posicion de nodo final con el que quiero eliminar.
    
    // elimino el nodo final (Porque es estudiante que quiero sacar)
    size--;
    heap.eliminarUltimoNodo(); 

    // como rompimos el invariante luego corregimos la posición.
    ordenarArbol(i);// se encarga de actualizar el handle
}
```
Dibujo:
![alt text](image-7.png)
> lo pongo al final.
![alt text](image-8.png)

> Elimino el último
![alt text](image-9.png)

> Mantengo el invariante
![alt text](image-10.png)

> Resultado
![alt text](image-11.png)

> handle - array heap
![alt text](image-12.png)



### ¿Actualizar examen? por qué no? (resolver o consultar dw)
> como tal para actulizar el heap solo necesito ver si la nota aumento o si bajo.

entonces:
```java
func actualizarHeap(inout heap; in indice:int){
    if(laNuevaNota > alPadre){
       intercambio nodos;
       actualizar el handle
    }if(laNuevaNota < alguno de sus hijos){
        lo intercambio con el menor
        actualizar el handle
    }
}
```
> Enunciado
![alt text](image-20.png)

> estudiante 3 tiene peor nota que estudiante 2
![alt text](image-21.png)

> estudainte 3 tiene peor nota que estudiante 1
![alt text](image-22.png)

> estudiante 3 es la nueva raíz 
![alt text](image-23.png)

> resultado
![alt text](image-24.png)