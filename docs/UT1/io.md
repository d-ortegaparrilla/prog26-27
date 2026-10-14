# Entrada i eixida de dades.

## Classe IO.
La classe IO s'ha introduït en la versió 25 LTS. Permet la impresió senz

## Classe Scanner per a lectura de dades.

La classe Scanner es troba disponible a partir de Java 5 i facilita la lectura de dades en els programes Java.

Primer veurem diversos exemples de lectura de dades en Java amb Scanner i després explicarem en detall com funciona.

Per a utilitzar Scanner en el programa haurem de fer el següent:

1. Escriure l'import

La classe Scanner es troba en el paquet `java.util`, per tant s'ha d'incloure a l'inici del programa la instrucció:

```java
import java.util.Scanner;
```

2. Crear un objecte Scanner

Hem de crear un objecte de la classe Scanner associat al dispositiu d'entrada. Si el dispositiu d'entrada és el teclat (el més freqüent), escriurem:

```java
Scanner sc = new Scanner(System.in);
```

S'ha creat l'objecte `sc` associat al teclat representat per `System.in`.

3. Una vegada fet açò podem llegir dades introduïdes per teclat. Per a llegir podem usar el mètode `nextXxx()` on `Xxx` indica el tipus, per exemple `nextInt()` per a llegir un enter, `nextDouble()` per a llegir un double, etc.

**Exemples de lectura**:

Exemple de lectura per teclat d'un número enter:

```java
int n;
System.out.println("Introduïu un número enter: ");
n = sc.nextInt(); // assigna a la variable n el número int introduït per teclat
```

Exemple de lectura per teclat d'un número tipus double:

```java
double x;
System.out.print("Introduïu un número de tipus double: ");
x = sc.nextDouble(); // assigna a la variable x el número double introduït per teclat
```

Exemple de lectura d'una cadena de caràcters:

```java
String s;
System.out.print("Introduïu text: ");
s = sc.nextLine(); // assigna a la variable s l'String introduït per teclat
```

Exemple de lectura d'un número de tipus long:

```java
long ln;
System.out.print("Introduïu un número: ");
ln = sc.nextLong(); // assigna a la variable ln el número long introduït per teclat
```

Exemple de lectura d'un caràcter:

```java
char c;
System.out.print("Introduïu un caràcter: ");
c = sc.next().charAt(0); // assigna a la variable c el primer caràcter (caràcter 0) de la cadena introduïda per teclat
```

**Exemple de programa amb lectura de dades amb Scanner**:

El programa ha de sol·licitar a l'usuari el nom de la persona i mostrar-lo per pantalla. Seguidament llig per teclat el radi d'una circumferència de tipus double i en mostra la longitud. A més, llig un enter i mostra el valor d'elevar-lo al quadrat.

```java
import java.util.Scanner;

void main() {
    Scanner sc = new Scanner(System.in); // crear un objecte Scanner
    String nom;
    double radi;
    int n;


    System.out.print("Introduïu el vostre nom: ");
    nom = sc.nextLine(); // llegir un String
    System.out.println("Hola " + nom + "!!!");

    System.out.print("Introduïu el radi de la circumferència: ");
    radi = sc.nextDouble(); // llegir un double
    System.out.println("Longitud de la circumferència: " + 2 * Math.PI * radi);

    System.out.print("Introduïu un número enter: ");
    n = sc.nextInt(); // llegir un enter
    System.out.println("El quadrat és: " + Math.pow(n, 2));
    
}
```


Funcionament de la classe Scanner.

És important conéixer el funcionament intern de la classe Scanner per a poder realitzar les operacions de lectura de manera correcta. De manera resumida, el procés de lectura per teclat en un programa Java és el següent:

Les dades que s'introduïxen des del teclat s'emmagatzemen en una zona de memòria que anomenarem búfer (buffer). Mitjançant un flux de dades (stream) estes dades passen al programa.

Un stream o flux de dades és un objecte que fa d'intermediari entre el programa i l'origen o la destinació de les dades. El programa llig de l'stream o escriu en ell, sense importar-li d'on procedixen les dades físicament o cap a quin dispositiu es dirigixen realment.

Un stream està format per una seqüència de bytes utilitzats per a l'entrada o eixida d'un programa.

Java crea de manera automàtica els següents streams quan s'executa un programa:

    System.in: stream d'entrada connectat al teclat.

    System.out: stream d'eixida connectat al monitor.

    System.err: stream d'eixida connectat al monitor per a missatges d'error.

A més d'estos streams estàndard, Java proporciona una gran quantitat de classes per a streams que permeten llegir i escriure en fitxers.

