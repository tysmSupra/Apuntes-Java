# Apunte Completo – Programación II (Java)
**Cátedra:** Programación II – UTN · Ciclo Lectivo 2024  
**Propósito:** Guía integral y unificada de todo el material subido (Introducción a Java, Conceptos POO, java1–7, Hilos, Colecciones/equals/hashCode, Wrappers/String, Sintaxis, E/S y Serialización).

---

## 0) Bibliografía y enlaces
- **Bibliografía general y de consulta** (Sun, Joyanes, Arnold/Gosling/Holmes, Eckel).  
- Enlaces motivacionales/industria: Devcode, Genbeta, Universia, Codesolt.  

> *Nota:* Esta guía resume el contenido provisto en las presentaciones y lo organiza para estudio.

---

## 1) ¿Qué es Java? Ecosistema y plataformas
### 1.1. Lenguaje + Plataforma
- Java es **lenguaje de programación** y **ecosistema** (JDK/JRE/JVM).
- **Compilado e interpretado**: el código fuente `.java` se compila a **bytecode** `.class` (portátil), ejecutado por la **JVM**.
- **Write Once, Run Anywhere**: el mismo bytecode corre donde exista un JRE compatible.

### 1.2. Ediciones
- **Java SE** (Standard Edition): aplicaciones de escritorio y base de librerías.  
- **Java EE/Jakarta EE** (Enterprise): aplicaciones empresariales distribuidas (servlets, JSP/JSF, EJB, JTA, etc.).  
- **Java ME** (Micro Edition): dispositivos embebidos/móviles.

### 1.3. Herramientas y flujo de trabajo
- **JDK**: incluye `javac` (compilador), `java` (intérprete/launcher), `javadoc`, `jar`.
- **IDE**: Eclipse, IntelliJ IDEA, NetBeans, BlueJ, etc.
- Flujo típico: `javac` compila → `java` ejecuta → empaquetado con `jar` si aplica.

### 1.4. Características del lenguaje
- **Orientado a Objetos**: todo hereda de `java.lang.Object`.
- **Gestión automática de memoria**: Garbage Collector (GC).
- **Seguridad**, **Robustez**, **Portabilidad** y **Multiplataforma** a través de la JVM.

---

## 2) Sintaxis esencial de Java
### 2.1. Primer programa y estructura
```java
public class Primero {
    public static void main(String[] args) {
        System.out.println("Hola mundo");
    }
}
```
- Regla: **una clase pública por archivo** y el nombre del archivo debe coincidir con el de la clase pública.
- Método `main` es el punto de entrada de aplicaciones de consola.

### 2.2. Comentarios y Javadoc
- `//` una línea, `/* ... */` múltiples, `/** ... */` documentación.
- Javadoc genera documentación HTML desde comentarios `/** ... */`.

### 2.3. Identificadores y palabras reservadas
- Sensibles a mayúsculas/minúsculas; no pueden empezar con dígitos; usar letras/`_`/`$`.
- No usar **palabras reservadas** del lenguaje.

### 2.4. Tipos, literales, valores por defecto
- **Primitivos**: `boolean, char, byte, short, int, long, float, double`.
- **Wrappers**: `Boolean, Character, Byte, Short, Integer, Long, Float, Double`.
- Literales decimales, octales (`0` prefijo), hexadecimales (`0x`/`0X`). Sufijos: `L` (long), `F` (float), `D` (double).
- Valores por defecto (en campos/atributos): numéricos `0`, boolean `false`, referencias `null`.

### 2.5. Casting (conversión de tipos)
- **Implícito** (ampliación sin pérdida): `int → long`, `float → double`.
- **Explícito** (posible pérdida): `double → (float)`, `int → (byte)`.

### 2.6. Operadores y precedencia
- Aritméticos `+ - * / %`, de asignación `= += -= *= /= %=`, incremento/decremento `++ --`.
- Relacionales `== != < <= > >=`, lógicos `&& || !` (cortocircuito) y bit a bit `& | ^`.
- Ternario `cond ? a : b`.
- Precedencia: `* /` sobre `+ -`. Paréntesis para desambiguar.

### 2.7. Control de flujo
- `if/else`, `switch` (soporta `String`, `int`, `enum`, etc.).
- Bucles: `while`, `do-while`, `for`, “for-each” (`for (Tipo x : coleccion)`).
- `break`, `continue`, `return`.

