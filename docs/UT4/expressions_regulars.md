# Expressions regulars en Java

Una **expressió regular** (coneguda com a ***regex***, de l'anglés *regular expression*) descriu un **patró formal de cerca o concordança** en un text.

En compte de buscar una paraula exacta i fixa (com `"hola"`), les expressions regulars permeten formular criteris flexibles com ara: *"un text que continga una lletra majúscula seguida de tres dígits i acabe en una vocal"*, *"una adreça de correu electrònic vàlida"* o *"un número de telèfon amb prefix internacional opcional"*.

Són una eina indispensable per a:

1. **Validació d'entrades de dades:** Comprovar si un formulari conté un format correcte de DNI, codi postal, targeta de crèdit, contrasenya, etc.
2. **Cerca i extracció d'informació:** Trobar totes les ocurrències d'un determinat patró dins d'un text extens.
3. **Substitució i neteja:** Transformar o emmascarar dades que compleixen un determinat criteri.

---

## 1. Caràcters escapats a Java

En la sintaxi de regex, la **barra invertida (`\`)** és un caràcter especial que s'utilitza per a indicar símbols predefinits (per exemple, `\d` representa qualsevol dígit del 0 al 9).

No obstant això, en Java, la barra invertida també és el caràcter d'escapament propi dels literals de cadena (`\n`, `\t`, `\"`). Per tant, si volem que la regex reba una barra invertida, **cal escapar-la amb una altra barra invertida**:

```java
String patroRegex = "\\d"; // A Java escrivim dues barres per a representar \d
```

Si volem buscar literalment el caràcter d'una barra invertida en el text, haurem d'escriure fins a quatre barres: `"\\\\"`.

---

## 2. Metacaràcters i classes de caràcters predefinides

Java proporciona abreviatures per als tipus de caràcters més habituals:

| Metacaràcter | En Java | Significat | Exemples que encaixen |
| :---: | :---: | :--- | :--- |
| **`.`** | `"."` | **Qualsevol caràcter** (excepte salts de línia). | En `.ose`: `"rose"`, `"nose"`, `"3ose"` |
| **`\d`** | `"\\d"` | **Dígit numèric** (equivalent a `[0-9]`). | `'0'`, `'5'`, `'9'` |
| **`\D`** | `"\\D"` | **No dígit** (qualsevol caràcter que no siga número). | `'a'`, `' '`, `'$'` |
| **`\s`** | `"\\s"` | **Espai en blanc** (espai, tabulació `\t`, salt de línia `\n`, retorn `\r`). | `' '`, `'\t'`, `'\n'` |
| **`\S`** | `"\\S"` | **No espai en blanc** (qualsevol caràcter visible). | `'x'`, `'7'`, `'@'` |
| **`\w`** | `"\\w"` | **Caràcter de paraula** (lletres `a-z`, `A-Z`, dígits `0-9` i subratllat `_`). | `'a'`, `'Z'`, `'3'`, `'_'` |
| **`\W`** | `"\\W"` | **No caràcter de paraula** (signes de puntuació, espais, símbols). | `'!'`, `' '`, `'+'`, `'.'` |

---

## 3. Classes de caràcters personalitzades

Podem definir conjunts específics de caràcters utilitzant **corxets `[ ]`**:

| Sintaxi | Descripció | Exemple | Coincideix amb |
| :--- | :--- | :--- | :--- |
| `[abc]` | Qualsevol dels caràcters llistats. | `[aeiou]` | Qualsevol vocal minúscula |
| `[a-z]` | **Rang** de caràcters consecutius. | `[0-9]` o `[A-Z]` | Qualsevol dígit o lletra majúscula |
| `[^abc]` | **Negació:** qualsevol caràcter **excepte** els indicats. | `[^0-9]` | Qualsevol símbol que no siga dígit |
| `[a-d[m-p]]` | **Unió:** caràcters d'un rang o de l'altre. | `[a-c[x-z]]` | `a, b, c, x, y, z` |
| `[a-z&&[def]]` | **Intersecció:** caràcters comuns a ambdós conjunts. | `[a-z&&[^aeiou]]` | Qualsevol consonant minúscula |

---

## 4. Marcadors de posició (Ancoratges)

Els ancoratges no coincideixen amb cap caràcter físic, sinó amb una **posició** dins del text:

| Símbol | Descripció | Exemple | Explicació |
| :---: | :--- | :--- | :--- |
| **`^`** | **Principi** de línia o de cadena. | `^[0-9]` | El text ha de començar obligatòriament per un dígit |
| **`$`** | **Final** de línia o de cadena. | `\.$` | El text ha d'acabar obligatòriament en un punt |
| **`\b`** | **Límit de paraula** (*word boundary*). | `\brose\b` | La paraula `"rose"` aïllada (no coincideix amb `"roser"` ni `"prose"`) |
| **`\B`** | **No límit de paraula**. | `\Brose` | Coincideix amb `"prose"`, però no amb `"rose"` |

---

## 5. Quantificadors (Multiplicitat)

Els quantificadors indiquen quantes vegades consecutives pot o ha d'aparéixer l'element que tenen immediatament a la seua esquerra:

| Quantificador | Freqüència d'aparició | Descripció | Exemple |
| :---: | :--- | :--- | :--- |
| **`*`** | **$0$ o més vegades** | Opcional, es pot repetir de manera il·limitada. | `0*\d` (zero o més zeros seguits d'un dígit) |
| **`+`** | **$1$ o més vegades** | Obligatori almenys una vegada, es pot repetir. | `\d+` (un o més dígits consecutius) |
| **`?`** | **$0$ o $1$ vegada** | Totalment opcional (apareix una vegada o cap). | `\d\d/?\d\d` (barra intermèdia opcional) |
| **`{n}`** | **Exactament $n$ vegades** | Nombre fix i invariable d'ocurrències. | `\d{8}` (exactament 8 dígits) |
| **`{n,m}`** | **Entre $n$ i $m$ vegades** | Mínim $n$ vegades i màxim $m$ vegades. | `\w{5,8}` (paraules d'entre 5 i 8 caràcters) |
| **`{n,}`** | **Almenys $n$ vegades** | Mínim $n$, sense límit superior. | `\d{3,}` (tres o més dígits) |

---

## 6. Alternança i agrupació

* **Alternança (`|`):** Actua com l'operador lògic OR. Permet triar entre diferents alternatives.
* **Agrupació `( )`:** Agrupa una subexpressió per a aplicar-li un quantificador o limitar l'abast d'una alternança.

```text
\w+@[\w.]+\.(net|edu|gov|es)
```

En aquest patró, el grup `(net|edu|gov|es)` indica que el domini de l'adreça de correu ha de ser obligatòriament una d'aquestes quatre opcions.

---

## 7. Ús d'expressions regulars en Java

En Java podem emprar les expressions regulars de dues formes:

### 7.1 Mètodes directes de la classe `String`

Per a validacions ràpides i substitucions directes, la pròpia classe `String` ofereix mètodes molt còmodes:

=== "`matches(regex)`: Validació completa"
    El mètode `matches()` comprova si **tota la cadena completa** encaixa amb el patró:
    ```java
    String codiPostal = "03610";
    if (codiPostal.matches("\\d{5}")) {
        IO.println("Codi postal vàlid.");
    }
    ```

=== "`replaceAll(regex, nou)`: Substitució"
    Substitueix totes les ocurrències que coincidisquen amb el patró per un altre text:
    ```java
    String text = "L'usuari 10 va comprar 4 llibres per 25 euros.";
    // Ocultem tots els números per asteriscs
    String censurat = text.replaceAll("\\d+", "[NÚMERO]");
    IO.println(censurat);
    // Eixida: L'usuari [NÚMERO] va comprar [NÚMERO] llibres per [NÚMERO] euros.
    ```

=== "`split(regex)`: Divisió avançada"
    Separa un text emprant patrons complexos (com un o més espais o signes de puntuació):
    ```java
    String csv = "Joan; ; Maria,   Pere;;Lluís";
    // Dividim per qualsevol combinació de comes, punts i comes i espais
    String[] noms = csv.split("[,;\\s]+");
    ```

### 7.2 El paquet `java.util.regex` (`Pattern` i `Matcher`)

Quan necessitem compilar patrons per a reutilitzar-los eficientment, aplicar modificadors (com ignorar majúscules/minúscules) o cercar múltiples ocurrències dins d'un text obtenint la seua posició, s'utilitzen les classes **`Pattern`** i **`Matcher`** del paquet `java.util.regex`:

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;
```

* **`Pattern`:** Representa el patró compilat en memòria mitjançant `Pattern.compile(patro, flags)`.
* **`Matcher`:** És el motor que recorre el text i gestiona les coincidències.

Principals mètodes de `Matcher`:

* `matcher.find()`: Cerca la següent coincidència en el text (retorna `true` si en troba una altra).
* `matcher.group()`: Retorna el text exacte que ha coincidit.
* `matcher.start()`: Retorna l'índex de posició del primer caràcter de la coincidència.
* `matcher.end()`: Retorna l'índex de la posició immediatament posterior a la coincidència.

---

## 8. Exemples pràctics resolts

### Exemple 1: Cerca i localització de patrons en un text

El programa cerca totes les aparicions de les paraules `"horse"` o `"course"` en una frase, mostrant el text detectat i la seua posició numèrica exacta en caràcters.

??? example "Solució en Java"
    ```java
    import java.util.regex.Pattern;
    import java.util.regex.Matcher;

    /*
     * Programa que localitza totes les ocurrències d'un patró compost
     * dins d'un text emprant Pattern i Matcher.
     */
    void main() {
        String text = "A horse is a horse, of course of course...";
        String patro = "horse|course";

        // Compilem el patró
        Pattern pattern = Pattern.compile(patro);
        Matcher matcher = pattern.matcher(text);

        IO.println("Cercant coincidències en el text...\n");
        while (matcher.find()) {
            IO.println("Coincidència: '" + matcher.group() + 
                       "' a la posició d'inici " + matcher.start() +
                       " (fins a " + matcher.end() + ")");
        }
    }
    ```

---

### Exemple 2: Validació de format de DNI i correu electrònic

El programa sol·licita a l'usuari un DNI (8 dígits i una lletra majúscula) i una adreça de correu electrònic corporativa o general, verificant-ne el format mitjançant `matches()`.

??? example "Solució en Java"
    ```java
    /*
     * Programa que valida formats d'entrada habituals (DNI i Email)
     * mitjançant expressions regulars amb String.matches().
     */
    void main() {
        IO.print("Introdueix un DNI (8 xifres i 1 lletra majúscula, ex: 12345678Z): ");
        String dni = IO.readln().trim();

        // Patró DNI: exactament 8 dígits seguits d'una lletra de la A a la Z majúscula
        String patroDni = "^[0-9]{8}[A-Z]$";

        if (dni.matches(patroDni)) {
            IO.println("El format de DNI és CORRECTE.");
        } else {
            IO.println("Format de DNI INCORRECTE! Han de ser 8 dígits i una majúscula.");
        }

        IO.print("\nIntrodueix el teu correu electrònic: ");
        String email = IO.readln().trim();

        // Patró d'email simplificat
        String patroEmail = "^[\\w.-]+@[\\w.-]+\\.[a-zA-Z]{2,6}$";

        if (email.matches(patroEmail)) {
            IO.println("L'adreça de correu és vàlida.");
        } else {
            IO.println("Adreça de correu no vàlida!");
        }
    }
    ```
