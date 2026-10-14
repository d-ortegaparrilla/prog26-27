# Exercicis resolts de la UT2

En aquest apartat es recullen diversos exercicis resolts pas a pas corresponents als continguts de la **Unitat Temàtica 2: Estructures de control**. S'inclouen tant resolucions mitjançant algorismes (pseudocodi i taules de variables) com la seua implementació en llenguatge **Java**.

---

## Estructures condicionals

### Exercici 1: Càlcul de tarifes de banquets ("La llagosta fumada")

**Enunciat:**  
El restaurant "La llagosta fumada" està especialitzat en l'organització de banquets. Aplica les tarifes següents segons el nombre de comensals ($NP$):

* El preu estàndard del plat per persona és de **20 €**.
* Si el nombre de persones és **superior a 200 però menor o igual a 300**, el preu per plat es redueix a **15 €**.
* Per a esdeveniments de **més de 300 persones**, el preu per plat és de **10 €**.

Dissenyeu un algorisme mitjançant pseudocodi i implementeu-lo en Java per a calcular el pressupost total ($TOT$) que cal presentar al client en funció dels assistents previstos.

??? tip "Taula de variables i pseudocodi"
    #### Taula de variables
    | Nom variable | Descripció | Tipus |
    | :--- | :--- | :--- |
    | `NP` | Nombre de persones / comensals | Enter |
    | `TOT` | Pressupost total a pagar pel banquet | Real |

    #### Pseudocodi
    ```text
    1. Inici
    2. Llegir NP
    3. Si NP > 300 Aleshores
           Fer TOT = NP * 10
       Si no
           Si NP > 200 Aleshores
               Fer TOT = NP * 15
           Si no
               Fer TOT = NP * 20
           Fi Si
       Fi Si
    4. Escriure "El pressupost total és: ", TOT
    5. Fi
    ```

??? example "Solució en Java"
    ```java
    /*
     * Programa que calcula el pressupost d'un banquet en funció
     * del nombre de comensals amb tarifes escalonades.
     */
    void main() {
        int np;
        double tot;

        IO.print("Introdueix el nombre de persones per al banquet: ");
        np = Integer.parseInt(IO.readln());

        if (np > 300) {
            tot = np * 10.0;
        } else if (np > 200) {
            tot = np * 15.0;
        } else {
            tot = np * 20.0;
        }

        IO.println("El pressupost total és de: " + tot + " €");
    }
    ```

---

### Exercici 2: Estacions de l'any segons el mes (`switch`)

**Enunciat:**  
Creeu un programa que demane a l'usuari un número de mes (de l'1 al 12), determine a quina estació de l'any pertany i la mostre per pantalla:

* **Hivern:** Desembre (12), Gener (1), Febrer (2).
* **Primavera:** Març (3), Abril (4), Maig (5).
* **Estiu:** Juny (6), Juliol (7), Agost (8).
* **Tardor:** Setembre (9), Octubre (10), Novembre (11).

Si l'usuari introdueix un número fora del rang 1..12, cal mostrar un missatge d'error.

??? example "Solució en Java (Instrucció clàssica `switch`)"
    ```java
    /*
     * Programa que calcula l'estació de l'any a partir del número de mes
     * emprant l'agrupació de casos en una instrucció switch clàssica.
     */
    void main() {
        int mes;
        String estacio;

        IO.print("Indica el número del mes (1-12): ");
        mes = Integer.parseInt(IO.readln());

        switch (mes) {
            case 12, 1, 2:
                estacio = "Hivern";
                break;
            case 3, 4, 5:
                estacio = "Primavera";
                break;
            case 6, 7, 8:
                estacio = "Estiu";
                break;
            case 9, 10, 11:
                estacio = "Tardor";
                break;
            default:
                estacio = "error";
        }

        if (estacio.equals("error")) {
            IO.println("Número de mes incorrecte! Ha de ser entre 1 i 12.");
        } else {
            IO.println("Estem a: " + estacio);
        }
    }
    ```

??? tip "Versió alternativa moderna: Expressió `switch` amb fletxa `->`"
    En les versions modernes de Java podem utilitzar el `switch` com a expressió directa per assignar el valor a la variable de manera molt més concisa:

    ```java
    void main() {
        IO.print("Indica el número del mes (1-12): ");
        int mes = Integer.parseInt(IO.readln());

        String estacio = switch (mes) {
            case 12, 1, 2  -> "Hivern";
            case 3, 4, 5   -> "Primavera";
            case 6, 7, 8   -> "Estiu";
            case 9, 10, 11 -> "Tardor";
            default        -> "Mes invàlid";
        };

        IO.println("Resultat: " + estacio);
    }
    ```

---

## Estructures repetitives

### Exercici 3: Càlcul de la mitjana d'edats (Comparativa dels 3 bucles)

**Enunciat:**  
Es requereix un algorisme per a obtindre l'edat mitjana (`PROMEDIO`) d'un grup de `NUMA` alumnes, valor que es demana inicialment per teclat. L'edat de cada alumne la denominem `EA`.  
Dissenyeu les solucions en pseudocodi emprant els tres tipus de bucles (`Mentre`, `Repeteix fins a` i `Des de... fins a`), i la corresponent implementació en Java.