Quan en el programa apareix una instrucció de lectura d'una dada per teclat, s'accedix al búfer d'entrada a la recerca de la dada. Si la troba, l'extrau del búfer i la incorpora al programa.

Si la dada no ha sigut trobada en el búfer, generalment es deurà al fet que el búfer està buit. Esta és la situació més habitual. En este cas el programa espera que l'usuari introduïsca la dada per teclat. Quan l'usuari la introduïx i prem retorn (intro), aleshores s'extrau el valor introduït del búfer i s'incorpora al programa.

Si la dada trobada no és del tipus esperat o d'un tipus compatible es produïx un error. Açò ocorre, per exemple, quan s'està executant el mètode nextInt() per a extreure un enter del búfer i s'introduïx un double o un char. El tipus de dada trobada en el búfer no coincidix amb el tipus que es vol llegir.

Com netejar el búfer d'entrada en Java.

Podem netejar el búfer mitjançant dos mètodes:

    next(): extrau del búfer el següent testimoni (token) en forma d'String. Hem de tindre en compte que este mètode només extrau un testimoni; si n'hi haguera més, romandrien en el búfer.

    nextLine(): extrau del búfer un String amb tot el contingut del búfer fins a trobar un salt de línia (\n), el qual es produïx en prémer retorn (intro). El salt de línia no s'inclou en l'String retornat. Este caràcter \n s'elimina del búfer.

Quan s'introduïxen dades de diferent tipus des del teclat hi haurà situacions en què serà necessari eliminar totalment el contingut del búfer d'entrada. D'una altra manera la lectura de dades no es realitzarà de manera correcta, en particular quan s'intente introduir dades de tipus String.

Exemple: Programa que llig per teclat el nom, edat i adreça d'una persona i ho mostra per pantalla.
Java

import java.util.Scanner;

public class Exemple2Scanner {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String nom, adreca;
        int edat;

        System.out.print("Introduïu el vostre nom: ");
        nom = sc.nextLine(); // llegir el nom
        System.out.print("Introduïu la vostra edat: ");
        edat = sc.nextInt(); // llegir l'edat
        System.out.print("Introduïu la vostra adreça: ");
        adreca = sc.nextLine(); // llegir l'adreça

        System.out.println("Dades introduïdes");
        System.out.println("Nom: " + nom);
        System.out.println("Edat: " + edat);
        System.out.println("Adreça: " + adreca);
    }
}

Si l'executem veiem que la lectura de dades no es realitza de manera correcta:
Plaintext

Introduïu el vostre nom: Joan Redondo
Introduïu la vostra edat: 25
Introduïu la vostra adreça: Dades introduïdes
Nom: Joan Redondo
Edat: 25
Adreça: 

S'ha llegit per teclat el nom i l'edat, però el programa no s'ha detingut perquè l'usuari introduïsca l'adreça, per la qual cosa la variable adreca es queda sense valor.

L'explicació al que ha ocorregut:

    Primer s'introduïx el nom per teclat.

    La següent operació de lectura per teclat és l'edat.

    Després de llegir l'edat amb nextInt(), el salt de línia (intro) roman en el búfer; si després intentem llegir un String amb nextLine(), este consumix directament el salt de línia pendent sense esperar que l'usuari escriga res.

La solució és senzilla: netejar el búfer després de llegir el número enter mitjançant el mètode sc.nextLine();.

El programa quedaria així:
Java

import java.util.Scanner;

public class Exemple2Scanner {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String nom, adreca;
        int edat;

        System.out.print("Introduïu el vostre nom: ");
        nom = sc.nextLine(); // llegir el nom
        System.out.print("Introduïu la vostra edat: ");
        edat = sc.nextInt(); // llegir l'edat

        sc.nextLine(); // netejar el búfer d'entrada

        System.out.print("Introduïu la vostra adreça: ");
        adreca = sc.nextLine(); // llegir l'adreça

        System.out.println("Dades introduïdes");
        System.out.println("Nom: " + nom);
        System.out.println("Edat: " + edat);
        System.out.println("Adreça: " + adreca);
    }
}

Ara, després d'introduir l'edat, el mètode nextLine() elimina el caràcter de retorn que havia quedat en el búfer, de manera que la lectura de l'adreça es realitza correctament:
Plaintext

Introduïu el vostre nom: Joan Redondo
Introduïu la vostra edat: 25
Introduïu la vostra adreça: C/ Major 134 - València.
Dades introduïdes
Nom: Joan Redondo
Edat: 25
Adreça: C/ Major 134 - València.

En general, cal netejar el búfer d'entrada de Scanner quan hàgem d'introduir una dada de tipus String mitjançant nextLine() després d'haver introduït una dada de tipus numèric (o amb mètodes que no consumixen el salt de línia com next(), nextInt(), etc.).