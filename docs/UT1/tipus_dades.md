# Tipus de dades i literals en Java.
## Tipus de dades en Java
Una dada sempre porta associada un tipus de dada, que determina el conjunt de valors que pot prendre.
A Java tota la informació que utilitza un programa està representada per dos tipus principals de dades:

1. Dades de tipus bàsic o primitiu.
2. Referències a objectes.

Els tipus de dades bàsiques o primitives no són objectes i es poden fer servir directament en un programa sense necessitat de crear objectes d'aquest tipus. La biblioteca Java disposa de classes associades a aquests tipus que proporcionen mètodes per facilitar-ne el maneig. 
Els tipus de dades primitives que suporta Java són:

| Tipus de dada | Representació | Grandària (bytes) | Rang de valors | Valor per defecte | Classe associada |
| ------------- | ------------- | ----------------- | -------------- | ----------------- | ---------------- |
| byte    | Número enter amb signe  | 1 | -128 a 127                                 | 0 | Byte    |
| short   | Número entero amb signe |	2 |	-32768 a 32767                             | 0 | Short   |
| int     | Número entero amb signe | 4 |	-2147483648 a 2147483647                   | 0 | Integer |
| long    | Número entero amb signo | 8 |	-9223372036854775808 a 9223372036854775807 | 0 | Long    |
| float   | Número en coma flotant de precisió simple. Norma IEEE 754 | 4 | ± 3.4x10-38 a ± 3.4x1038   | 0.0 | Float |
| double  | Número en coma flotant de precisió doble. Norma IEEE 754  | 8 | ± 1.8x10-308 a ± 1.8x10308 |	0.0 | Double |
| char    | Caràcter Unicode	| 2 | \u0000 a \uFFFF | \u0000 | Character |
| boolean |	Dada lògic	| no definit | true ó false | false | Boolean |
| void    |	- |	- |	- |	- |	Void |

### Dades numèriques enteres.

Les dades numèriques són representades en Java pels tipus: `byte`, `short`, `int`, `long`. El tipus de dada numèric enter és un subconjunt finit dels números enters del món real. Poden ser positius o negativus.

Exemple de declaració de variables enteres:

```java
int a;
byte n1, n2;
short x;
```


### Dades numèriques reals.
En Java els representen els tipus: `float`, `double`. El tipus de dada numèric real és un subconjunt finit dels números reals. Sempre porten un punt decimal i també poden ser positius o negatius. Els números reals tenen una part entera i una part decimal.

Per exemple: 0.08   -54.0001

Exemple de declaració de variables reals:

```java
float pes;
double longitud;
float altura = 2.5F;
double area = 1.7E4; //equival a 1.7 * 104
double z = .123; //si la part entera és 0 es pot ometre
```

!!! warning "Sufix `F` obligatori per a literals `float`"
    En Java, qualsevol número amb punt decimal (com `2.5`) s'interpreta per defecte com a `double` (64 bits). Si s'assigna a una variable `float` (32 bits) sense afegir el sufix `F` o `f` (`float altura = 2.5F;`), el compilador indicarà un error de possible pèrdua de precisió.


### Dades de tipus caràcter.
En Java es representa amb el tipus `char`. Una dada de tipus caràcter s'utilitza per a representar un caràcter dins el rang \u0000 a \uFFFF (números des de 0 fins al 65535) en Unicode.

En Java s'utilitza el codi Unicode per a la representació de caràcters. Aquest codi actualment representa els caràcters de la majoria d'idiomes escrits en tot el món. Els 127 primers caràcters d'Unicode corresponen al codi ASCII.

El codi ASCII (American Standard Code for Information Interchange) assigna valors numèrics a les lletres, números, signes de puntuació i alguns altres caràcters especiales.

Debut a la limitació de la seua grandària, el codi ASCII no és suficient per a representar caràcters no existents a l'alfabet anglès. 

Exemple de declaració de variables de tipus caràcter:

```java
char car;
char lletra1 = 'z';
char lletra = '\u0061'; //codi unicode del caràcter 'a'
```

