# Exercicis resolts de la UT4 (RA6)

En aquest apartat es recullen diversos exercicis pràctics resolts pas a pas corresponents als continguts de la **Unitat Temàtica 4: Arrays i cadenes de caràcters**.

Els exercicis abasten des del tractament bàsic de vectors unidimensionals, desplaçament i inserció ordenada d'elements, algorismes de fusió (*merge*), manipulació de caràcters i cadenes, fins a operacions amb matrius bidimensionals.

---

## Exercicis amb arrays unidimensionals

### Exercici 1: Classificació i mitjana de nombres positius i negatius

**Enunciat:**  
Creeu un programa que guarde en un array 10 nombres enters llegits des del teclat. A continuació, recorregueu l'array per a comptar quants valors són positius i quants negatius, calculant també la mitjana aritmètica de cadascun dels dos grups de manera independent.

??? example "Solució en Java"
    ```java
    /*
     * Programa que llegeix 10 enters en un array i calcula
     * quantitat i mitjana de positius i negatius per separat.
     */
    void main() {
        final int TOTAL = 10;
        int[] numeros = new int[TOTAL];
        int pos = 0, neg = 0;
        double sumaPos = 0.0, sumaNeg = 0.0;

        IO.println("Lectura dels elements de l'array:");
        for (int i = 0; i < numeros.length; i++) {
            IO.print("números[" + i + "] = ");
            numeros[i] = Integer.parseInt(IO.readln());
        }

        // Recorregut per a acumular i comptabilitzar
        for (int i = 0; i < numeros.length; i++) {
            if (numeros[i] > 0) {
                sumaPos += numeros[i];
                pos++;
            } else if (numeros[i] < 0) {
                sumaNeg += numeros[i];
                neg++;
            }
        }

        IO.println("\n--- RESULTATS ---");
        if (pos != 0) {
            IO.println("Mitjana dels valors positius: " + (sumaPos / pos));
        } else {
            IO.println("No s'han introduït números positius.");
        }

        if (neg != 0) {
            IO.println("Mitjana dels valors negatius: " + (sumaNeg / neg));
        } else {
            IO.println("No s'han introduït números negatius.");
        }
    }
    ```

---

### Exercici 2: Càlcul de la nota mitjana i filtrat d'alumnes destacats

**Enunciat:**  
Desenvolupeu un programa que demane inicialment el nombre d'alumnes d'una aula (garantint que siga un nombre positiu). A continuació, sol·licite la nota final de cadascun i la guarde en un vector de tipus `double`. El programa haurà de calcular la mitjana de la classe i finalment imprimir la llista detallada d'aquells estudiants la qualificació dels quals supere la mitjana del curs.

??? example "Solució en Java"
    ```java
    /*
     * Programa que gestiona les qualificacions d'una classe,
     * en calcula la mitjana i filtra les notes superiors a aquesta.
     */
    void main() {
        int numAlumnes;
        double suma = 0.0;

        do {
            IO.print("Número d'alumnes de la classe (> 0): ");
            numAlumnes = Integer.parseInt(IO.readln());
        } while (numAlumnes <= 0);

        double[] notes = new double[numAlumnes];

        // 1r Recorregut: Entrada de dades
        for (int i = 0; i < notes.length; i++) {
            IO.print("Nota final de l'alumne " + (i + 1) + ": ");
            notes[i] = Double.parseDouble(IO.readln());
        }

        // 2n Recorregut: Càlcul de la suma
        for (double n : notes) {
            suma += n;
        }

        double mitjana = suma / notes.length;
        IO.println("\nNota mitjana del curs: " + mitjana);

        // 3r Recorregut: Mostra els alumnes per damunt de la mitjana
        IO.println("\nLlistat d'alumnes amb nota superior a la mitjana:");
        for (int i = 0; i < notes.length; i++) {
            if (notes[i] > mitjana) {
                IO.println("Alumne núm. " + (i + 1) + " -> Nota: " + notes[i]);
            }
        }
    }
    ```

---

### Exercici 3: Lectura i impressió en ordre invers

**Enunciat:**  
Dissenyeu un programa que llegeixi 5 nombres per entrada estàndard, els emmagatzeme en un array i posteriorment els mostre per pantalla en ordre cronològicament invers a com van ser introduïts.

