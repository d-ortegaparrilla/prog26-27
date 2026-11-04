# La classe String

En Java, el tractament de text es realitza principalment a través de la classe **`java.lang.String`**. A diferència d'altres llenguatges on les cadenes són simples vectors de caràcters acabats en nul, en Java un `String` és un **objecte d'una classe de ple dret** que encapsula una seqüència de caràcters i proporciona un ampli ventall de mètodes per a operar sobre ella.

Tots els literals escrits entre cometes dobles (per exemple, `"Hola Món"`) són instàncies automàtiques de la classe `String`.

---

## 1. Immutabilitat dels objectes `String`

Una característica fonamental i distintiva dels objectes `String` en Java és que són **immutables**:

!!! important "Concepte d'immutabilitat"
    Una vegada que un objecte `String` ha sigut creat a la memòria Heap, **el seu contingut intern mai no es pot modificar**. Qualsevol mètode o operació que aparentment modifique una cadena (com `toUpperCase()`, `replace()` o la concatenació amb `+`) el que fa en realitat és **crear i retornar un objecte `String` completament nou** amb les modificacions, deixant la cadena original intacta.

Observem el següent exemple:

```java
String salutacio = "bon dia";
salutacio = salutacio.toUpperCase();
```

1. Inicialment es crea a l'Heap l'objecte amb el text `"bon dia"` i la variable `salutacio` l'apunta.
2. En cridar a `toUpperCase()`, Java crea un **segon objecte** independent amb el text `"BON DIA"`.
3. L'operador d'assignació `=` fa que la referència `salutacio` passe a apuntar al nou objecte.
4. L'objecte inicial `"bon dia"` queda orfe en memòria i serà eliminat automàticament pel **Recol·lector de Fem** (*Garbage Collector*).

```mermaid
graph LR
    subgraph Memòria Stack
        S["salutacio (Referència)"]
    end
    subgraph Memòria Heap
        O1["Objecte 1: 'bon dia' (Orfe -> Garbage Collector)"]
        O2["Objecte 2: 'BON DIA'"]
    end
    S -.->|Abans| O1
    S ===>|Després d'assignar| O2
```

---

## 2. Creació d'objectes `String`

Podem crear cadenes mitjançant diferents formes:

### 2.1 Literals entre cometes dobles

És la forma directa i recomanada. Java utilitza una zona especial de memòria anomenada **String Constant Pool** per a optimitzar l'ús de la memòria:

```java
String s1 = "Petrer";
String s2 = "Petrer"; // Reutilitza la mateixa instància de memòria del Pool
```

### 2.2 Operador de concatenació `+`

Permet unir dues o més cadenes, o combinar cadenes amb qualsevol altre tipus de dada (`int`, `double`, `boolean`):

```java
String nom = "Laura";
int edat = 22;
String presentacio = "Hola, em dic " + nom + " i tinc " + edat + " anys.";
```

### 2.3 Constructors de la classe `String`

La classe `String` compta amb múltiples constructors per a inicialitzar cadenes a partir d'altres fonts de dades:

| Constructor | Descripció | Exemple |
| :--- | :--- | :--- |
| `String()` | Crea una cadena buida equivalent a `""`. | `String s = new String();` |
| `String(String original)` | Crea un nou objecte duplicant el contingut de la cadena indicada. | `String s = new String("hola");` |
| `String(char[] array)` | Crea un `String` a partir d'un array complet de caràcters. | `char[] c = {'A', 'B'}; String s = new String(c);` |
| `String(char[] a, int pos, int len)` | Crea un `String` prenent `len` caràcters a partir de la posició `pos`. | `String s = new String(c, 0, 1);` |

---

## 3. Mètodes principals de la classe `String`

La classe `String` ofereix desenes de mètodes d'utilitat per al processament de text:

| Mètode | Valor de retorn | Descripció | Exemple (`s = "Programació Java"`) |
| :--- | :---: | :--- | :--- |
| **`length()`** | `int` | Retorna el nombre de caràcters de la cadena. | `s.length()` $\rightarrow$ `16` |
| **`charAt(int i)`** | `char` | Retorna el caràcter situat a la posició `i` (de $0$ a $n-1$). | `s.charAt(0)` $\rightarrow$ `'P'` |
| **`substring(int inici)`** | `String` | Retorna la subcadena des de la posició `inici` fins al final. | `s.substring(12)` $\rightarrow$ `"Java"` |
| **`substring(int inici, int fi)`** | `String` | Retorna la subcadena des de `inici` fins a `fi - 1`. | `s.substring(0, 4)` $\rightarrow$ `"Prog"` |
| **`indexOf(String text)`** | `int` | Retorna la posició de la primera aparició de `text` (o `-1` si no hi és). | `s.indexOf("gra")` $\rightarrow$ `3` |
| **`indexOf(String text, int desDe)`** | `int` | Cerca la primera aparició de `text` a partir de la posició indicada. | `s.indexOf("a", 6)` $\rightarrow$ `8` |
| **`lastIndexOf(String text)`** | `int` | Retorna la posició de l'última aparició de `text` (o `-1`). | `s.lastIndexOf("a")` $\rightarrow$ `15` |
| **`toUpperCase()`** | `String` | Retorna una nova cadena convertida a majúscules. | `s.toUpperCase()` $\rightarrow$ `"PROGRAMACIÓ JAVA"` |
| **`toLowerCase()`** | `String` | Retorna una nova cadena convertida a minúscules. | `s.toLowerCase()` $\rightarrow$ `"programació java"` |
| **`trim()`** | `String` | Elimina els espais en blanc dels extrems inicial i final. | `"  hola  ".trim()` $\rightarrow$ `"hola"` |
| **`strip()`** | `String` | Versió moderna (Java 11+) de `trim()` que reconeix tots els espais Unicode. | `"  test  ".strip()` $\rightarrow$ `"test"` |
| **`startsWith(String prefix)`** | `boolean` | Retorna `true` si la cadena comença pel prefix especificat. | `s.startsWith("Pro")` $\rightarrow$ `true` |
| **`endsWith(String sufix)`** | `boolean` | Retorna `true` si la cadena acaba pel sufix especificat. | `s.endsWith("va")` $\rightarrow$ `true` |
| **`contains(CharSequence seq)`** | `boolean` | Comprova si conté la subcadena en qualsevol posició. | `s.contains("rama")` $\rightarrow$ `true` |
| **`equals(Object altre)`** | `boolean` | Compara el contingut exacte de dues cadenes (distingeix majúscules). | `s.equals("Hola")` $\rightarrow$ `false` |
| **`equalsIgnoreCase(String a)`** | `boolean` | Compara dues cadenes ignorant majúscules i minúscules. | `"HOLA".equalsIgnoreCase("hola")` $\rightarrow$ `true` |
| **`compareTo(String altre)`** | `int` | Comparació lexicogràfica ($0$ si són iguals, $<0$ si és menor, $>0$ si és major). | `"arbre".compareTo("barca")` $\rightarrow$ $<0$ |
| **`compareToIgnoreCase(String a)`** | `int` | Comparació alfabètica sense distingir majúscules/minúscules. | `"A".compareToIgnoreCase("a")` $\rightarrow$ `0` |
| **`replace(char vell, char nou)`** | `String` | Substitueix totes les aparicions d'un caràcter per un altre. | `"casa".replace('a', 'o')` $\rightarrow$ `"coso"` |
| **`split(String regex)`** | `String[]` | Divideix la cadena en un array de subcadenes segons un separador. | `"1,2,3".split(",")` $\rightarrow$ `{"1","2","3"}` |
| **`String.valueOf(tipus v)`** | `String` | Mètode estàtic que converteix qualsevol dada primitiva a cadena. | `String.valueOf(125)` $\rightarrow$ `"125"` |

---

## 4. Comparació de cadenes: `equals()` vs `==`

Un dels errors més comuns en aprendre Java és utilitzar l'operador d'igualtat relacional `==` per a comparar cadenes:

!!! danger "Molt important: Mai compares cadenes amb `==`"
    * L'operador **`==`** compara si dues referències apunten a la **mateixa adreça de memòria física**, no el seu contingut de text.
    * El mètode **`equals()`** compara el **contingut caràcter a caràcter** dels dos textos.

```java
String s1 = new String("hola");
String s2 = new String("hola");

if (s1 == s2) {
    IO.println("Són idèntics en memòria"); // NO s'executa! Són dos objectes diferents
}

if (s1.equals(s2)) {
    IO.println("Tenen el mateix text!"); // SÍ s'executa correctament
}
```

---

## 5. Exemples pràctics resolts

### Exemple 1: Processament de noms i extracció d'inicials

Llegeix el nom complet d'un usuari amb cognoms (per exemple, `"  garcia pérez, joan  "`), el neteja d'espais residuals, el divideix en paraules i genera les inicials en majúscules.

??? example "Solució en Java"
    ```java
    /*
     * Programa que processa una cadena de text, neteja espais amb trim(),
     * divideix paraules amb split() i extreu les inicials en majúscules.
     */
    void main() {
        IO.print("Introdueix el teu nom complet (Nom Cognom1 Cognom2): ");
        String linia = IO.readln().trim();

        // Dividim la cadena per un o més espais en blanc
        String[] paraules = linia.split(" ");
        String inicials = "";

        IO.println("\nParaules detectades:");
        for (String p : paraules) {
            if (!p.isEmpty()) {
                IO.println("- " + p);
                // Afegim la primera lletra en majúscula
                inicials += p.substring(0, 1).toUpperCase() + ".";
            }
        }

        IO.println("\nInicials generades: " + inicials);
    }
    ```

---

### Exemple 2: Comprovació de palíndroms

Un palíndrom és una paraula que es llegeix exactament igual d'esquerra a dreta que de dreta a esquerra (per exemple: `"radar"`, `"annna"`, `"reconèixer"`). El programa comprova si una paraula introduïda per teclat compleix aquesta condició.

??? example "Solució en Java"
    ```java
    /*
     * Programa que comprova si una paraula és un palíndrom
     * comparant els caràcters simètrics des dels extrems.
     */
    void main() {
        IO.print("Introdueix una paraula per a comprovar si és palíndrom: ");
        String paraula = IO.readln().trim().toLowerCase();

        boolean esPalindrom = true;
        int i = 0;
        int j = paraula.length() - 1;

        while (i < j && esPalindrom) {
            if (paraula.charAt(i) != paraula.charAt(j)) {
                esPalindrom = false;
            }
            i++;
            j--;
        }

        if (esPalindrom && !paraula.isEmpty()) {
            IO.println("La paraula \"" + paraula + "\" ÉS un palíndrom!");
        } else {
            IO.println("La paraula \"" + paraula + "\" NO és un palíndrom.");
        }
    }
    ```