### Dades de tipus lògic.
Es representen amb el tipus `boolean`. Les dades d'aquest tipus sols poden contindre dos valors: `true` (vertader) o `false` (fals).

Exemple de declaració de variables lògiques:

```java
boolean primer;
boolean parell = false;
```

Els tipus de dades lògics són també coneguts com a **booleans**, en honor del matemàtic anglès *George Boole*, que va desenvolupar la teoria coneguda com a àlgebra de boole, que va ser la base per a la representació dels circuits lògics.

### Dades de tipus enumerat.
De vegades, una variable només ha de contenir un conjunt restringit de valors. Per exemple, pots vendre roba o pizzes en quatre talles: petita, mitjana, gran i extragran. És clar que podries codificar aquestes talles com a nombres enters (1, 2, 3, 4) o com a caràcters (S, M, L, X), però aquesta és una solució propensa a errors. És massa fàcil que una variable acabe tenint un valor incorrecte (com un 0 o una m).

Es pot definir el teu propi tipus enumerat sempre que es presente una situació així. Un tipus enumerat té un nombre finit de valors amb nom. Per exemple:

```java
enum Size { SMALL, MEDIUM, LARGE, EXTRA_LARGE };
```

Ara es podrien declarar variables d'aquest tipus:

```java
Size s = Size.MEDIUM;
```

Una variable de tipus `Size` només pot contenir un dels valors llistats en la declaració del tipus, o bé el valor especial `null`, que indica que la variable no té assignat cap valor.

## Literals en Java. Variables i constants.
### Literals.
Un literal és un valor de tipus enter, real, lògic, caràcter, cadena de caràcters o un valor nul (null) que pot aparéixer dins d'un programa.

Per exemple: 150, 12.4, "ANA", null, 't'

Els literals solen aparéixer en l'assignació de valors a les variables o formant part d'expressions aritmètiques o lògiques. Per exemple:

```java
x = 25;
preu = 120.99;
mes = "gener";
descompte = preu - (preu * 5 / 100);
valor = (a > 3 && a < 5);
```

Quan s'utilitzen literals, és molt important tindre en compte que Java és un **llenguatge fortament tipat**, això vol dir que fa un control estricte dels tipus de dades que poden contindre les variables.

Per exemple, si una variable s'ha declarat com a `int` no podrem assignar-li un valor de tipus `double`.

```java
int n = 2.5; // Esta assignació no és correcta i provocarà un error.
```

Esta assignació provocaria un error, ja que estem assignant un valor no enter (2.5) a una variable declarada com a `int`. Per tant, és molt important saber de quin tipus és un literal per a treballar de manera correcta amb ells i no obtindre resultats inesperats.

Els literals en Java poden ser:

- Literals de tipus enter
- Literals de tipus real
- Literals de tipus caràcter
- Literals de cadenes de caràcters

#### Literal Java de tipus enter.
El tipus del literal enter és `int` a menys que el seu valor absolut siga major que el d'un int o que s'especifique el sufix l (ela) o L, cas en què serà de tipus long. El signe + al principi és opcional i el signe – serà obligatori si el número és negatiu.

982                   literal enter de tipus int
-25                   literal enter de tipus int
+1200                 literal enter de tipus int
1234                  literal enter de tipus int
1234L                 literal enter de tipus long. El tipus long l'indica la L
123400000000          literal enter de tipus long. El valor del número supera el rang d'un int


#### Literal Java de tipus real.
Són números en base 10, que han de portar una part sencera, un punt decimal i una part fraccionària. Si la part sencera és zero, es pot ometre. El signe + al principi és opcional i el signe – serà obligatori si el número és negatiu. Per exemple:

12.2303
-3.44
+10.33
0.456
.96

També poden representar-se utilitzant la notació científica. En este cas s'utilitza una E (majúscula o minúscula) seguida de l'exponent (positiu o negatiu). L'exponent està format per dígits del 0 al 9. Per exemple, el número en notació científica 14*10⁻³ s'escriu: 14E-3. Més exemples de literal Java de tipus real:

2.15E2      -> 2.15 * 10²
.0007E4     -> 0.0007 * 10⁴
-50.445e-10 -> -50.445 * 10⁻¹⁰

El tipus d'estos literals és sempre double, a menys que s'afija el sufix F o f per a indicar que és float. Per exemple:

2.15          literal real de tipus double
2.15F         literal real de tipus float
.23e5         literal real de tipus double
+74.336E-2F   literal real de tipus float

També es poden utilitzar els sufixos d o D per a indicar que el literal és de tipus double:
12.002d       literal real de tipus double

Literal Java de tipus caràcter.
Conté un sol caràcter tancat entre cometes simples. És de tipus char. Les seqüències d'escapament es consideren literals de tipus caràcter. Per exemple:

'a'
'4'
'\n'
'\u0061'

#### Literal Java de tipus cadena de caràcters.
Està format per 0 o més caràcters tancats entre cometes dobles. Poden incloure seqüències d'escapament. Per exemple:

"Açò és una cadena de caràcters"
"Prem "C" per a continuar"
""    -> cadena buida
"T"   -> cadena d'un sol caràcter, és diferent de 't' que és un caràcter

Les cadenes de caràcters en Java són objectes de tipus `String`.

!!! warning "Diferència fonamental entre `char` i `String`"
    * `'T'`: És un literal de tipus bàsic primitiu `char`, sempre tancat entre cometes simples (`'`). Només pot contindre un sol caràcter.
    * `"T"`: És un objecte de la classe `String`, tancat entre cometes dobles (`"`). Encara que continga un sol símbol, disposa de mètodes i propietats d'objecte i no es pot assignar directament a una variable de tipus `char`.

### Variables.
Les dades que gestiona un programa s'emmagatzemen en la memòria de l'ordinador. Per a accedir-hi s'utilitza la seua adreça de memòria o posició dins de la memòria on es troba la dada. Per a facilitar la referència a les posicions de memòria, es pot substituir la cadena binària de zeros i uns que indica l'adreça per un identificador.

**Un identificador és el nom que se li dóna a un component dins d'un programa** (una variable, una constant, un mètode, una classe, etc.). Exemple d'identificadors: nom, matriculaAlumne, $suma5, any, etc.

**Definició**: Una variable és una zona de memòria que es referencia amb un identificador, conegut com a nom de la variable, on s'emmagatzema el valor d'una dada **que pot canviar** durant l'execució del programa.

Una variable té tres característiques bàsiques:
- **Nom** o identificador de la variable.
- **Tipus**. Conjunt de valors que pot prendre la variable (numèric, caràcter, etc.).
- **Valor**. Informació que emmagatzema.

Per a poder utilitzar una variable en un programa, primer hem de declarar-la. Declarar una variable significa assignar-li un nom i un tipus. Per exemple:

```java
int a;   //declarem la variable a de tipus int
char b;  //declarem la variable b de tipus char
```

També podem assignar-li un valor inicial a la variable quan es declara:

```java
int x = 5;            //declarem la variable x de tipus int i li assignem el valor 5
char caracter = 'b';  //declarem la variable caràcter de tipus char i li assignem el valor 'b'
double altura = 6.25; //declarem la variable altura de tipus double i li assignem el valor 6.25
int comptador = 0;    //declarem la variable comptador de tipus int i li assignem el valor 0
```

### Constants.
Un programa pot contindre certs valors que no han de canviar durant la seua execució. Estos valors s'anomenen constants.

**Definició**: Una constant és una zona de memòria que es referencia amb un identificador, conegut com a nom de la constant, on s'emmagatzema un valor que no pot canviar durant l'execució del programa.
Una constant en Java es declara de manera similar a una variable, anteposant la paraula final. Exemple:

```java
final double PI = 3.141591;
final int diesSetmana = 7;
```

!!! tip "Bona pràctica: Convenció en el nom de constants"
    En la comunitat Java s'acostuma a escriure el nom de les constants (`final`) en **MAJÚSCULES**, separant les paraules amb un guió baix: `final int DIES_SETMANA = 7;` o `final double PI = 3.14159;`.