??? example "Solució en Java"
    ```java
    /*
     * Programa que llegeix 5 valors i els inverteix en pantalla.
     */
    void main() {
        int[] t = new int[5];

        for (int i = 0; i < t.length; i++) {
            IO.print("Introdueix el número " + (i + 1) + ": ");
            t[i] = Integer.parseInt(IO.readln());
        }

        IO.println("\nEls números en ordre invers són:");
        for (int i = t.length - 1; i >= 0; i--) {
            IO.print(t[i] + " ");
        }
        IO.println();
    }
    ```

---

### Exercici 4: Inserció d'un element amb desplaçament

**Enunciat:**  
Declareu un array de 10 elements enters. Llegiu per teclat 9 nombres i emmagatzemeu-los en les 9 primeres posicions (de la 0 a la 8). Després, sol·liciteu a l'usuari un nou valor i la posició (entre 0 i 8) on desitja inserir-lo. El programa haurà de desplaçar cap a la dreta tots els elements situats des d'aquella posició fins al final per a fer espai, inserir el nou element i finalment mostrar l'array resultant complet.

??? example "Solució en Java"
    ```java
    /*
     * Programa que insereix un nou valor en una posició indicada
     * desplaçant els elements posteriors cap a la dreta.
     */
    void main() {
        int[] t = new int[10];

        IO.println("Introdueix 9 nombres enters:");
        for (int i = 0; i < 9; i++) {
            IO.print("Element [" + i + "]: ");
            t[i] = Integer.parseInt(IO.readln());
        }

        IO.print("\nIntrodueix el nou element a inserir: ");
        int nou = Integer.parseInt(IO.readln());

        int pos;
        do {
            IO.print("Indica la posició on inserir-lo (0 a 8): ");
            pos = Integer.parseInt(IO.readln());
        } while (pos < 0 || pos > 8);

        // Desplacem els elements des de la posició 8 fins a 'pos' cap a la dreta
        for (int i = 8; i >= pos; i--) {
            t[i + 1] = t[i];
        }

        // Inserim el nou número en el buit generat
        t[pos] = nou;

        IO.println("\nL'array resultant amb 10 elements és:");
        for (int i = 0; i < t.length; i++) {
            IO.print(t[i] + " ");
        }
        IO.println();
    }
    ```

---

### Exercici 5: Inserció en un vector ordenat

**Enunciat:**  
Creeu un programa que llegeixi 5 nombres enters introduïts per teclat en ordre creixent i els guarde en un array de 10 posicions. A continuació, sol·liciteu un nou nombre enter i determineu la posició exacta on s'ha d'inserir per tal que la seqüència mantinga el seu ordre creixent, desplaçant els elements que calga. Mostreu finalment la sèrie ordenada resultant (amb 6 elements).

??? example "Solució en Java"
    ```java
    /*
     * Programa que manté l'ordre d'un vector en inserir un nou valor.
     */
    void main() {
        int[] t = new int[10];

        IO.println("Introdueix 5 nombres en ordre creixent:");
        for (int i = 0; i < 5; i++) {
            IO.print("Element [" + i + "]: ");
            t[i] = Integer.parseInt(IO.readln());
        }

        IO.print("\nNúmero a inserir entre els anteriors: ");
        int num = Integer.parseInt(IO.readln());

        // Cerquem la posició (lloc) on ha d'anar el nou element
        int lloc = 0;
        int j = 0;
        while (j < 5 && t[j] < num) {
            lloc++;
            j++;
        }

        // Desplacem els elements des del final (posició 4) fins a 'lloc' cap a la dreta
        for (int i = 4; i >= lloc; i--) {
            t[i + 1] = t[i];
        }

        // Col·loquem el nou valor en la seua posició ordenada
        t[lloc] = num;

        IO.println("\nLa nova sèrie ordenada queda:");
        for (int i = 0; i < 6; i++) {
            IO.print(t[i] + " ");
        }
        IO.println();
    }
    ```

---

### Exercici 6: Fusió de dos vectors ordenats (*Merge*)

