# Operacions amb vectors: La classe `Arrays`

En la secció anterior hem aprés a gestionar vectors de forma manual mitjançant bucles `for` i `for-each`. No obstant això, tasques com ordenar un vector, cercar un element, copiar dades o mostrar el contingut per pantalla són necessitats tan habituals que la plataforma Java incorpora una eina estàndard específica: la classe **`java.util.Arrays`**.

Aquesta classe conté una col·lecció de **mètodes estàtics** altament optimitzats per a treballar amb arrays de qualsevol tipus primitiu (`int`, `double`, `boolean`, `char`, etc.) i d'objectes. Per a utilitzar-la, cal incloure la sentència d'importació a l'inici del programa:

```java
import java.util.Arrays;
```

!!! tip "Per què utilitzar `java.util.Arrays`?"
    Encara que podem programar els nostres propis algorismes de cerca o d'ordenació, els mètodes de la classe `Arrays` ofereixen un **codi eficient, provat i lliure d'errors**, reduint dràsticament el temps de desenvolupament. Sempre que siga possible, aprofitarem les funcionalitats que ofereix aquesta classe.

---

## 1. Mostrar el contingut d'un array: `Arrays.toString()`

Quan intentem imprimir directament un array mitjançant `IO.println(t)` o `System.out.println(t)`, Java no mostra els elements, sinó la seua referència interna en memòria (per exemple, `[I@5f184fc6`).

El mètode **`Arrays.toString()`** converteix qualsevol vector en una cadena de text formatada, amb els elements continguts entre corxets i separats per comes:

```java
int[] valors = {8, 41, 37, 22, 19};

// Impressió directa clàssica (incorrecta per a veure els elements)
IO.println(valors); // Mostra una referència: [I@...

// Impressió correcta i neta amb Arrays.toString()
IO.println(Arrays.toString(valors)); 
// Eixida: [8, 41, 37, 22, 19]
```

---

## 2. Inicialització i emplenat: `Arrays.fill()`

Permet assignar de manera directa un mateix valor a totes les posicions d'un array o a un subconjunt determinat d'elles:

### 2.1 Emplenar tot l'array

```java
double[] sous = new double[5];
Arrays.fill(sous, 1234.56);

IO.println(Arrays.toString(sous));
// Eixida: [1234.56, 1234.56, 1234.56, 1234.56, 1234.56]
```

### 2.2 Emplenar un subrang: `[desDe, finsA)`

Podem indicar els límits del rang que volem modificar:

```java
Arrays.fill(sous, 1, 4, 999.0);
```

!!! important "Rang obert a la dreta: `[desDe, finsA)`"
    En tots els mètodes de l'API de Java que accepten un rang amb dos índexs (`desDe`, `finsA`), **l'índex final mai s'inclou**.  
    En l'exemple anterior, el rang `(1, 4)` modifica exclusivament les posicions **1, 2 i 3** (l'anterior a la 4).

---

## 3. Ordenació d'elements: `Arrays.sort()`

Ordenar un vector consisteix a reorganitzar les seues dades perquè queden en ordre ascendent (de menor a major):

```java
int[] edats = {85, 19, 3, 23, 7};

Arrays.sort(edats); // Ordena el vector in-place (modifica l'original)

IO.println(Arrays.toString(edats));
// Eixida: [3, 7, 19, 23, 85]
```

També admet ordenar únicament un subrang amb `Arrays.sort(vector, desDe, finsA)`.

---

## 4. Cerca en arrays: `Arrays.binarySearch()`

Localitzar si un determinat valor (anomenat **clau de cerca**) existeix dins d'un array i quina posició ocupa depén fonamentalment de si el vector està ordenat o no.

### 4.1 Cerca en taules no ordenades (Cerca seqüencial)

Quan les dades estan desordenades, no tenim més remei que recórrer el vector element a element des del principi fins al final o fins a trobar la clau:

```java
int clau = 22;
int[] dades = {8, 41, 37, 22, 19};
int pos = -1;

for (int i = 0; i < dades.length; i++) {
    if (dades[i] == clau) {
        pos = i;
        break; // Trobat, interrompem el bucle
    }
}
```

### 4.2 Cerca en taules ordenades: Cerca dicotòmica / binària

