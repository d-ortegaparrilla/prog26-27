# Arrays de caràcters en Java

Un **array de caràcters** és una estructura unidimensional els elements de la qual són de tipus primitiu `char`. Aquest tipus d'array té una relació històrica i conceptual molt estreta amb les cadenes de text (`String`), i compta amb particularitats exclusives en el llenguatge Java.

---

## 1. Concepte i declaració

La declaració i instanciació d'un array de caràcters segueix la mateixa sintaxi que qualsevol altre vector unidimensional:

```java
char[] cadena = new char[8];
```

Quan es crea amb `new`, tots els elements s'inicialitzen per defecte amb el **caràcter nul**, representat com **`'\0'`** (o en codificació Unicode com `'\u0000'`).

També és possible inicialitzar-lo directament amb un conjunt de caràcters literals entre claus:

```java
char[] vocals = {'a', 'e', 'i', 'o', 'u'};
```

---

## 2. Particularitats dels arrays de caràcters

A diferència dels arrays d'altres tipus (com `int[]` o `double[]`), els arrays de tipus `char` presenten comportaments únics:

### 2.1 Impressió directa del contingut

Quan passem un array numèric a `IO.println()` o `System.out.println()`, Java imprimeix la representació de la seua referència en memòria (per exemple, `[I@5f184fc6`). En canvi, amb els arrays de caràcters, els mètodes d'impressió estan sobrecarregats per a mostrar directament la **seqüència de caràcters** com si fóra un text continu:

```java
char[] vocals = {'a', 'e', 'i', 'o', 'u'};
IO.println(vocals); // Mostra per pantalla: aeiou
```

Si l'array conté caràcters nuls inicials o finals, aquests s'imprimeixen com a espais invisibles:

```java
char[] buffer = new char[6];
buffer[0] = 'm';
buffer[1] = 'n';

IO.print(buffer);
IO.println("."); // Mostra: mn    . (les 4 posicions nuls resten en blanc)
```

### 2.2 L'atribut `.length`

L'atribut `.length` d'un array de caràcters retorna sempre la **capacitat total física** de l'array reservada en memòria, independentment de si les posicions estan ocupades per caràcters nuls `'\0'` o per caràcters visibles:

```java
char[] text = new char[10];
text[0] = 'H';
text[1] = 'i';

IO.println(text.length); // Retorna sempre 10
```

---

## 3. Conversió entre `String` i `char[]`

A causa de la semblança entre una cadena de caràcters i un vector de tipus `char`, Java proporciona mecanismes directes i molt eficients per a convertir entre ambdues representacions.

### 3.1 De `String` a `char[]`: `toCharArray()`

El mètode **`toCharArray()`** de la classe `String` descompon una cadena i retorna un nou array de caràcters independent amb tots els caràcters del text:

```java
String salutacio = "Programació";
char[] lletres = salutacio.toCharArray();

IO.println("Primer caràcter: " + lletres[0]); // 'P'
IO.println("Total lletres: " + lletres.length); // 11
```

### 3.2 De `char[]` a `String`: Constructors de `String`

Podem construir un nou objecte `String` a partir d'un array de caràcters emprant els constructors sobrecarregats de la classe `String`:

=== "Conversió de l'array complet"
    ```java
    char[] vocals = {'a', 'e', 'i', 'o', 'u'};
    String s = new String(vocals); // Crea la cadena "aeiou"
    ```

=== "Conversió d'un subconjunt d'elements"
    ```java
    char[] lletres = {'P', 'R', 'O', 'G', 'R', 'A', 'M'};
    // Paràmetres: (array, posició_inici, quantitat_elements)
    String subtext = new String(lletres, 0, 4); // Crea la cadena "PROG"
    ```

---

## 4. Recorregut d'un array de caràcters

Podem recórrer un vector de caràcters de dues maneres segons si treballem amb tota la grandària o amb contingut parcial acabat en caràcter nul:

### 4.1 Recorregut complet amb bucle `for`

Quan l'array està ple o coneixem la quantitat d'elements útils:

```java
char[] s = {'A', 'l', 'c', 'o', 'i'};

for (int i = 0; i < s.length; i++) {
    IO.print(s[i] + " ");
}
// Eixida: A l c o i
```

### 4.2 Recorregut amb sentinella nul `'\0'`

Si l'array té una capacitat sobredimensionada i el text útil acaba en el primer caràcter nul `'\0'` (com es feia tradicionalment en el llenguatge C), podem iterar mitjançant un bucle `while`:

```java
char[] buffer = new char[10];
buffer[0] = 'H';
buffer[1] = 'o';
buffer[2] = 'l';
buffer[3] = 'a';
// buffer[4] .. buffer[9] contenen '\0'

int i = 0;
while (buffer[i] != '\0') {
    IO.print(buffer[i]);
    i++;
}
IO.println(); // Mostra: Hola
```

---

## 5. Exemples pràctics resolts

### Exemple 1: Eliminació d'un caràcter amb desplaçament a l'esquerra

Donat un array de caràcters que conté el text `"Hola"`, volem eliminar totes les aparicions de la lletra `'l'` sense deixar buits ni forats buits entre lletres (desplaçant els caràcters posteriors a l'esquerra) i marcant el final amb el caràcter nul `'\0'`.

??? example "Solució en Java"
    ```java
    /*
     * Programa que elimina un caràcter seleccionat d'un array de caràcters
     * reorganitzant els elements contigus i afegint el caràcter nul al final.
     */
    void main() {
        char[] s = new char[10];
        s[0] = 'H';
        s[1] = 'o';
        s[2] = 'l';
        s[3] = 'a';
        // Estat inicial: ['H', 'o', 'l', 'a', '\0', '\0', '\0', '\0', '\0', '\0']

        char aEliminar = 'l';
        int j = 0; // Índex on s'aniran copiant els caràcters vàlids

        for (int i = 0; s[i] != '\0'; i++) {
            if (s[i] != aEliminar) {
                s[j] = s[i];
                j++;
            }
        }

        // Establim el caràcter nul al final de la nova seqüència compactada
        s[j] = '\0';

        // Mostrem el resultat caràcter a caràcter
        IO.print("Array resultant: ");
        for (int i = 0; s[i] != '\0'; i++) {
            IO.print(s[i]);
        }
        IO.println(); // Eixida: Hoa
    }
    ```

---

### Exemple 2: Càlcul de la lletra del DNI

A l'Estat espanyol cada ciutadà té un document nacional d'identitat (DNI) format per un número de 8 xifres i una lletra de control. L'algorisme oficial calcula el residu de dividir el número entre 23 (operació mòdul `% 23`), obtenint un valor entre 0 i 22 que es correspon amb una lletra d'una taula predefinida.

??? example "Solució en Java"
    ```java
    /*
     * Programa que calcula la lletra de control d'un DNI a partir
     * del número de 8 xifres emprant un vector de caràcters.
     */
    void main() {
        // Taula oficial de correspondències de lletres del DNI (ordre mòdul 23)
        char[] lletresDni = {
            'T', 'R', 'W', 'A', 'G', 'M', 'Y', 'F', 'P', 'D', 'X',
            'B', 'N', 'J', 'Z', 'S', 'Q', 'V', 'H', 'L', 'C', 'K', 'E'
        };

        String entrada;
        do {
            IO.print("Introdueix el número de DNI (8 dígits): ");
            entrada = IO.readln().trim();
        } while (entrada.length() != 8);

        int numero = Integer.parseInt(entrada);
        int modul = numero % 23;
        char lletraAssignada = lletresDni[modul];

        IO.println("El DNI complet és: " + numero + "-" + lletraAssignada);
    }
    ```
