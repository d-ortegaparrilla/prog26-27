# Organització del codi: Classes i mètodes estàtics

Fins ara hem treballat amb fitxers compactes (*compact files*) on declaràvem les funcions i el mètode `void main()` junts en un únic fitxer. Aquesta aproximació és ideal per a aprendre la lògica algorísmica i resoldre problemes concrets.

No obstant això, en projectes de programari reals el codi augmenta ràpidament i mantindre desenes o centenars de funcions en un sol document esdevé caòtic i poc mantenible. La solució natural consisteix a **dividir el codi entre diversos fitxers**.

---

## 1. La classe com a agrupador de funcions

En Java, qualsevol bloc de codi que vulga ser compartit o reutilitzat des d'altres fitxers s'organitza formalment dins d'una **classe** (`class`).

!!! info "La classe com a mòdul contenidor (sense entrar en la POO)"
    Encara que a la Unitat Temàtica 4 estudiarem en profunditat el paradigma de la **Programació Orientada a Objectes** (classes, instàncies, atributs d'estat, constructors, herència...), en aquest moment del curs considerarem una classe simplement com una **biblioteca, mòdul o contenidor** que serveix per agrupar i encapsular funcions amb una temàtica comuna (per exemple, operacions aritmètiques, càlculs geomètrics, utilitats de format, etc.).

La sintaxi bàsica per a definir una classe en el seu propi fitxer és:

```java
public class NomClasse {
    // Conjunt de funcions relacionades
}
```

Per convenció estricta en Java:
1. El nom de la classe s'escriu en estil **PascalCase** (la primera lletra en majúscula: `Calculs`, `Geometria`, `Validacions`).
2. El nom del fitxer a disc ha de coincidir **exactament** amb el nom de la classe i portar l'extensió `.java` (per exemple, `Geometria.java`).

---

## 2. Mètodes estàtics (`static`)

Quan definim funcions dins d'una classe amb l'objectiu que puguen ser invocades des d'un altre fitxer sense necessitat de crear cap objecte en memòria, **totes aquestes funcions s'han de declarar com a mètodes `static`**:

```java
public class Aritmetica {
    
    // Mètode estàtic: pertany a la classe Aritmetica
    public static int suma(int a, int b) {
        return a + b;
    }

    // Un altre mètode estàtic
    public static int resta(int a, int b) {
        return a - b;
    }
}
```

* **`public`**: Modificador de visibilitat que permet que la classe o mètode siga accessible des d'altres fitxers del projecte.
* **`static`**: Indica que el mètode pertany a la classe en general i no a una instància particular. Gràcies a `static`, podem executar la funció directament fent referència al nom de la classe.

---

## 3. Com invocar mètodes d'un altre fitxer

Per a executar una funció `static` que es troba definida en una altra classe, la sintaxi consisteix a indicar el **nom de la classe**, seguit d'un punt **`.`** i el nom del mètode amb els seus arguments:

```java
NomClasse.nomMetode(arguments);
```

### Exemple complet de divisió en dos fitxers

Imaginem que tenim dos fitxers ubicats dins de la mateixa carpeta de treball del nostre projecte:

=== "Fitxer de biblioteca: `Geometria.java`"

    ```java
    public class Geometria {

        // Calcula l'àrea d'un rectangle
        public static double areaRectangle(double base, double altura) {
            return base * altura;
        }

        // Calcula el perímetre d'un rectangle
        public static double perimetreRectangle(double base, double altura) {
            return 2 * (base + altura);
        }
    }
    ```

=== "Fitxer del programa principal: `Principal.java`"

    ```java
    void main() {
        double b = 5.0;
        double h = 3.0;

        // Invoquem els mètodes estàtics precedits del nom de la classe
        double area = Geometria.areaRectangle(b, h);
        double perimetre = Geometria.perimetreRectangle(b, h);

        IO.println("Base: " + b + ", Altura: " + h);
        IO.println("Àrea del rectangle: " + area);
        IO.println("Perímetre del rectangle: " + perimetre);
    }
    ```

Quan Java compila i executa `Geometria.areaRectangle(b, h)`, busca automàticament la classe `Geometria` en el mateix directori, localitza el mètode estàtic `areaRectangle`, n'executa les instruccions i en retorna el resultat al programa principal.

---

## 4. Connexió amb l'API estàndard de Java

Ara que ja coneixes el funcionament de la sintaxi `NomClasse.nomMetode()`, comprendràs d'on provenen moltes de les crides estàndard de Java que ja hem utilitzat:

* `Math.sqrt(...)` o `Math.pow(...)` són precisament mètodes `static` que residixen dins de la classe `Math`.
* `Integer.parseInt(...)` és un mètode `static` contingut a la classe `Integer`.
* `IO.println(...)` o `IO.readln()` són mètodes `static` de la classe `IO`.

En el següent apartat veurem amb detall l'**API estàndard de Java** i com aprofitar la classe `Math` per als nostres càlculs.