**Enunciat:**  
Creeu un programa que sol·licite a l'usuari dos arrays $A$ i $B$ de 5 nombres enters cadascun, tots dos ordenats de forma creixent. El programa ha de fusionar ambdós vectors en un tercer array $C$ de 10 elements de manera que el resultat final quede completament ordenat des del primer moment, sense necessitat d'ordenar $C$ a posteriori.

??? example "Solució en Java"
    ```java
    /*
     * Algorisme de fusió (Merge) de dos vectors ordenats.
     */
    void main() {
        int[] a = new int[5];
        int[] b = new int[5];
        int[] c = new int[10];

        IO.println("Introdueix 5 valors ordenats per al vector A:");
        for (int i = 0; i < 5; i++) {
            IO.print("A[" + i + "]: ");
            a[i] = Integer.parseInt(IO.readln());
        }

        IO.println("\nIntrodueix 5 valors ordenats per al vector B:");
        for (int i = 0; i < 5; i++) {
            IO.print("B[" + i + "]: ");
            b[i] = Integer.parseInt(IO.readln());
        }

        // Algorisme de fusió: comparem els caps de tots dos vectors
        int i = 0; // Índex per a A
        int j = 0; // Índex per a B
        int k = 0; // Índex per a C

        while (i < 5 && j < 5) {
            if (a[i] < b[j]) {
                c[k] = a[i];
                i++;
            } else {
                c[k] = b[j];
                j++;
            }
            k++;
        }

        // Copiem els elements residuals que queden pendents
        if (i == 5) {
            // A ha acabat, afegim la resta de B
            while (j < 5) {
                c[k] = b[j];
                j++;
                k++;
            }
        } else {
            // B ha acabat, afegim la resta de A
            while (i < 5) {
                c[k] = a[i];
                i++;
                k++;
            }
        }

        IO.println("\nArray C resultant fusionat i ordenat:");
        for (int x = 0; x < c.length; x++) {
            IO.print(c[x] + " ");
        }
        IO.println();
    }
    ```

---

## Exercicis amb arrays de caràcters i cadenes

### Exercici 7: Eliminació de caràcters amb compactació

**Enunciat:**  
Implementeu un programa que elimine un caràcter determinat d'un array de tipus `char[]` (per exemple, la lletra `'l'`). L'algorisme ha de compactar els caràcters vàlids cap a l'esquerra per tal de no deixar buits i col·locar el caràcter nul `'\0'` al final de la seqüència útil resultant.

??? example "Solució en Java"
    ```java
    /*
     * Programa que elimina un caràcter d'un vector char[]
     * compactant la informació amb caràcter nul sentinella.
     */
    void main() {
        char[] s = {'H', 'o', 'l', 'a'};
        char eliminar = 'l';

        IO.print("Text original: ");
        IO.println(s);

        int j = 0; // Punter d'escriptura
        for (int i = 0; i < s.length; i++) {
            if (s[i] != eliminar) {
                s[j] = s[i];
                j++;
            }
        }

        // Marquem el nou final amb el caràcter nul si s'ha reduït la mida
        if (j < s.length) {
            s[j] = '\0';
        }

        IO.print("Text netejat: ");
        for (int i = 0; i < s.length && s[i] != '\0'; i++) {
            IO.print(s[i]);
        }
        IO.println(); // Eixida: Hoa
    }
    ```

---

### Exercici 8: Càlcul de la lletra del DNI

**Enunciat:**  
Desenvolupeu un programa que demane un número de DNI de 8 dígits (com a text o com a enter) i calcule la lletra que li correspon d'acord amb la fórmula oficial: la lletra s'obté buscant en una taula predefinida l'índex corresponent al residu de la divisió del número entre 23 (`numero % 23`). Mostreu el document complet (número i lletra units per un guió).