---

## 3) Programación Orientada a Objetos (POO)
### 3.1. Clases y objetos
- **Clase**: plantilla que define **estado** (atributos/variables de instancia) y **comportamiento** (métodos).
- **Objeto**: instancia de una clase.

### 3.2. Encapsulamiento
- Atributos privados + métodos **getter/setter** públicos para exponer estado controladamente.

```java
public class Persona {
    private String nombre;
    private String apellido;
    public String getNombre() { return nombre; }
    public void setNombre(String n) { this.nombre = n; }
}
```

### 3.3. Paquetes
- Organización lógica de clases bajo un **namespace**; declaración con `package` (primera línea del archivo).  
- Importación con `import paquete.*` o `import paquete.Clase`.

### 3.4. Modificadores de acceso
- **Clase**: `public` o *default* (sin palabra clave) → visible dentro del paquete.
- **Miembros**: `public`, `protected`, *default*, `private`.
  - `protected`: acceso por herencia incluso desde otros paquetes.
  - *default*: acceso solo dentro del mismo paquete.

### 3.5. Herencia y polimorfismo
- `extends` para heredar. Subclase hereda miembros `public`/`protected` (no `private`).
- **Overriding** (sobrescritura): misma firma, puede ajustar el tipo de retorno **covariante**. No puede reducir el nivel de acceso. Los métodos `static` **no se sobrescriben** (se **ocultan**–*hiding*).
- **Overloading** (sobrecarga): mismo nombre, distinta lista de parámetros; puede variar tipo de retorno y modificadores.

### 3.6. `final`, `abstract` y miembros `static`
- `final class` no admite subclases. `final` en método impide overriding. `final` en variable → constante (una sola asignación).
- `abstract class` no instanciable; puede tener métodos concretos y abstractos.
- `static`: miembros de clase (compartidos por todas las instancias); accesibles como `Clase.miembro`.

### 3.7. Constructores
- Se ejecutan al instanciar. No tienen tipo de retorno (ni `void`).
- Si se define algún constructor, **no** se genera el constructor vacío por defecto; si se necesita, declararlo explícitamente.
- Reglas con `super(...)`: la primera instrucción del constructor puede invocar al constructor de la superclase.

### 3.8. `this` y `super`
- `this` referencia a la instancia actual (desambiguación de nombres, encadenamiento de constructores).  
- `super` referencia a miembros de la superclase (incluidos constructores mediante `super(...)`).

### 3.9. JavaBeans (POJO con convención)
- Atributos privados; getters/setters públicos; **constructor vacío**; clase pública; en general serializable; boolean con prefijo `is`.

### 3.10. `instanceof` y *casting* de referencias
- `obj instanceof Tipo` devuelve `true/false`.
- *Upcasting* (subtipo → supertipo) implícito; *downcasting* explícito (verificar con `instanceof`).

### 3.11. `enum`
- Enumeraciones para valores constantes tipados. No se declaran dentro de métodos; pueden tener comportamiento adicional (campos, constructores, métodos).

---

## 4) `Object`, `toString()`, `equals()` y `hashCode()`
### 4.1. `toString()`
- Se invoca al imprimir referencias; conviene sobrescribir para devolver descripciones legibles.

### 4.2. `equals()` vs `==`
- `==` compara **referencias** (misma dirección/objeto).  
- `equals()` compara **contenido** (si se sobrescribe correctamente). Por defecto, en `Object`, es equivalente a `==`.

### 4.3. Contrato de `equals()`
- **Reflexivo**, **Simétrico**, **Transitivo**, **Consistente**, y para cualquier `x != null`, `x.equals(null)` debe ser **false**.

### 4.4. `hashCode()`
- Usado por colecciones basadas en hash. Contrato: si `a.equals(b)` entonces `a.hashCode() == b.hashCode()`.
- Estable durante la vida del objeto en colecciones (no cambiar campos que afectan el hash cuando esté como clave).

### 4.5. Sugerencias de implementación
- Usa campos **inmutables** en `equals`/`hashCode` cuando sea posible.
- Asegura consistencia entre ambos; utiliza utilidades como `Objects.equals()`/`Objects.hash()` (Java 7+).

---

## 5) Framework de Colecciones
### 5.1. Interfaces principales
- `Collection` (raíz), `List`, `Set`, `Queue`, `Deque`; `Map` (estructura clave→valor, no subinterfaz de `Collection`).

