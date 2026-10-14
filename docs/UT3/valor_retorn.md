# Valor retornat per una funció

Fins ara hem vist com enviar informació cap a la funció mitjançant paràmetres d'entrada. No obstant això, en la majoria de casos el programa principal necessita rebre el resultat calculat per la funció per a utilitzar-lo en altres càlculs, condicions o assignacions.

Aquest flux d'informació de tornada s'aconsegueix especificant un **tipus de retorn** i utilitzant la sentència **`return`**.

---

## 1. La instrucció `return`

La sentència `return` compleix dues funcions simultànies:

1. **Finalitza immediatament** l'execució de la funció.
2. **Retorna el valor** especificat cap al punt del programa on es va realitzar la invocació.

```java
tipusRetorn nomFuncio(paràmetres) {
    // Càlculs...
    return valor;
}
```

On `valor` ha de ser del mateix tipus (o d'un tipus compatible per promoció implícita) que `tipusRetorn`.

### Exemple: Funció que retorna un enter

```java
int suma(int x, int y) {
    int resultat;
    resultat = x + y;
    return resultat; // Retorna el resultat de la suma
}
```

En invocar aquesta funció des del `void main()`, la crida es **substitueix pel valor retornat**:

```java
void main() {
    int a = suma(2, 3);          // suma(2, 3) esdevé 5 -> a = 5
    int b = suma(7, 1) * 5;      // suma(7, 1) esdevé 8 -> b = 8 * 5 = 40
    IO.println("a = " + a);
    IO.println("b = " + b);
}
```

---

## 2. Funcions `void` vs Funcions amb retorn

* **Funcions `void`:** Indiquen que la funció no retorna cap dada (solen anomenar-se *procediments* o accions). Poden ometre el `return` o utilitzar un `return;` sense paràmetres simplement per finalitzar l'execució.
* **Funcions amb tipus concret (`int`, `double`, `boolean`, `String`...):** És **obligatori** que tots els camins d'execució de la funció acaben amb una sentència `return` que proporcione un valor del tipus promés. En cas contrari, el compilador donarà un error: `missing return statement`.

---

## 3. Bones pràctiques: Únic punt d'eixida

Encara que Java permet col·locar múltiples sentències `return` dins d'una mateixa funció (per exemple, dins de branques `if-else`), les bones pràctiques d'enginyeria del programari aconsellen el principi de **punt únic d'entrada i únic punt d'eixida**:

=== "Pràctica desaconsellada (múltiples returns)"

    ```java
    boolean esPositiu(int n) {
        if (n >= 0) {
            return true;  // Primer punt d'eixida
        } else {
            return false; // Segon punt d'eixida
        }
    }
    ```

=== "Bona pràctica (únic return al final)"

    ```java
    boolean esPositiu(int n) {
        boolean resultat;
        
        if (n >= 0) {
            resultat = true;
        } else {
            resultat = false;
        }
        
        return resultat; // Únic punt d'eixida al final de la funció
    }
    ```

!!! tip "Per què un únic return?"
    * **Llegibilitat:** Saps amb certesa on acaba la funció (a l'última línia).
    * **Manteniment:** Si en el futur cal afegir una neteja de recursos, logs o modificacions prèvies al retorn, només cal col·locar-les abans de l'únic `return`.
    * **Depuració:** Facilita establir punts de ruptura (*breakpoints*) per inspeccionar el valor final exacte abans que la funció retorne el control.
