# Introducció

A mesura que augmenta l'extensió i la complexitat d'un programa, és habitual haver d'implementar, en diferents parts del codi, la mateixa funcionalitat. Si es resol copiant i apegalant una i altra vegada el mateix fragment de codi, sorgeixen dos problemes greus:

- **Duplicitat de codi:** Incrementa innecessàriament la grandària del programa i en dificulta la lectura i comprensió.
- **Dificultat en el manteniment:** Qualsevol modificació, correcció d'un error o millora en el fragment repetit s'hauria de replicar manualment en tots i cadascun dels llocs on apareix.

Encara que davant de repeticions consecutives podem pensar en una estructura repetitiva (`for`, `while`), quan la funcionalitat es necessita en moments o llocs dispars del flux d'execució, els bucles no són una solució viable.

La **programació modular** proposa una estratègia fonamental en enginyeria del programari: el paradigma de **"divideix i venceràs"** (*divide and conquer*). Consisteix a descompondre un problema complex en subproblemes més menuts i abordables, cadascun resolt mitjançant un mòdul, funció o mètode amb un propòsit clar, aïllat i ben delimitat.

!!! info "Objectius de la Unitat Temàtica 3 (RA2, RA4, RA5)"
    * **Programació modular:** Comprendre el concepte de funció/mètode i els avantatges del disseny modular (reutilització, mantenibilitat, llegibilitat).
    * **Definició i invocació:** Dominar la sintaxi de declaració de funcions estàtiques en Java, la definició de paràmetres i el valor de retorn (`return`).
    * **Pas d'informació:** Interioritzar el mecanisme de pas de paràmetres per valor o per còpia propi de Java.
    * **Àmbit i visibilitat:** Identificar l'abast de les variables locals i de bloc, evitant conflictes i optimitzant l'ús de la memòria.
    * **Sobrecàrrega de funcions:** Dissenyar mètodes sobrecarregats (*overloading*) que comparteixen nom amb llistes de paràmetres diferents.
    * **Recursivitat:** Desenvolupar algorismes recursius identificant de forma rigorosa el cas base i el cas recursiu.
    * **API de Java:** Conéixer i aprofitar les classes i funcions de la biblioteca estàndard (com `java.lang.Math`) i aprendre a consultar la documentació oficial d'Oracle.