### 5.2. Implementaciones frecuentes
- **List**: `ArrayList` (acceso aleatorio rápido, inserciones/eliminaciones interiores costosas), `LinkedList` (inserciones/eliminaciones eficientes, iteración más costosa), `Vector` (sincronizado, obsoleto en diseños modernos).
- **Set**: `HashSet` (no ordenado, únicos), `LinkedHashSet` (mantiene orden de inserción), `TreeSet` (orden natural/`Comparator`, elementos comparables entre sí).
- **Map**: `HashMap` (no ordenado), `LinkedHashMap` (orden de inserción/uso), `TreeMap` (orden por clave), `Hashtable` (sincronizado, legado).
- **Queue/Deque**: `PriorityQueue` (cola con prioridad), `ArrayDeque`.

### 5.3. Genéricos y autoboxing
- Desde Java 5, colecciones **genéricas**: `List<String>`.  
- Autoboxing/unboxing: `List<Integer> xs; xs.add(42); int n = xs.get(0);`.

### 5.4. Iteración y utilidades
- `Iterator` (`hasNext()`, `next()`, `remove()`); `ListIterator` (bidireccional).  
- `Collections` utilidades: `sort`, `reverse`, `shuffle`, `binarySearch`, `unmodifiableXxx`, etc.

### 5.5. Ordenación
- **Natural**: `Comparable#compareTo` en el propio tipo.  
- **Externa**: `Comparator#compare(a, b)` (permite distintas vistas de orden sin modificar la clase).

### 5.6. Conversión Array ↔ List
- `Arrays.asList(array)` (vista respaldada por el mismo respaldo).  
- `list.toArray(new Tipo[0])` (copia tipada).

---

## 6) Hilos (Threads) y concurrencia
### 6.1. Conceptos
- **Thread** = unidad de ejecución ligera con **propia pila**.  
- En Java, un *hilo* puede representarse como **objeto** (`java.lang.Thread`) y como **flujo de ejecución**.

### 6.2. Crear hilos
- **Extender `Thread`** y sobrescribir `run()`.
- **Implementar `Runnable`** y pasar la instancia a un `Thread` (`new Thread(r).start()`). *Más flexible* (permite heredar de otra clase).

### 6.3. Inicio y nombre
- Se inicia con `start()` (no llamar `run()` directamente).  
- `Thread.currentThread().getName()` obtiene el nombre; `setName()` lo cambia.

### 6.4. Estados del ciclo de vida
- **NEW → RUNNABLE → RUNNING → WAIT/BLOCKED → DEAD** (terminado).  
- Esperas típicas: **sleep**, **espera de E/S**, **wait** por monitor.

### 6.5. Planificación (scheduler) y control
- **Prioridades** (`setPriority(1..10)` según VM), `yield()` (ceder), `join()` (esperar a que termine otro hilo), `sleep(ms)` (pausar).

### 6.6. Sincronización
- `synchronized` en **métodos** o **bloques** garantiza exclusión mutua.  
- Sincronización **estática** (en el `Class` object) para miembros `static`.
- **Comunicación entre hilos** con monitores: `wait()`, `notify()`, `notifyAll()`.

### 6.7. Buenas prácticas
- Limitar la sección crítica.  
- Evitar *deadlocks*: orden fijo para adquirir bloqueos; tiempo de espera.  
- Preferir librerías de alto nivel (java.util.concurrent) en proyectos modernos.

---

## 7) Entrada/Salida (I/O) y Serialización
### 7.1. Streams
- **Bytes**: `InputStream`/`OutputStream` y derivados (`FileInputStream`, `FileOutputStream`).  
- **Caracteres**: `Reader`/`Writer` (`FileReader`, `FileWriter`, `BufferedReader`, `BufferedWriter`).
- `File`: representación de rutas/archivos/directorios; consultas (`exists`, `canRead`, `isDirectory`, etc.), `renameTo`, etc.

### 7.2. Ejemplos típicos
- Crear archivo y escribir líneas; lectura con `BufferedReader#readLine()`; copiar archivos leyendo bytes y escribiendo a la salida.

### 7.3. Serialización de objetos
- Implementar `java.io.Serializable` en la clase.  
- Guardar con `ObjectOutputStream`; leer con `ObjectInputStream`.
- **`transient`**: excluye un campo de la serialización.
- Considerar `serialVersionUID` para compatibilidad de versión.