??? tip "Taula de variables i pseudocodi dels 3 cicles"
    #### Taula de variables
    | Nom variable | Descripció | Tipus |
    | :--- | :--- | :--- |
    | `NUMA` | Nombre total d'alumnes | Enter |
    | `C` | Comptador d'iteracions | Enter |
    | `EA` | Edat de cada alumne llegida | Enter |
    | `SUMA` | Acumulador de les edats | Enter |
    | `PROMEDIO` | Edat mitjana resultant | Real |

    === "a) Cicle Mentre (while)"
        ```text
        1. Inici
        2. Fer SUMA = 0
        3. Llegir NUMA
        4. Fer C = 1
        5. Mentre C <= NUMA fer
               Llegir EA
               Fer SUMA = SUMA + EA
               Fer C = C + 1
           Fi Mentre
        6. Fer PROMEDIO = SUMA / NUMA
        7. Escriure "L'edat mitjana és: ", PROMEDIO
        8. Fi
        ```

    === "b) Cicle Repeteix fins a (do-while)"
        ```text
        1. Inici
        2. Fer SUMA = 0
        3. Llegir NUMA
        4. Fer C = 1
        5. Repeteix
               Llegir EA
               Fer SUMA = SUMA + EA
               Fer C = C + 1
           Fins a C > NUMA
        6. Fer PROMEDIO = SUMA / NUMA
        7. Escriure "L'edat mitjana és: ", PROMEDIO
        8. Fi
        ```

    === "c) Cicle Des de... fins a (for)"
        ```text
        1. Inici
        2. Fer SUMA = 0
        3. Llegir NUMA
        4. Des de C = 1 fins a NUMA fer
               Llegir EA
               Fer SUMA = SUMA + EA
           Fi Des de
        5. Fer PROMEDIO = SUMA / NUMA
        6. Escriure "L'edat mitjana és: ", PROMEDIO
        7. Fi
        ```

??? example "Solució en Java"
    Com que coneixem per endavant el nombre exacte de repeticions (`numa`), l'estructura més idònia en Java és el bucle `for`:

    ```java
    /*
     * Programa que calcula l'edat mitjana d'un grup d'alumnes
     * utilitzant un bucle for.
     */
    void main() {
        int numa;
        int suma = 0;
        double mitjana;

        IO.print("Quants alumnes hi ha al grup?: ");
        numa = Integer.parseInt(IO.readln());

        for (int c = 1; c <= numa; c++) {
            IO.print("Introdueix l'edat de l'alumne " + c + ": ");
            int ea = Integer.parseInt(IO.readln());
            suma = suma + ea;
        }

        mitjana = (double) suma / numa;
        IO.println("L'edat mitjana del grup és: " + mitjana);
    }
    ```

---

### Exercici 4: Cerca del valor màxim amb sentinella ("L'arbre més alt")

**Enunciat:**  
Un centre d'investigació de la flora urbana necessita una aplicació que permeta registrar l'alçada en centímetres d'un conjunt d'arbres i determine quin és l'arbre més alt i quina és la seua etiqueta identificativa.

* Els arbres s'identifiquen mitjançant números correlatius començant pel `0`.
* L'entrada de dades finalitza quan l'usuari introdueix el valor sentinella `-1`.
* Cal tindre en compte el cas en què l'usuari introduïsca directament `-1` en el primer arbre (no hi ha arbres mesurats).

??? example "Solució en Java"
    ```java
    /*
     * Programa que cerca l'arbre més alt mitjançant un bucle while
     * controlat per sentinella (-1).
     */
    void main() {
        int altura;
        int etiqueta = 0;

        int alturaArbreMesAlt = -1;
        int etiquetaArbreMesAlt = -1;

        IO.print("Alçada de l'arbre (etiqueta " + etiqueta + ") en cm (-1 per finalitzar): ");
        altura = Integer.parseInt(IO.readln());

        // El primer arbre serà inicialment el més alt
        alturaArbreMesAlt = altura;
        etiquetaArbreMesAlt = etiqueta;

        while (altura != -1) {
            // Comprovem si l'arbre actual és més alt que el màxim guardat
            if (altura > alturaArbreMesAlt) {
                alturaArbreMesAlt = altura;
                etiquetaArbreMesAlt = etiqueta;
            }

            etiqueta++;
            IO.print("Alçada de l'arbre (etiqueta " + etiqueta + ") en cm (-1 per finalitzar): ");
            altura = Integer.parseInt(IO.readln());
        }

        if (etiquetaArbreMesAlt == -1 || alturaArbreMesAlt == -1) {
            IO.println("No s'ha introduït cap arbre.");
        } else {
            IO.println("--- RESULTAT ---");
            IO.println("L'arbre més alt mesura: " + alturaArbreMesAlt + " cm.");
            IO.println("Etiqueta de l'arbre: " + etiquetaArbreMesAlt);
        }
    }
    ```

---

### Exercici 5: Triangle rectangle d'asteriscs (Bucles niats)

**Enunciat:**  
Creeu un programa que demane a l'usuari la mida del catet d'un triangle (nombre de línies) i dibuixe per pantalla un triangle rectangle sòlid format per asteriscs (`* `), utilitzant bucles niats.

*Exemple d'eixida per a catet = 4:*
```text
* 
* * 
* * * 
* * * * 
```

??? example "Solució en Java"
    ```java
    /*
     * Programa que dibuixa un triangle rectangle d'asteriscs
     * mitjançant dos bucles for niats.
     */
    void main() {
        int catet;

        do {
            IO.print("Introdueix la longitud del catet (> 0): ");
            catet = Integer.parseInt(IO.readln());
        } while (catet <= 0);

        // Bucle extern: controla les files
        for (int fila = 0; fila < catet; fila++) {
            // Bucle intern: imprimeix els asteriscs corresponents a la fila actual
            for (int col = 0; col <= fila; col++) {
                IO.print("* ");
            }
            IO.println(); // Salt de línia al final de cada fila
        }
    }
    ```