??? example "Solució en Java"
    ```java
    /*
     * Programa que calcula la lletra del DNI amb vector de caràcters i mòdul 23.
     */
    void main() {
        char[] taulaLletres = {
            'T', 'R', 'W', 'A', 'G', 'M', 'Y', 'F', 'P', 'D', 'X',
            'B', 'N', 'J', 'Z', 'S', 'Q', 'V', 'H', 'L', 'C', 'K', 'E'
        };

        String dniStr;
        do {
            IO.print("Introdueix les 8 xifres del DNI: ");
            dniStr = IO.readln().trim();
        } while (dniStr.length() != 8 || !dniStr.matches("\\d{8}"));

        int numDni = Integer.parseInt(dniStr);
        int modul = numDni % 23;
        char lletra = taulaLletres[modul];

        IO.println("DNI complet: " + numDni + "-" + lletra);
    }
    ```

---

## Exercicis amb matrius bidimensionals

### Exercici 9: Intercanvi de files d'una matriu

**Enunciat:**  
Escriu un programa que, donada una matriu rectangular de $4 \times 4$ enters, demane a l'usuari l'índex de dues files $i$ i $j$ i n'intercanvie completament els seus continguts mitjançant una variable auxiliar. Mostreu la matriu abans i després de l'operació.

??? example "Solució en Java"
    ```java
    /*
     * Programa que intercanvia dues files d'una matriu.
     */
    void main() {
        int[][] matriu = {
            {3,  5, -1, 6},
            {2,  6,  8, 2},
            {12, 4,  1, 1},
            {1,  6,  4, 2}
        };

        IO.println("--- Matriu inicial ---");
        for (int i = 0; i < matriu.length; i++) {
            for (int j = 0; j < matriu[i].length; j++) {
                IO.print(matriu[i][j] + "\t");
            }
            IO.println();
        }

        IO.print("\nIntrodueix la primera fila a intercanviar (0 a 3): ");
        int f1 = Integer.parseInt(IO.readln());

        IO.print("Introdueix la segona fila a intercanviar (0 a 3): ");
        int f2 = Integer.parseInt(IO.readln());

        if (f1 >= 0 && f1 < matriu.length && f2 >= 0 && f2 < matriu.length) {
            // Intercanviem columna per columna entre les dues files
            for (int k = 0; k < matriu[f1].length; k++) {
                int aux = matriu[f1][k];
                matriu[f1][k] = matriu[f2][k];
                matriu[f2][k] = aux;
            }

            IO.println("\n--- Matriu després de l'intercanvi ---");
            for (int i = 0; i < matriu.length; i++) {
                for (int j = 0; j < matriu[i].length; j++) {
                    IO.print(matriu[i][j] + "\t");
                }
                IO.println();
            }
        } else {
            IO.println("Error: Índexs de fila fora de rang.");
        }
    }
    ```

---

### Exercici 10: Suma de dues matrius $3 \times 3$

**Enunciat:**  
Creeu un programa que demane els elements de dues matrius $A$ i $B$ de dimensions $3 \times 3$, en calcule la matriu suma (on cada posició és la suma algebraica dels elements homòlegs $A[i][j] + B[i][j]$) i mostre per pantalla la matriu resultant en format tabular.

??? example "Solució en Java"
    ```java
    /*
     * Programa que suma dues matrius 3x3 de nombres enters.
     */
    void main() {
        final int MIDA = 3;
        int[][] a = new int[MIDA][MIDA];
        int[][] b = new int[MIDA][MIDA];
        int[][] suma = new int[MIDA][MIDA];

        IO.println("Dades de la matriu A:");
        for (int i = 0; i < MIDA; i++) {
            for (int j = 0; j < MIDA; j++) {
                IO.print("A[" + i + "][" + j + "]: ");
                a[i][j] = Integer.parseInt(IO.readln());
            }
        }

        IO.println("\nDades de la matriu B:");
        for (int i = 0; i < MIDA; i++) {
            for (int j = 0; j < MIDA; j++) {
                IO.print("B[" + i + "][" + j + "]: ");
                b[i][j] = Integer.parseInt(IO.readln());
            }
        }

        // Càlcul de la suma
        for (int i = 0; i < MIDA; i++) {
            for (int j = 0; j < MIDA; j++) {
                suma[i][j] = a[i][j] + b[i][j];
            }
        }

        IO.println("\nMatriu Resultant (A + B):");
        for (int i = 0; i < MIDA; i++) {
            for (int j = 0; j < MIDA; j++) {
                IO.print(suma[i][j] + "\t");
            }
            IO.println();
        }
    }
    ```
