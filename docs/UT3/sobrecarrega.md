# Sobrecàrrega de funcions

Java permet que dues o més funcions compartisquen el mateix identificador (nom) dins del mateix fitxer. Aquesta característica s'anomena **sobrecàrrega de funcions** (*function overloading*).

---

## 1. Com funciona la sobrecàrrega?

El compilador de Java sap quina versió exacta de la funció ha d'executar analitzant la **llista d'arguments** utilitzada en la invocació.

Perquè dues funcions puguen sobrecarregar-se, la seua **signatura** (*signature*) ha de ser diferent:

* **Nombre de paràmetres diferent:**
    ```java
    int suma(int a, int b) { ... }
    int suma(int a, int b, int c) { ... }
    ```
* **Tipus de paràmetres diferent:**
    ```java
    int suma(int a, int b) { ... }
    double suma(double a, double b) { ... }
    ```
* **Ordre de tipus diferent:**
    ```java
    void mostraDada(String text, int numero) { ... }
    void mostraDada(int numero, String text) { ... }
    ```

!!! warning "El tipus de retorn NO sobrecarrega"
    El tipus de dada retornat **no forma part de la signatura** utilitzada pel compilador per resoldre la invocació. Per tant, dues funcions amb el mateix nom i idèntics paràmetres, encara que retornen tipus diferents, produiran un **error de compilació** (*method is already defined*):
    ```java
    int calcula(int x) { return x * 2; }
    // ERROR: ja existeix calcula(int)
    double calcula(int x) { return x * 2.5; }
    ```

---

## 2. Exemple pràctic: Suma simple vs Suma ponderada

Suposem que volem implementar una funció per calcular la suma clàssica de dos enters, i també una versió per fer una suma ponderada on cada valor té un determinat pes percentual:

```java
// Versió 1: Suma simple de dos enters
int suma(int a, int b) {
    int resultat;
    resultat = a + b;
    return resultat;
}

// Versió 2: Suma ponderada amb pesos
double suma(int a, double pesA, int b, double pesB) {
    double resultat;
    resultat = (a * pesA + b * pesB) / (pesA + pesB);
    return resultat;
}

void main() {
    // Invoca la versió 1 (2 paràmetres enters) -> Retorna 5
    int s1 = suma(2, 3);
    IO.println("Suma simple: " + s1);

    // Invoca la versió 2 (4 paràmetres: int, double, int, double) -> Retorna 3.25
    double s2 = suma(2, 0.25, 3, 0.75);
    IO.println("Suma ponderada: " + s2);
}
```

---

## 3. Reutilització entre funcions sobrecarregades

Un patró de disseny excel·lent en funcions sobrecarregades consisteix a **fer que una versió invoque l'altra**, evitant duplicar la lògica de càlcul:

```java
// Màxim de 2 nombres
int maxim(int a, int b) {
    int max;
    if (a > b) {
        max = a;
    } else {
        max = b;
    }
    return max;
}

// Màxim de 3 nombres (reutilitza la versió de 2 nombres!)
int maxim(int a, int b, int c) {
    int maxParcial = maxim(a, b); // Crida a maxim(int, int)
    return maxim(maxParcial, c);  // Crida de nou a maxim(int, int)
}

void main() {
    IO.println("Màxim de 5 i 8: " + maxim(5, 8));
    IO.println("Màxim de 5, 12 i 8: " + maxim(5, 12, 8));
}
```

---

## 4. Sobrecàrrega a l'API estàndard de Java

La sobrecàrrega s'utilitza contínuament en Java:

* **`IO.println()` i `IO.print()`**: Estan sobrecarregades per admetre qualsevol tipus de dada: `IO.println(int)`, `IO.println(double)`, `IO.println(boolean)`, `IO.println(String)`, etc.
* **`Math.max()` i `Math.abs()`**: Estan sobrecarregades a la classe `Math` per a suportar de forma transparent tipus `int`, `long`, `float` i `double`.