---

## 8) Strings y Wrappers en detalle
### 8.1. `String`
- **Inmutable**: métodos como `concat`, `replace`, `toUpperCase` retornan **nuevas** instancias.  
- Uso intensivo de concatenación → preferir `StringBuilder`/`StringBuffer`.

### 8.2. `StringBuilder` vs `StringBuffer`
- Misma API; `StringBuffer` es **sincronizado** (thread-safe), **más lento**.  
- `StringBuilder` **no sincronizado** (más rápido) para contexto monohilo.

### 8.3. Wrappers
- Constructores y factorías: `valueOf(String)`, `parseXxx(String)` (devuelve primitivo), `xxxValue()` para extraer primitivos.
- Lanzan `NumberFormatException` si el `String` no es válido.

---

## 9) Ejemplos prácticos clave
### 9.1. `equals`/`hashCode`
```java
final class Punto {
    private final int x, y;
    Punto(int x, int y) { this.x = x; this.y = y; }
    @Override public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Punto)) return false;
        Punto p = (Punto) o; return x == p.x && y == p.y;
    }
    @Override public int hashCode() {
        int r = Integer.hashCode(x);
        r = 31 * r + Integer.hashCode(y);
        return r;
    }
    @Override public String toString() { return "("+x+","+y+")"; }
}
```

### 9.2. Ordenación con `Comparable` y `Comparator`
```java
class DVDInfo implements Comparable<DVDInfo> {
    private final String title; private final String genre; private final int year;
    DVDInfo(String t, String g, int y) { title=t; genre=g; year=y; }
    public String getTitle(){return title;} public String getGenre(){return genre;}
    @Override public int compareTo(DVDInfo o){ return title.compareTo(o.title); }
}
class GenreSort implements java.util.Comparator<DVDInfo> {
    @Override public int compare(DVDInfo a, DVDInfo b){ return a.getGenre().compareTo(b.getGenre()); }
}
```

### 9.3. Hilos – `Runnable` + `sleep` + `join`
```java
class Trabajo implements Runnable {
    private final String nombre;
    Trabajo(String n){ this.nombre = n; }
    @Override public void run(){
        for(int i=1;i<=3;i++){
            System.out.println(nombre+" paso "+i);
            try { Thread.sleep(1000); } catch(InterruptedException ignored) {}
        }
    }
}
public class DemoHilos {
    public static void main(String[] args) throws InterruptedException {
        Thread a = new Thread(new Trabajo("A"));
        Thread b = new Thread(new Trabajo("B"));
        a.start(); b.start();
        a.join(); b.join();
        System.out.println("Fin");
    }
}
```

### 9.4. E/S de caracteres (lectura línea a línea)
```java
try (var in = new java.io.BufferedReader(new java.io.FileReader("in.txt"));
     var out = new java.io.BufferedWriter(new java.io.FileWriter("out.txt"))) {
    String line;
    while((line = in.readLine()) != null){
        out.write(line);
        out.newLine();
    }
}
```

### 9.5. Serialización simple
```java
class Alumno implements java.io.Serializable {
    String nombre; transient String password; // no se serializa
}
// Guardar
try (var oos = new java.io.ObjectOutputStream(new java.io.FileOutputStream("alumno.bin"))) {
    oos.writeObject(new Alumno());
}
// Leer
try (var ois = new java.io.ObjectInputStream(new java.io.FileInputStream("alumno.bin"))) {
    Alumno a = (Alumno) ois.readObject();
}
```

---

## 10) Checklist de repaso por tema
- [ ] Diferencia `==` vs `equals()` y contrato de `hashCode()`
- [ ] Interfaces de colecciones y cuándo usar cada implementación
- [ ] `Comparable` vs `Comparator`
- [ ] Ciclo de vida de un thread y métodos (`start`, `sleep`, `join`, `yield`)
- [ ] Uso correcto de `synchronized` y `wait/notify`
- [ ] Streams de **bytes** vs **caracteres** y clases clave
- [ ] Serialización (`Serializable`, `transient`)
- [ ] Strings inmutables; `StringBuilder`/`StringBuffer`
- [ ] Modificadores `public/protected/default/private`, `final`, `abstract`, `static`
- [ ] Constructores, `this` y `super`
- [ ] Reglas de sobrecarga y sobrescritura

---