Si el vector està ordenat, podem emprar l'algorisme de **cerca dicotòmica** (*binary search*), el qual divideix la taula en dues meitats successives descartant la meitat on és impossible que estiga el valor.

Java implementa aquest algorisme en el mètode **`Arrays.binarySearch(t, clau)`**:

!!! danger "Requisit fonamental per a `Arrays.binarySearch`"
    **L'array ha d'estar obligatòriament ordenat en ordre creixent abans de cridar a `binarySearch`** (per exemple, havent executat prèviament `Arrays.sort(t)`). Si l'array no està ordenat, el resultat que retorna el mètode és indefinit i completament impredictible.

#### Interpretació del resultat retornat:

* **Si l'element existeix:** Retorna el seu índex numèric ($\ge 0$).
* **Si l'element NO existeix:** Retorna un **nombre negatiu**. Aquest valor conté informació molt valuosa: indica la posició on hauria d'haver estat inserit l'element per tal que el vector continuara ordenat:

$$\text{índexInserció} = -\text{posicióRetornada} - 1$$

```java
int[] nums = {2, 4, 5, 6, 9}; // Taula ordenada prèviament

// 1. Cerquem el número 5 (que SÍ existeix a la posició 2)
int pos1 = Arrays.binarySearch(nums, 5);
IO.println("Posició del 5: " + pos1); // Retorna 2

// 2. Cerquem el número 3 (que NO existeix)
int pos2 = Arrays.binarySearch(nums, 3);
IO.println("Posició retornada per al 3: " + pos2); // Retorna -2

// Calculem on hauria d'haver anat el 3:
int indexInsercio = -pos2 - 1; // -(-2) - 1 = 1
IO.println("El número 3 hauria d'anar a l'índex: " + indexInsercio); // Índex 1 (entre el 2 i el 4)
```

---

## 5. Còpia d'arrays: `Arrays.copyOf()` i `System.arraycopy()`

Recordem que l'operador d'assignació `=` només copia la referència en memòria, no els elements. Per a duplicar vertaderament un array disposem de diverses alternatives:

### 5.1 `Arrays.copyOf()`

Construeix i retorna un **nou array** independent amb la longitud especificada:

```java
int[] original = {1, 2, 6, 23};

// Còpia exacta de la mateixa mida
int[] copia = Arrays.copyOf(original, original.length);

// Còpia reduïda (trunca els elements sobrants)
int[] reduida = Arrays.copyOf(original, 2); // [1, 2]

// Còpia ampliada (els nous buits s'inicialitzen amb el valor per defecte, 0)
int[] ampliada = Arrays.copyOf(original, 7); // [1, 2, 6, 23, 0, 0, 0]
```

### 5.2 `Arrays.copyOfRange()`

Genera una còpia d'un subrang de posicions delimitat per $[desDe, finsA)$:

```java
int[] t = {7, 5, 3, 1, 0, -2};
int[] sub = Arrays.copyOfRange(t, 1, 4); // Copia els índexs 1, 2 i 3
IO.println(Arrays.toString(sub)); // [5, 3, 1]
```

### 5.3 `System.arraycopy()`

Mentre que `Arrays.copyOf()` crea una taula nova, el mètode natiu de baix nivell **`System.arraycopy()`** copia elements entre dues taules que **ja han sigut creades prèviament**:

```java
System.arraycopy(origen, posOrigen, destí, posDestí, quantitatElements);
```

```java
int[] font = {10, 20, 30, 40, 50};
int[] desti = new int[5];

// Copiem 3 elements des de la posició 1 de 'font' a la posició 2 de 'desti'
System.arraycopy(font, 1, desti, 2, 3);

IO.println(Arrays.toString(desti)); // [0, 0, 20, 30, 40]
```

---

## 6. Algorismes avançats amb la classe `Arrays`

La combinació de `Arrays.copyOf()`, `Arrays.binarySearch()` i `System.arraycopy()` permet implementar amb facilitat operacions complexes de manipulació dinàmica sobre vectors estàtics.

### 6.1 Inserció d'un nou element en un vector no ordenat

Consisteix a incrementar la grandària del vector en 1 posició i situar el nou element a l'últim lloc:

| Fase | `[0]` | `[1]` | `[2]` | `[3]` | `[4]` *(nou)* |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **1. Vector original `t`** | `3` | `13` | `26` | `6` | — |
| **2. Còpia ampliada (`Arrays.copyOf`)** | `3` | `13` | `26` | `6` | `0` *(per defecte)* |
| **3. Assignació del nou valor** | `3` | `13` | `26` | `6` | **`12`** |

