# L'API de Java i la classe Math

Java inclou de sèrie una biblioteca de classes i mètodes molt potent coneguda com l'**API de Java** (*Application Programming Interface*). Aquesta biblioteca proporciona milers de funcionalitats ja implementades i altament optimitzades, agrupades en paquets (*packages*).

El paquet bàsic del sistema és **`java.lang`**, que conté classes essencials com `System`, `String` o `Math`. Com que és indispensable, `java.lang` s'importa de forma **automàtica** en tots els fitxers Java sense necessitat d'escriure la sentència `import`.

---

## 1. La classe `java.lang.Math`

La classe `Math` conté un conjunt de mètodes i constants estàtiques per a realitzar càlculs numèrics, operacions algebraiques i funcions trigonomètriques avançades.

Com que tots els seus membres són **estàtics (`static`)**, no cal instanciar cap objecte: s'invoquen directament precedits del nom de la classe: `Math.nomMetode()`.

### Constants matemàtiques

* **`Math.PI`**: El valor del nombre π ≈ 3.141592653589793.
* **`Math.E`**: La base dels logaritmes naturals *e* ≈ 2.718281828459045.

---

## 2. Principals mètodes estàtics de `Math`

| Mètode | Descripció | Exemple | Resultat |
| :--- | :--- | :--- | :--- |
| `Math.abs(x)` | Retorna el valor absolut de `x` (sense signe). | `Math.abs(-7.5)` | `7.5` |
| `Math.max(a, b)` | Retorna el major dels dos valors. | `Math.max(12, 25)` | `25` |
| `Math.min(a, b)` | Retorna el menor dels dos valors. | `Math.min(12, 25)` | `12` |
| `Math.pow(base, exp)` | Retorna la potència base<sup>exp</sup> com a `double`. | `Math.pow(2, 3)` | `8.0` |
| `Math.sqrt(x)` | Retorna l'arrel quadrada √x com a `double`. | `Math.sqrt(25.0)` | `5.0` |
| `Math.floor(x)` | Trunca cap a baix (el major enter ≤ x). | `Math.floor(4.9)` | `4.0` |
| `Math.ceil(x)` | Arredoneix cap a dalt (el menor enter ≥ x). | `Math.ceil(4.1)` | `5.0` |
| `Math.round(x)` | Arredoneix a l'enter més proper. | `Math.round(4.6)` | `5` |
| `Math.random()` | Retorna un nombre real aleatori en el rang `[0.0, 1.0)`. | `Math.random()` | `0.7423...` |
| `Math.sin(rad)` | Retorna el sinus de l'angle en radians. | `Math.sin(Math.PI / 2)` | `1.0` |
| `Math.cos(rad)` | Retorna el cosinus de l'angle en radians. | `Math.cos(0)` | `1.0` |
| `Math.log(x)` | Retorna el logaritme natural (base *e*) de `x`. | `Math.log(Math.E)` | `1.0` |

---

## 3. Generació de nombres aleatoris amb `Math.random()`

El mètode `Math.random()` genera un valor de tipus `double` tal que:

```text
0.0 <= Math.random() < 1.0
```

> **Rang semiobert `[0.0, 1.0)`:** Pot retornar el `0.0`, però mai arriba a ser `1.0` (el valor màxim possible és `0.999999...`).

Per a generar nombres enters aleatoris compresos dins d'un rang tancat `[min, max]`, s'utilitza la fórmula general:

```text
enterAleatori = min + (int) (Math.random() * (max - min + 1))
```

En codi Java, utilitzant un càsting explícit a `int`:

```java
int min = 1;
int max = 6; // Simulem el llançament d'un dau de 6 cares
int dau = min + (int) (Math.random() * (max - min + 1));
IO.println("Ha eixit un: " + dau);
```

---

## 4. Com consultar la documentació oficial (Javadoc)

Com a desenvolupador professional, és fonamental saber interpretar la documentació oficial d'Oracle.

* **Enllaç a la documentació oficial:** [Oracle Java SE API Specification](https://docs.oracle.com/en/java/javase/25/docs/api/index.html)

Quan consultes la documentació d'una classe a l'API oficial de Java, presta especial atenció a:

1. **El paquet (*Package*):** Indica on resideix la classe i si requereix sentència `import`.
2. **Modificadors i tipus de retorn (*Modifier and Type*):** Si diu `static`, s'invoca amb la classe (`Math.abs()`). Si diu `double`, sabràs quin tipus de variable has d'utilitzar per recollir el resultat.
3. **Paràmetres esperats:** El tipus i ordre de les dades requerides.
4. **Casos especials i excepcions:** Què retorna si el paràmetre és `NaN`, negatiu o zero, o si pot llançar alguna excepció.