```java
int[] t = {3, 13, 26, 6};
int nou = 12;

// Redimensionem creant una nova instància amb una posició addicional
t = Arrays.copyOf(t, t.length + 1);

// Guardem el nou element en l'última posició disponible
t[t.length - 1] = nou;

IO.println(Arrays.toString(t)); // [3, 13, 26, 6, 12]
```

---

### 6.2 Inserció ordenada (Mantenint l'ordre)

Si tenim un array ja ordenat i volem inserir un valor de manera que la taula **continue ordenada**:

1. Calculem la posició on ha d'anar amb `Arrays.binarySearch()`.
2. Creem una nova taula amb longitud `t.length + 1`.
3. Copiem els elements previs al punt d'inserció.
4. Inserim el nou valor en la posició d'inserció.
5. Copiem els elements posteriors desplaçats una posició a la dreta amb `System.arraycopy()`.

```java
/*
 * Inserció d'un element en un vector mantenint l'ordre.
 */
int[] t = {1, 2, 3, 4, 6, 7, 8};
int nou = 5;

// 1. Busquem la posició adequada
int pos = Arrays.binarySearch(t, nou);
int indexInsercio = (pos >= 0) ? pos : -pos - 1;

// 2. Creem la nova taula ampliada
int[] copia = new int[t.length + 1];

// 3. Copiem la part anterior al buit
System.arraycopy(t, 0, copia, 0, indexInsercio);

// 4. Inserim el nou valor
copia[indexInsercio] = nou;

// 5. Copiem la part posterior desplaçada un lloc a la dreta
System.arraycopy(t, indexInsercio, copia, indexInsercio + 1, t.length - indexInsercio);

// 6. Actualitzem la referència
t = copia;

IO.println(Arrays.toString(t)); 
// Eixida: [1, 2, 3, 4, 5, 6, 7, 8]
```

---

### 6.3 Eliminació d'un element

En voler esborrar un element, la longitud física del vector haurà de decréixer en 1 unitat:

=== "En taules desordenades (Tècnica ràpida)"
    Si l'ordre no importa, substituïm l'element que volem esborrar pel **darrer element** del vector i retallem la grandària:
    ```java
    int[] t = {30, 46, 40, 36, 96, 63};
    int indexBorrat = 1; // Volem eliminar t[1] (el 46)

    // Movem l'últim element al buit de l'esborrat
    t[indexBorrat] = t[t.length - 1];

    // Reduïm la grandària de la taula
    t = Arrays.copyOf(t, t.length - 1);

    IO.println(Arrays.toString(t)); 
    // Eixida: [30, 63, 40, 36, 96]
    ```

=== "En taules ordenades (Amb compactació)"
    Si la taula està ordenada, cal mantenir la correlació desplaçant a l'esquerra tots els elements posteriors:
    ```java
    int[] t = {12, 27, 33, 38, 72, 92};
    int aBorrar = 33;

    int indexBorrat = Arrays.binarySearch(t, aBorrar);

    if (indexBorrat >= 0) {
        // Desplacem cap a l'esquerra els elements posteriors
        System.arraycopy(t, indexBorrat + 1, t, indexBorrat, t.length - indexBorrat - 1);

        // Retallem l'última posició residual
        t = Arrays.copyOf(t, t.length - 1);

        IO.println(Arrays.toString(t)); 
        // Eixida: [12, 27, 38, 72, 92]
    }
    ```

---

## 7. Comparació d'arrays: `Arrays.equals()`

Igual que ocorre amb els objectes `String`, **l'operador `==` mai s'ha d'utilitzar per a comparar arrays**, ja que avalua si dues referències apunten a la mateixa zona de memòria física:

```java
int[] t1 = {7, 9, 20};
int[] t2 = {7, 9, 20};

IO.println(t1 == t2); // Mostra FALSE! (són dos blocs de memòria diferents)
```

Per a comprovar si dos vectors contenen exactament els mateixos valors i en el mateix ordre, disposem del mètode **`Arrays.equals()`**:

```java
boolean sonIguals = Arrays.equals(t1, t2);
IO.println(sonIguals); // Mostra TRUE!
```


